# SystemVerilog Cheat Sheet

A quick reference for basic SystemVerilog syntax, RTL design, FSMs, testbenches, and waveform/debug usage.

---

## 🧹 Basic Module Template

Basic structure for a simple RTL module.

```systemverilog
module my_module (
    input  logic clk,
    input  logic rst_n,
    input  logic a,
    input  logic b,
    output logic y
);

    always_comb begin
        y = a & b;
    end

endmodule
```

---

## ⚡ Basic Sequential Template

Use `always_ff` for clocked logic.

```systemverilog
module seq_example (
    input  logic clk,
    input  logic rst_n,
    input  logic d,
    output logic q
);

    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n)
            q <= 1'b0;
        else
            q <= d;
    end

endmodule
```

---

## 🔀 Basic Combinational Template

Use `always_comb` for combinational logic.

```systemverilog
module comb_example (
    input  logic a,
    input  logic b,
    input  logic sel,
    output logic y
);

    always_comb begin
        if (sel)
            y = a;
        else
            y = b;
    end

endmodule
```

---

## 📦 Continuous Assignment

Useful for simple combinational expressions.

```systemverilog
module assign_example (
    input  logic a,
    input  logic b,
    output logic y
);

    assign y = a | b;

endmodule
```

---

## 🔢 Parameters

Use parameters to make modules reusable.

```systemverilog
module register #(
    parameter int WIDTH = 8
)(
    input  logic             clk,
    input  logic             rst_n,
    input  logic [WIDTH-1:0] d,
    output logic [WIDTH-1:0] q
);

    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n)
            q <= '0;
        else
            q <= d;
    end

endmodule
```

---

## 🧮 Vector Declaration

Define buses and signals with width.

```systemverilog
logic        a;
logic [7:0]  data;
logic [15:0] addr;
```

---

## 🔍 Bit Select and Part Select

Access individual bits or ranges.

```systemverilog
logic [7:0] data;
logic bit0;
logic [3:0] upper_nibble;

assign bit0         = data[0];
assign upper_nibble = data[7:4];
```

---

## 🧩 Concatenation

Combine signals into a larger bus.

```systemverilog
logic [3:0] a, b;
logic [7:0] y;

assign y = {a, b};
```

---

## 🔁 Replication

Repeat the same bit or bus multiple times.

```systemverilog
logic [7:0] mask;

assign mask = {8{1'b1}};
```

---

## ✅ If / Else

Basic conditional logic.

```systemverilog
always_comb begin
    if (a > b)
        y = a;
    else
        y = b;
end
```

---

## 📚 Case Statement

Useful for muxes, decoders, and control logic.

```systemverilog
always_comb begin
    case (sel)
        2'b00: y = a;
        2'b01: y = b;
        2'b10: y = c;
        default: y = '0;
    endcase
end
```

---

## 🧠 Unique Case

Helps describe mutually exclusive branches.

```systemverilog
always_comb begin
    unique case (state)
        IDLE: y = 2'b00;
        RUN : y = 2'b01;
        DONE: y = 2'b10;
        default: y = 2'b00;
    endcase
end
```

---

## ⏱️ Counter Template

Basic synchronous counter.

```systemverilog
module counter #(
    parameter int WIDTH = 8
)(
    input  logic             clk,
    input  logic             rst_n,
    input  logic             en,
    output logic [WIDTH-1:0] count
);

    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n)
            count <= '0;
        else if (en)
            count <= count + 1'b1;
    end

endmodule
```

---

## 📥 Shift Register

Useful for serial data and pipelines.

```systemverilog
module shift_register #(
    parameter int WIDTH = 8
)(
    input  logic             clk,
    input  logic             rst_n,
    input  logic             shift_en,
    input  logic             serial_in,
    output logic [WIDTH-1:0] data_o
);

    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n)
            data_o <= '0;
        else if (shift_en)
            data_o <= {data_o[WIDTH-2:0], serial_in};
    end

endmodule
```

---

## 🧱 Generate Loop

Instantiate repeated logic blocks.

```systemverilog
module gen_example (
    input  logic [3:0] a,
    input  logic [3:0] b,
    output logic [3:0] y
);

    genvar i;
    generate
        for (i = 0; i < 4; i++) begin : gen_and
            assign y[i] = a[i] & b[i];
        end
    endgenerate

endmodule
```

---

## 🧰 Function

Useful for compact combinational calculations.

```systemverilog
function automatic logic [7:0] add_one (
    input logic [7:0] value
);
    add_one = value + 1'b1;
endfunction
```

---

## 🛠️ Task

Useful in testbenches for repeated stimulus.

```systemverilog
task automatic send_bit(input logic bit_value);
    begin
        data_i = bit_value;
        valid_i = 1'b1;
        #10;
        valid_i = 1'b0;
        #10;
    end
endtask
```

---

# FSM

---

## 🚦 Simple FSM Template

Standard 2-process FSM: one sequential block and one combinational block.

