# Python Cheat Sheet

A quick reference for basic Python usage, plotting, data handling, and simulation/data analysis.

---

## 🧹 Basic Start

Common imports and a clean starting point for scripts.

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

---

## ⚡ Basic Script Template

Simple structure to start a new script.

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

def main():
    x = np.linspace(0, 10, 100)
    y = np.sin(x)

    plt.plot(x, y)
    plt.grid(True)
    plt.title("Signal")
    plt.xlabel("x")
    plt.ylabel("y")
    plt.show()

if __name__ == "__main__":
    main()
```

---

## 🔢 Variables and Basic Types

Create variables and use common data types.

```python
a = 10
b = 3.14
name = "test"
flag = True
```

---

## 📚 Lists

Store and manipulate sequences of values.

```python
values = [1, 2, 3, 4]

first_value = values[0]
last_value = values[-1]

values.append(5)
subset = values[1:4]
```

---

## 🧮 NumPy Arrays

Create arrays for numerical operations.

```python
import numpy as np

x = np.array([1, 2, 3, 4])
y = np.linspace(0, 10, 100)

z = np.zeros(5)
o = np.ones(5)
```

---

## ⚙️ Element-wise Operations

Operate element by element on arrays.

```python
import numpy as np

x = np.linspace(0, 10, 100)

y1 = x**2
y2 = 2 * x
y3 = np.sin(x) * np.cos(x)
y4 = x / 2
```

---

## 🔍 Indexing

Access single values or slices.

```python
import numpy as np

x = np.linspace(0, 10, 100)

first_value = x[0]
last_value = x[-1]
partial = x[0:10]
```

---

## 📏 Shape and Size

Check array dimensions.

```python
import numpy as np

A = np.array([[1, 2], [3, 4], [5, 6]])

print(A.shape)
print(A.size)
print(len(A))
```

---

## 🔁 For Loop

Repeat operations over a sequence.

```python
values = [1, 2, 3]

for v in values:
    print(v)
```

---

## ✅ If Statement

Basic conditional logic.

```python
x = 10

if x > 5:
    print("x is greater than 5")
else:
    print("x is less than or equal to 5")
```

---

## 🖨️ Print and Debug

Display values and formatted text.

```python
x = 3.14159

print(x)
print(f"Value = {x:.2f}")
```

---

## 📊 Basic Plot

Plot a simple signal.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.plot(x, y, linewidth=2)
plt.grid(True)
plt.title("Sine Wave")
plt.xlabel("x")
plt.ylabel("sin(x)")
plt.show()
```

---

## 📈 Multiple Curves

Plot multiple signals on the same figure.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 100)

plt.plot(x, np.sin(x), linewidth=1.5, label="sin(x)")
plt.plot(x, np.cos(x), linewidth=1.5, label="cos(x)")

plt.legend()
plt.grid(True)
plt.xlabel("x")
plt.ylabel("Amplitude")
plt.show()
```

---

## 🧩 Subplots

Split the figure into multiple plots.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 100)

plt.subplot(2, 1, 1)
plt.plot(x, np.sin(x))
plt.title("sin(x)")
plt.grid(True)

plt.subplot(2, 1, 2)
plt.plot(x, np.cos(x))
plt.title("cos(x)")
plt.grid(True)

plt.tight_layout()
plt.show()
```

---

## 🎨 Plot Customization

Adjust style, limits, labels, and appearance.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.plot(x, y, "r--", linewidth=2)
plt.xlim([0, 10])
plt.ylim([-1, 1])
plt.xlabel("x")
plt.ylabel("Amplitude")
plt.title("Customized Plot")
plt.grid(True)
plt.show()
```

---

## 🖼️ New Figure

Open a new figure before plotting.

```python
import matplotlib.pyplot as plt

plt.figure()
plt.plot([1, 2, 3], [1, 4, 9])
plt.grid(True)
plt.show()
```

---

## 📂 Read CSV with Pandas

Import data from a CSV file.

```python
import pandas as pd

data = pd.read_csv("data.csv")

x = data.iloc[:, 0]
y = data.iloc[:, 1]

print(data.head())
```

---

## 🔄 DataFrame to NumPy Array

Convert tabular data to array format.

```python
import pandas as pd

data = pd.read_csv("data.csv")
array_data = data.to_numpy()
```

---

## 💾 Save CSV

Export processed data to a CSV file.

```python
import pandas as pd

result = pd.DataFrame({
    "x": [1, 2, 3],
    "y": [4, 5, 6]
})

