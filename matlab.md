# MATLAB Cheat Sheet

---

## 📊 Basic Plot

Plot simples de um sinal.

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

## 📈 Multiple Plots

Plotar várias curvas no mesmo gráfico.

```matlab
x = 0:0.1:10;

plot(x, sin(x)); 
hold on;
plot(x, cos(x));

legend('sin', 'cos');
grid on;
```

---

## 🧩 Subplots

Dividir a figura em múltiplos gráficos.

```matlab
x = 0:0.1:10;

subplot(2,1,1);
plot(x, sin(x));
title('sin');

subplot(2,1,2);
plot(x, cos(x));
title('cos');
```

---

## 🎨 Plot Customization

Alterar estilo e limites do gráfico.

```matlab
plot(x, sin(x), 'r--', 'LineWidth', 2);
xlim([0 10]);
ylim([-1 1]);
grid on;
```

---

## 📂 Read CSV / Data

Importar dados de um arquivo CSV.

```matlab
data = readtable('data.csv');

x = data.Var1;
y = data.Var2;

plot(x, y);
```

---

## 🔄 Table to Array

Converter tabela para array numérico.

```matlab
data = readtable('data.csv');
array = table2array(data);
```

---

## 🔢 Vectors & Matrices

Criar e manipular vetores e matrizes.

```matlab
x = linspace(0, 10, 100);
z = zeros(1, 10);
o = ones(1, 10);

A = [1 2; 3 4];
B = A';
```

---

## ⚙️ Element-wise Operations

Operações elemento a elemento (muito importante).

```matlab
x = 0:0.1:10;

y1 = x.^2;
y2 = sin(x) .* cos(x);
```

---

## 📉 FFT (Frequency Domain)

Converter sinal para domínio da frequência.

```matlab
fs = 1000;
t = 0:1/fs:1;
signal = sin(2*pi*50*t);

Y = fft(signal);
f = (0:length(Y)-1)*fs/length(Y);

plot(f, abs(Y));
```

---

## 📊 Moving Average Filter

Suavizar um sinal com média móvel.

```matlab
window = 5;
filtered = movmean(signal, window);
```

---

## ⏱️ Time Signal

Criar eixo de tempo e sinal.

```matlab
fs = 1000;
t = 0:1/fs:1;

signal = sin(2*pi*10*t);
```

---

## 📈 Linear Fit

Ajuste linear de dados (regressão).

```matlab
x = 1:10;
y = 2*x + 3;

p = polyfit(x, y, 1);
y_fit = polyval(p, x);

plot(x, y, 'o');
hold on;
plot(x, y_fit);
```

---

## 🔄 Interpolation

Interpolar pontos entre dados existentes.

```matlab
x = 1:10;
y = sin(x);

xq = 1:0.1:10;
yq = interp1(x, y, xq);

plot(x, y, 'o', xq, yq, '-');
```

---

## 💾 Save Figure

Salvar gráfico como imagem.

```matlab
exportgraphics(gcf, 'figure.png', 'Resolution', 300);
```

---

## 📁 Save Data

Salvar variáveis em arquivo.

```matlab
save('data.mat', 'x', 'y');
```

---

## 🧪 Debug

Exibir valores e verificar dimensões.

```matlab
disp(x);
fprintf('Value: %.2f\n', x(1));

size(x)
length(x)
```

---

## 🧹 Clean Workspace

Limpar ambiente de trabalho.

```matlab
clear;
clc;
close all;
```

---

## ⚡ Script Template

Template básico para começar scripts.

```matlab
%% Initialization
clear; clc; close all;

%% Parameters
fs = 1000;
t = 0:1/fs:1;

%% Signal
signal = sin(2*pi*10*t);

%% Plot
plot(t, signal);
grid on;
title('Signal');
```