```systemverilog
module fsm_simple (
    input  logic clk,
    input  logic rst_n,
    input  logic start,
    output logic done
);

    typedef enum logic [1:0] {
        IDLE,
        RUN,
        FINISH
    } state_t;

    state_t state, next_state;

    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n)
            state <= IDLE;
        else
            state <= next_state;
    end

    always_comb begin
        next_state = state;
        done = 1'b0;

        case (state)
            IDLE: begin
                if (start)
                    next_state = RUN;
            end

            RUN: begin
                next_state = FINISH;
            end

            FINISH: begin
                done = 1'b1;
                next_state = IDLE;
            end

            default: begin
                next_state = IDLE;
            end
        endcase
    end

endmodule
```

---

## 🚦 FSM with Output Logic Separated

3-process style: state register, next-state logic, output logic.

```systemverilog
module fsm_three_process (
    input  logic clk,
    input  logic rst_n,
    input  logic start,
    output logic busy,
    output logic done
);

    typedef enum logic [1:0] {
        S_IDLE,
        S_RUN,
        S_DONE
    } state_t;

    state_t state, next_state;

    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n)
            state <= S_IDLE;
        else
            state <= next_state;
    end

    always_comb begin
        next_state = state;

        case (state)
            S_IDLE: if (start) next_state = S_RUN;
            S_RUN : next_state = S_DONE;
            S_DONE: next_state = S_IDLE;
            default: next_state = S_IDLE;
        endcase
    end

    always_comb begin
        busy = 1'b0;
        done = 1'b0;

        case (state)
            S_IDLE: begin
                busy = 1'b0;
                done = 1'b0;
            end

            S_RUN: begin
                busy = 1'b1;
                done = 1'b0;
            end

            S_DONE: begin
                busy = 1'b0;
                done = 1'b1;
            end
        endcase
    end

endmodule
```

---

# Testbench

---

## 🧪 Basic Testbench Template

Simple testbench with clock generation and DUT instantiation.

```systemverilog
module tb_my_module;

    logic clk;
    logic rst_n;
    logic a;
    logic b;
    logic y;

    my_module dut (
        .clk   (clk),
        .rst_n (rst_n),
        .a     (a),
        .b     (b),
        .y     (y)
    );

    initial clk = 0;
    always #5 clk = ~clk;

    initial begin
        rst_n = 0;
        a = 0;
        b = 0;

        #20;
        rst_n = 1;

        #10 a = 1;
        #10 b = 1;
        #20 a = 0;
        #20 $finish;
    end

endmodule
```

---

## ⏲️ Reset Sequence

Simple reset pulse at the start of simulation.

```systemverilog
initial begin
    rst_n = 1'b0;
    #20;
    rst_n = 1'b1;
end
```

---

## 🕒 Clock Generation

Basic clock generator.

```systemverilog
initial clk = 1'b0;
always #5 clk = ~clk;
```

---

## 🖨️ Display Signals

Print values during simulation.

```systemverilog
initial begin
    $display("Start simulation");
    $monitor("t=%0t a=%0b b=%0b y=%0b", $time, a, b, y);
end
```

---

## ✅ Wait for Condition

Pause until a signal changes to a desired value.

```systemverilog
initial begin
    wait(done == 1'b1);
    $display("Operation finished at t=%0t", $time);
end
```

---

## 🔁 Repeat Block

Repeat an action multiple times.

```systemverilog
initial begin
    repeat (10) begin
        #10 data_i = $urandom_range(0, 1);
    end
end
```

---

## 🎲 Random Stimulus

Generate random values for testing.

```systemverilog
initial begin
    repeat (8) begin
        #10 a = $urandom_range(0, 1);
        b = $urandom_range(0, 1);
    end
end
```

---

## 📥 Task-Based Stimulus

Cleaner way to send repeated input patterns.

```systemverilog
task automatic send_byte(input logic [7:0] value);
    begin
        data_i  = value;
        valid_i = 1'b1;
        #10;
        valid_i = 1'b0;
        #10;
    end
endtask

initial begin
    send_byte(8'h12);
    send_byte(8'hA5);
    send_byte(8'hFF);
end
```

---

# Waveform / Internal Signals / Hierarchical Access

---

## 📡 Dump Waveform

Generate waveform file for GTKWave or another viewer.

```systemverilog
initial begin
    $dumpfile("wave.vcd");
    $dumpvars(0, tb_my_module);
end
```

---

## 🔍 Dump Specific Blocks

Dump only selected hierarchy levels.

```systemverilog
initial begin
    $dumpfile("wave.vcd");
    $dumpvars(0, tb_my_module.dut);
end
```

---

## 🧠 Hierarchical Signal Access

Access an internal DUT signal directly from the testbench.

```systemverilog
initial begin
    #50;
    $display("internal_state = %0d", tb_my_module.dut.state);
end
```

---

## 🧠 Hierarchical Access to Deep Signals

Access signals inside submodules without adding top-level ports.