result.to_csv("output.csv", index=False)
```

---

## 📸 Save Figure

Export the current figure as an image.

```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3], [1, 4, 9])
plt.savefig("figure.png", dpi=300, bbox_inches="tight")
```

---

## ⏱️ Time Axis

Create a time vector for sampled signals.

```python
import numpy as np

fs = 1000
t = np.arange(0, 1, 1/fs)
```

---

## 🌊 Generate a Signal

Create a basic sinusoidal signal.

```python
import numpy as np
import matplotlib.pyplot as plt

fs = 1000
t = np.arange(0, 1, 1/fs)

signal = np.sin(2 * np.pi * 10 * t)

plt.plot(t, signal)
plt.grid(True)
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.show()
```

---

## 📉 FFT

Transform a signal into the frequency domain.

```python
import numpy as np
import matplotlib.pyplot as plt

fs = 1000
t = np.arange(0, 1, 1/fs)
signal = np.sin(2 * np.pi * 50 * t)

Y = np.fft.fft(signal)
N = len(Y)
f = np.arange(N) * fs / N

plt.plot(f, np.abs(Y))
plt.grid(True)
plt.xlabel("Frequency (Hz)")
plt.ylabel("|FFT|")
plt.show()
```

---

## 📊 Moving Average

Smooth a signal using a moving average.

```python
import numpy as np

signal = np.array([1, 2, 3, 4, 5, 6, 7])
window = 3

filtered = np.convolve(signal, np.ones(window)/window, mode="same")
print(filtered)
```

---

## 📈 Linear Fit

Fit data with a straight line.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.arange(1, 11)
y = 2 * x + 3

p = np.polyfit(x, y, 1)
y_fit = np.polyval(p, x)

plt.plot(x, y, "o", label="Data")
plt.plot(x, y_fit, label="Linear Fit")
plt.grid(True)
plt.legend()
plt.show()
```

---

## 🔄 Interpolation

Estimate values between known points.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.arange(1, 11)
y = np.sin(x)

xq = np.arange(1, 10.1, 0.1)
yq = np.interp(xq, x, y)

plt.plot(x, y, "o", label="Original Data")
plt.plot(xq, yq, "-", label="Interpolated")
plt.grid(True)
plt.legend()
plt.show()
```

---

# Simulation / Data Analysis

---

## 📂 Read Simulation CSV

Example for simulation or measured data exported as CSV.

```python
import pandas as pd

data = pd.read_csv("sim.csv")

time = data.iloc[:, 0].to_numpy()
vin  = data.iloc[:, 3].to_numpy()
vout = data.iloc[:, 5].to_numpy()
i    = data.iloc[:, 7].to_numpy()
```

---

## 📊 Plot Input and Output Signals

Quick visualization of imported signals.

```python
import matplotlib.pyplot as plt

plt.plot(time, vin, linewidth=1.5, label="Vin")
plt.plot(time, vout, linewidth=1.5, label="Vout")

plt.legend()
plt.xlabel("Time (s)")
plt.ylabel("Voltage (V)")
plt.title("Input and Output Signals")
plt.grid(True)
plt.show()
```

---

## ⚡ Instantaneous Power

Compute instantaneous power from voltage and current.

```python
power = vout * i

plt.plot(time, power)
plt.xlabel("Time (s)")
plt.ylabel("Power (W)")
plt.title("Instantaneous Power")
plt.grid(True)
plt.show()
```

---

## 🔋 Average Power

Compute average power over the full waveform.

```python
import numpy as np

P_avg = np.mean(power)
print(f"Average Power = {P_avg:.3e} W")
```

---

## 🔋 Energy

Integrate power over time to get energy.

```python
import numpy as np

E = np.trapz(power, time)
print(f"Energy = {E:.3e} J")
```

---

## 📉 FFT of Output Signal

Inspect spectral content of the output.

```python
import numpy as np
import matplotlib.pyplot as plt

Y = np.fft.fft(vout)
N = len(Y)
dt = time[1] - time[0]
fs = 1 / dt
f = np.arange(N) * fs / N

plt.plot(f, np.abs(Y))
plt.xlim([0, fs/2])
plt.xlabel("Frequency (Hz)")
plt.ylabel("|FFT(Vout)|")
plt.title("Output Spectrum")
plt.grid(True)
plt.show()
```

---

## 🧪 RMS Value

Compute RMS of a signal.

```python
import numpy as np

