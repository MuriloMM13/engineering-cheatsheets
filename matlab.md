# MATLAB Cheat Sheet — Advanced (Engineering)

---

## 📂 Read CSV (Simulation Data)

Importar dados típicos de simulação (ex: ngspice export).

```matlab id="csv1"
data = readtable('sim.csv');

time = data{:,1};
vin  = data{:,4};
vout = data{:,6};
i    = data{:,8};
```

---

## 📊 Plot Multiple Signals (Clean Style)

Plot organizado para análise.

```matlab id="plot_clean"
plot(time, vin, 'LineWidth', 1.5); hold on;
plot(time, vout, 'LineWidth', 1.5);

legend('Vin', 'Vout');
xlabel('Time (s)');
ylabel('Voltage (V)');
grid on;
```

---

## ⚡ Instantaneous Power

Calcular potência instantânea.

```matlab id="power_inst"
power = vout .* i;
plot(time, power);
title('Instantaneous Power');
```

---

## 🔋 Average Power

Calcular potência média ao longo do tempo.

```matlab id="power_avg"
P_avg = mean(power);
```

---

## 🔋 Energy Calculation

Energia consumida (integração no tempo).

```matlab id="energy"
E = trapz(time, power);
```

---

## 📈 Detect Rising Edge Delay

Encontrar delay entre entrada e saída.

```matlab id="delay"
threshold = 0.5;

t_in  = time(find(vin > threshold, 1));
t_out = time(find(vout > threshold, 1));

delay = t_out - t_in;
```

---

## 📉 Frequency Response (FFT Clean)

Análise espectral mais útil.

```matlab id="fft_clean"
Y = fft(vout);
N = length(Y);

f = (0:N-1)*(1/(time(2)-time(1)))/N;

plot(f, abs(Y));
xlim([0 max(f)/2]);
```

---

## 🧪 Noise / Signal RMS

Calcular valor RMS do sinal.

```matlab id="rms"
rms_val = rms(vout);
```

---

## 📊 Peak Detection

Encontrar picos em sinais.

```matlab id="peaks"
[pks, locs] = findpeaks(vout, time);

plot(time, vout); hold on;
plot(locs, pks, 'o');
```

---

## 📉 Gain Calculation

Ganho entre entrada e saída.

```matlab id="gain"
gain = max(vout) / max(vin);
```

---

## 📊 Smoothing (Better Filter)

Filtro simples para reduzir ruído.

```matlab id="smooth"
vout_smooth = smoothdata(vout, 'movmean', 10);
```

---

## 📁 Export Data (CSV)

Salvar resultados processados.

```matlab id="export_csv"
result = table(time, vin, vout, power);
writetable(result, 'processed.csv');
```

---

## 📸 Publication-Style Plot

Plot mais bonito para relatório.

```matlab id="pub_plot"
figure;
plot(time, vout, 'LineWidth', 2);

xlabel('Time (s)');
ylabel('Voltage (V)');
title('Output Signal');

grid on;
set(gca, 'FontSize', 12);
```

---

## ⚡ Automatic Metrics Script (Template)

Template para análise completa.

```matlab id="template_adv"
clear; clc; close all;

%% Load Data
data = readtable('sim.csv');

time = data{:,1};
vin  = data{:,4};
vout = data{:,6};
i    = data{:,8};

%% Power
power = vout .* i;
P_avg = mean(power);
E = trapz(time, power);

%% Delay
threshold = 0.5;
t_in  = time(find(vin > threshold, 1));
t_out = time(find(vout > threshold, 1));
delay = t_out - t_in;

%% Plot
plot(time, vin); hold on;
plot(time, vout);
legend('Vin', 'Vout');
grid on;

%% Display
fprintf('Average Power: %.3e W\n', P_avg);
fprintf('Energy: %.3e J\n', E);
fprintf('Delay: %.3e s\n', delay);
```
