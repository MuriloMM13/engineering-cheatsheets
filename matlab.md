# MATLAB Cheat Sheet

A quick reference for basic MATLAB usage, plotting, data handling, and SPICE/simulation analysis.

---

## 🧹 Clean Workspace

Clear variables, command window, and open figures.

```matlab
clear;
clc;
close all;
```

---

## ⚡ Basic Script Template

Simple structure to start a new script.

```matlab
%% Initialization
clear; clc; close all;

%% Parameters
x = 0:0.1:10;
y = sin(x);

%% Plot
plot(x, y);
grid on;
title('Signal');
xlabel('x');
ylabel('y');
```

---

## 🔢 Create Vectors and Matrices

Useful commands for building vectors and matrices.

```matlab
x1 = 0:0.1:10;
x2 = linspace(0, 10, 100);

z = zeros(1, 10);
o = ones(1, 10);

A = [1 2; 3 4];
B = A';
```

---

## 🔍 Indexing

Access specific elements or ranges.

```matlab
x = 0:0.1:10;

first_value = x(1);
last_value = x(end);
partial = x(1:10);
```

---

## ⚙️ Element-wise Operations

Use these when operating point by point on vectors.

```matlab
x = 0:0.1:10;

y1 = x.^2;
y2 = 2 .* x;
y3 = sin(x) .* cos(x);
y4 = x ./ 2;
```

---

## 📏 Size and Length

Check dimensions of arrays and signals.

```matlab
A = [1 2; 3 4; 5 6];

size(A)
length(A)
numel(A)
```

---

## 📊 Basic Plot

Plot a simple signal.

```matlab
x = 0:0.1:10;
y = sin(x);

plot(x, y, 'LineWidth', 2);
grid on;
title('Sine Wave');
xlabel('x');
ylabel('sin(x)');
```

---

## 📈 Multiple Curves

Plot multiple signals on the same figure.

```matlab
x = 0:0.1:10;

plot(x, sin(x), 'LineWidth', 1.5);
hold on;
plot(x, cos(x), 'LineWidth', 1.5);

legend('sin(x)', 'cos(x)');
grid on;
xlabel('x');
ylabel('Amplitude');
```

---

## 🧩 Subplots

Split the figure into multiple plots.

```matlab
x = 0:0.1:10;

subplot(2,1,1);
plot(x, sin(x));
title('sin(x)');
grid on;

subplot(2,1,2);
plot(x, cos(x));
title('cos(x)');
grid on;
```

---

## 🎨 Plot Customization

Adjust style, limits, labels, and appearance.

```matlab
x = 0:0.1:10;
y = sin(x);

plot(x, y, 'r--', 'LineWidth', 2);
xlim([0 10]);
ylim([-1 1]);
xlabel('x');
ylabel('Amplitude');
title('Customized Plot');
grid on;
```

---

## 🖼️ New Figure

Open a new figure window before plotting.

```matlab
figure;
plot(x, y);
grid on;
```

---

## 📂 Read CSV as Table

Useful for generic data import.

```matlab
data = readtable('data.csv');

x = data{:,1};
y = data{:,2};

plot(x, y);
grid on;
```

---

## 🔄 Convert Table to Array

Convert imported table data to numeric array.

```matlab
data = readtable('data.csv');
array_data = table2array(data);
```

---

## 💾 Save Variables

Save variables into a MAT file.

```matlab
save('data.mat', 'x', 'y');
```

---

## 📸 Save Figure

Export the current figure as an image.

```matlab
exportgraphics(gcf, 'figure.png', 'Resolution', 300);
```

---

## 🧪 Display and Debug

Print values and inspect variables.

```matlab
disp(x);
fprintf('First value = %.2f\n', x(1));

size(x)
length(x)
```

---

## ⏱️ Time Axis

Create a time vector for sampled signals.

```matlab
fs = 1000;
t = 0:1/fs:1;
```

---

## 🌊 Generate a Signal

Create a basic sinusoidal signal.

```matlab
fs = 1000;
t = 0:1/fs:1;

signal = sin(2*pi*10*t);
plot(t, signal);
grid on;
xlabel('Time (s)');
ylabel('Amplitude');
```

---

## 📉 FFT

Transform a signal into the frequency domain.

```matlab
fs = 1000;
t = 0:1/fs:1;
signal = sin(2*pi*50*t);

Y = fft(signal);
N = length(Y);
f = (0:N-1)*fs/N;

plot(f, abs(Y));
grid on;
xlabel('Frequency (Hz)');
ylabel('|FFT|');
```

---

## 📊 Moving Average

Smooth a signal using a moving average.

```matlab
window = 5;
filtered = movmean(signal, window);
```

---

## 📈 Linear Fit

Fit data with a straight line.

```matlab
x = 1:10;
y = 2*x + 3;

p = polyfit(x, y, 1);
y_fit = polyval(p, x);

plot(x, y, 'o');
hold on;
plot(x, y_fit, 'LineWidth', 1.5);
grid on;
legend('Data', 'Linear Fit');
```

---

## 🔄 Interpolation

Estimate values between known points.

```matlab
x = 1:10;
y = sin(x);

xq = 1:0.1:10;
yq = interp1(x, y, xq);

plot(x, y, 'o');
hold on;
plot(xq, yq, '-');
grid on;
legend('Original Data', 'Interpolated');
```

---

# SPICE / Simulation Analysis

---

## 📂 Read Simulation CSV

Example for simulation data exported from SPICE tools.

```matlab
data = readtable('sim.csv');

time = data{:,1};
vin  = data{:,4};
vout = data{:,6};
i    = data{:,8};
```