rms_val = np.sqrt(np.mean(vout**2))
print(f"RMS = {rms_val:.3e}")
```

---

## 📍 Peak Detection

Detect peaks in the waveform.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import find_peaks

peaks, _ = find_peaks(vout)

plt.plot(time, vout)
plt.plot(time[peaks], vout[peaks], "o")
plt.xlabel("Time (s)")
plt.ylabel("Voltage (V)")
plt.title("Peak Detection")
plt.grid(True)
plt.show()
```

---

## 📈 Gain Estimation

Estimate gain using peak values.

```python
gain = np.max(vout) / np.max(vin)
print(f"Gain = {gain:.3f}")
```

---

## 🧼 Signal Smoothing

Reduce noise for easier visualization.

```python
import numpy as np
import matplotlib.pyplot as plt

window = 10
vout_smooth = np.convolve(vout, np.ones(window)/window, mode="same")

plt.plot(time, vout, label="Original")
plt.plot(time, vout_smooth, linewidth=1.5, label="Smoothed")
plt.legend()
plt.grid(True)
plt.show()
```

---

## ⏳ Propagation Delay

Estimate delay using a threshold crossing.

```python
import numpy as np

threshold = 0.5

idx_in = np.where(vin > threshold)[0][0]
idx_out = np.where(vout > threshold)[0][0]

t_in = time[idx_in]
t_out = time[idx_out]

delay = t_out - t_in
print(f"Delay = {delay:.3e} s")
```

---

## ⬆️ Rise Time

Estimate rise time between 10% and 90%.

```python
import numpy as np

v_low = 0.1 * np.max(vout)
v_high = 0.9 * np.max(vout)

t10 = time[np.where(vout >= v_low)[0][0]]
t90 = time[np.where(vout >= v_high)[0][0]]

rise_time = t90 - t10
print(f"Rise Time = {rise_time:.3e} s")
```

---

## ⬇️ Fall Time

Estimate fall time between 90% and 10%.

```python
import numpy as np

v_low = 0.1 * np.max(vout)
v_high = 0.9 * np.max(vout)

t90 = time[np.where(vout <= v_high)[0][0]]
t10 = time[np.where(vout <= v_low)[0][0]]

fall_time = t10 - t90
print(f"Fall Time = {fall_time:.3e} s")
```

---

## 🔄 Average Current

Estimate mean current.

```python
import numpy as np

I_avg = np.mean(i)
print(f"Average Current = {I_avg:.3e} A")
```

---

## 📁 Export Processed Results

Save processed data into a new CSV file.

```python
import pandas as pd

result = pd.DataFrame({
    "time": time,
    "vin": vin,
    "vout": vout,
    "power": power
})

result.to_csv("processed.csv", index=False)
```

---

## 📋 Report-Style Plot

Cleaner plot for reports and presentations.

```python
import matplotlib.pyplot as plt

plt.figure()
plt.plot(time, vout, linewidth=2)

plt.xlabel("Time (s)")
plt.ylabel("Voltage (V)")
plt.title("Output Signal")
plt.grid(True)
plt.show()
```

---

## 🧠 Full Analysis Template

Basic full-flow script for simulation analysis.

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

data = pd.read_csv("sim.csv")

time = data.iloc[:, 0].to_numpy()
vin  = data.iloc[:, 3].to_numpy()
vout = data.iloc[:, 5].to_numpy()
i    = data.iloc[:, 7].to_numpy()

plt.figure()
plt.plot(time, vin, linewidth=1.5, label="Vin")
plt.plot(time, vout, linewidth=1.5, label="Vout")
plt.legend()
plt.xlabel("Time (s)")
plt.ylabel("Voltage (V)")
plt.title("Signals")
plt.grid(True)

power = vout * i
P_avg = np.mean(power)
E = np.trapz(power, time)

threshold = 0.5
idx_in = np.where(vin > threshold)[0][0]
idx_out = np.where(vout > threshold)[0][0]
delay = time[idx_out] - time[idx_in]

v_low = 0.1 * np.max(vout)
v_high = 0.9 * np.max(vout)
t10 = time[np.where(vout >= v_low)[0][0]]
t90 = time[np.where(vout >= v_high)[0][0]]
rise_time = t90 - t10

gain = np.max(vout) / np.max(vin)

print(f"Average Power = {P_avg:.3e} W")
print(f"Energy        = {E:.3e} J")
print(f"Delay         = {delay:.3e} s")
print(f"Rise Time     = {rise_time:.3e} s")
print(f"Gain          = {gain:.3f}")

plt.show()
```