```systemverilog
initial begin
    #100;
    $display("internal_counter = %0d", tb_my_module.dut.u_ctrl.counter_reg);
end
```

---

## 📈 Monitor Internal Signals

Print internal DUT signals during simulation.

```systemverilog
initial begin
    $monitor("t=%0t state=%0d counter=%0d",
             $time,
             tb_my_module.dut.state,
             tb_my_module.dut.u_ctrl.counter_reg);
end
```

---

## ⚠️ Force a Signal in Simulation

Temporarily override a signal during simulation.

```systemverilog
initial begin
    #50;
    force tb_my_module.dut.internal_en = 1'b1;
    #20;
    release tb_my_module.dut.internal_en;
end
```

---

## 🧪 Check Internal Value

Simple check using hierarchical reference.

```systemverilog
initial begin
    #100;
    if (tb_my_module.dut.state != 2'b01)
        $display("Unexpected state at t=%0t", $time);
end
```

---

# Arrays and Memories

---

## 📚 Packed Array

Useful for buses and vectors.

```systemverilog
logic [7:0] data;
logic [31:0] word;
```

---

## 🗂️ Unpacked Array

Useful for memory-like structures.

```systemverilog
logic [7:0] mem [0:15];
```

---

## 📥 Initialize Memory

Assign values to a memory array.

```systemverilog
initial begin
    mem[0] = 8'h12;
    mem[1] = 8'h34;
    mem[2] = 8'h56;
end
```

---

## 🔁 Loop Through Memory

Read or write multiple entries.

```systemverilog
integer i;

initial begin
    for (i = 0; i < 16; i++) begin
        mem[i] = i;
    end
end
```

---

# Useful RTL Patterns

---

## 🧱 Default Assignment in always_comb

Avoid unintended latches.

```systemverilog
always_comb begin
    y = 1'b0;

    if (en)
        y = a & b;
end
```

---

## 🚫 Latch Avoidance

Always assign outputs in all branches.

```systemverilog
always_comb begin
    if (sel)
        y = a;
    else
        y = b;
end
```

---

## 🪜 Priority Logic

Priority with ordered `if / else if`.

```systemverilog
always_comb begin
    if (req[3])
        grant = 4'b1000;
    else if (req[2])
        grant = 4'b0100;
    else if (req[1])
        grant = 4'b0010;
    else if (req[0])
        grant = 4'b0001;
    else
        grant = 4'b0000;
end
```

---

## 🧭 One-Cycle Pulse

Generate a single-cycle pulse from an input edge.

```systemverilog
logic sig_d;
logic pulse;

always_ff @(posedge clk or negedge rst_n) begin
    if (!rst_n) begin
        sig_d <= 1'b0;
        pulse <= 1'b0;
    end else begin
        sig_d <= sig;
        pulse <= sig & ~sig_d;
    end
end
```

---

## 📌 Simple Register with Enable

Very common RTL pattern.

```systemverilog
always_ff @(posedge clk or negedge rst_n) begin
    if (!rst_n)
        reg_q <= '0;
    else if (en)
        reg_q <= reg_d;
end
```

---

# Assertions / Checks

---

## ✅ Immediate Check

Basic verification inside testbench logic.

```systemverilog
initial begin
    #50;
    if (y !== expected_y)
        $display("Mismatch at t=%0t", $time);
end
```

---

## 🛑 Fatal Error

Stop simulation when something is wrong.

```systemverilog
initial begin
    #100;
    if (done !== 1'b1)
        $fatal("DONE was not asserted");
end
```

---

# Full Example

---

## 🧠 RTL + Testbench Mini Example

Small example combining DUT, clock, reset, waveform dump, and internal access.

```systemverilog
module pulse_gen (
    input  logic clk,
    input  logic rst_n,
    input  logic sig,
    output logic pulse
);

    logic sig_d;

    always_ff @(posedge clk or negedge rst_n) begin
        if (!rst_n) begin
            sig_d <= 1'b0;
            pulse <= 1'b0;
        end else begin
            sig_d <= sig;
            pulse <= sig & ~sig_d;
        end
    end

endmodule

module tb_pulse_gen;

    logic clk;
    logic rst_n;
    logic sig;
    logic pulse;

    pulse_gen dut (
        .clk   (clk),
        .rst_n (rst_n),
        .sig   (sig),
        .pulse (pulse)
    );

    initial clk = 0;
    always #5 clk = ~clk;

    initial begin
        $dumpfile("wave.vcd");
        $dumpvars(0, tb_pulse_gen);
    end

    initial begin
        rst_n = 0;
        sig = 0;

        #20;
        rst_n = 1;

        #12 sig = 1;
        #10 sig = 1;
        #10 sig = 0;
        #20 sig = 1;
        #10 sig = 0;
        #20 $finish;
    end

    initial begin
        $monitor("t=%0t sig=%0b pulse=%0b sig_d=%0b",
                 $time, sig, pulse, tb_pulse_gen.dut.sig_d);
    end

endmodule
```