---

## 📊 Plot Input and Output Signals

Quick visualization of simulation signals.

```matlab
plot(time, vin, 'LineWidth', 1.5);
hold on;
plot(time, vout, 'LineWidth', 1.5);

legend('Vin', 'Vout');
xlabel('Time (s)');
ylabel('Voltage (V)');
title('Input and Output Signals');
grid on;
```

---

## ⚡ Instantaneous Power

Compute instantaneous power from voltage and current.

```matlab
power = vout .* i;

plot(time, power);
xlabel('Time (s)');
ylabel('Power (W)');
title('Instantaneous Power');
grid on;
```

---

## 🔋 Average Power

Compute average power over the full waveform.

```matlab
P_avg = mean(power);
fprintf('Average Power = %.3e W\n', P_avg);
```

---

## 🔋 Energy

Integrate power over time to get energy.

```matlab
E = trapz(time, power);
fprintf('Energy = %.3e J\n', E);
```

---

## 📉 FFT of Output Signal

Inspect spectral content of the output.

```matlab
Y = fft(vout);
N = length(Y);
dt = time(2) - time(1);
fs = 1/dt;
f = (0:N-1)*fs/N;

plot(f, abs(Y));
xlim([0 fs/2]);
xlabel('Frequency (Hz)');
ylabel('|FFT(Vout)|');
title('Output Spectrum');
grid on;
```

---

## 🧪 RMS Value

Compute RMS of a signal.

```matlab
rms_val = rms(vout);
fprintf('RMS = %.3e\n', rms_val);
```

---

## 📍 Peak Detection

Detect peaks in the waveform.

```matlab
[pks, locs] = findpeaks(vout, time);

plot(time, vout);
hold on;
plot(locs, pks, 'o');
xlabel('Time (s)');
ylabel('Voltage (V)');
title('Peak Detection');
grid on;
```

---

## 📈 Gain Estimation

Estimate gain using peak values.

```matlab
gain = max(vout) / max(vin);
fprintf('Gain = %.3f\n', gain);
```

---

## 🧼 Signal Smoothing

Reduce noise for easier visualization.

```matlab
vout_smooth = smoothdata(vout, 'movmean', 10);

plot(time, vout, 'DisplayName', 'Original');
hold on;
plot(time, vout_smooth, 'LineWidth', 1.5, 'DisplayName', 'Smoothed');
legend;
grid on;
```

---

## ⏳ Propagation Delay

Estimate delay using a threshold crossing.

```matlab
threshold = 0.5;

idx_in  = find(vin  > threshold, 1);
idx_out = find(vout > threshold, 1);

t_in  = time(idx_in);
t_out = time(idx_out);

delay = t_out - t_in;
fprintf('Delay = %.3e s\n', delay);
```

---

## ⬆️ Rise Time

Estimate rise time between 10% and 90%.

```matlab
v_low  = 0.1 * max(vout);
v_high = 0.9 * max(vout);

t10 = time(find(vout >= v_low, 1));
t90 = time(find(vout >= v_high, 1));

rise_time = t90 - t10;
fprintf('Rise Time = %.3e s\n', rise_time);
```

---

## ⬇️ Fall Time

Estimate fall time between 90% and 10%.

```matlab
v_low  = 0.1 * max(vout);
v_high = 0.9 * max(vout);

t90 = time(find(vout <= v_high, 1));
t10 = time(find(vout <= v_low, 1));

fall_time = t10 - t90;
fprintf('Fall Time = %.3e s\n', fall_time);
```

---

## 🔄 Static Current Estimate

Estimate mean current.

```matlab
I_avg = mean(i);
fprintf('Average Current = %.3e A\n', I_avg);
```

---

## 📁 Export Processed Results

Save processed data into a new CSV.

```matlab
result = table(time, vin, vout, power);
writetable(result, 'processed.csv');
```

---

## 📋 Report-Style Plot

Cleaner plot for reports and presentations.

```matlab
figure;
plot(time, vout, 'LineWidth', 2);

xlabel('Time (s)');
ylabel('Voltage (V)');
title('Output Signal');
grid on;
set(gca, 'FontSize', 12);
```

---

## 🧠 Full Analysis Template

Basic full-flow script for simulation analysis.

```matlab
%% Initialization
clear; clc; close all;

%% Load Data
data = readtable('sim.csv');

time = data{:,1};
vin  = data{:,4};
vout = data{:,6};
i    = data{:,8};

%% Plot Signals
figure;
plot(time, vin, 'LineWidth', 1.5);
hold on;
plot(time, vout, 'LineWidth', 1.5);
legend('Vin', 'Vout');
xlabel('Time (s)');
ylabel('Voltage (V)');
title('Signals');
grid on;

%% Power
power = vout .* i;
P_avg = mean(power);
E = trapz(time, power);

%% Delay
threshold = 0.5;
idx_in  = find(vin  > threshold, 1);
idx_out = find(vout > threshold, 1);
delay = time(idx_out) - time(idx_in);

%% Rise Time
v_low  = 0.1 * max(vout);
v_high = 0.9 * max(vout);
t10 = time(find(vout >= v_low, 1));
t90 = time(find(vout >= v_high, 1));
rise_time = t90 - t10;

%% Gain
gain = max(vout) / max(vin);

%% Results
fprintf('Average Power = %.3e W\n', P_avg);
fprintf('Energy        = %.3e J\n', E);
fprintf('Delay         = %.3e s\n', delay);
fprintf('Rise Time     = %.3e s\n', rise_time);
fprintf('Gain          = %.3f\n', gain);
```
