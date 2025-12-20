---
# Preamble

## Author
author:
  name: Мантуров Татархан Бесланович
  degrees: DSc
  orcid: 0000-0002-0877-7063
  email: kulyabov-ds@rudn.ru
  affiliation:
    - name: Российский университет дружбы народов
      country: Российская Федерация
      postal-code: 117198
      city: Москва
      address: ул. Миклухо-Маклая, д. 6
## Title
title: "Отчёт по лабораторной работе №1"
subtitle: "Дисциплина: Сетевые технологии"
license: "CC BY"
## Generic options
lang: ru-RU
number-sections: true
toc: true
toc-title: "Содержание"
toc-depth: 2
## Crossref customization
crossref:
  lof-title: "Список иллюстраций"
  lot-title: "Список таблиц"
  lol-title: "Листинги"
## Bibliography
bibliography:
  - bib/cite.bib
csl: _resources/csl/gost-r-7-0-5-2008-numeric.csl
## Formats
format:
### Pdf output format
  pdf:
    toc: true
    number-sections: true
    colorlinks: false
    toc-depth: 2
    lof: true # List of figures
    lot: true # List of tables
#### Document
    documentclass: scrreprt
    papersize: a4
    fontsize: 12pt
    linestretch: 1.5
#### Language
    babel-lang: russian
    babel-otherlangs: english
#### Biblatex
    cite-method: biblatex
    biblio-style: gost-numeric
    biblatexoptions:
      - backend=biber
      - langhook=extras
      - autolang=other*
#### Misc options
    csquotes: true
    indent: true
    header-includes: |
      \usepackage{indentfirst}
      \usepackage{float}
      \floatplacement{figure}{H}
      \usepackage[math,RM={Scale=0.94},SS={Scale=0.94},SScon={Scale=0.94},TT={Scale=MatchLowercase,FakeStretch=0.9},DefaultFeatures={Ligatures=Common}]{plex-otf}
### Docx output format
  docx:
    toc: true
    number-sections: true
    toc-depth: 2
---

# Цель работы

Целью данной работы является изучение методов кодирования и модуляции сигналов с помощью высокоуровнего языка программирования Octave. Определение спектра и параметров сигнала. Демонстрация принципов модуляции сигнала на примере аналоговой амплитудной модуляции. Исследование свойства самосинхронизации сигнала.

# Задание

1. Построить график функции $$ y=sin(x)+\frac{1}{3}sin(3x)+\frac{1}{5}sin(5x) $$ на интервале
[−10; 10], используя Octave и функцию plot. График экспортировать в файлы формата .eps, .png.
2. Добавить график функции $$ y=cos(x)+\frac{1}{3}cos(3x)+\frac{1}{5}cos(5x) $$ на интервале
-10; 10. График экспортировать в файлы формата .eps, .png.
3. Разработать код m-файла, результатом выполнения которого являются графики меандра, реализованные с различным количеством гармоник.
4. Определить спектр двух отдельных сигналов и их суммы
5. Выполнить задание с другой частотой дискретизации. Пояснить, что будет, если взять частоту дискретизации меньше 80 Гц?
6. Продемонстрировать принципы модуляции сигнала на примере аналоговой амплитудной модуляции
7. По заданных битовых последовательностей требуется получить кодированные сигналы для нескольких кодов, проверить свойства самосинхронизуемости кодов, получить спектры.

# Выполнение лабораторной работы

## Построение графиков в Octave

Сначала установили в нашей ОС Octave: ```sudo apt install octave``` ([рис. @fig-001]), ([рис. @fig-002])

Далее запустили в нашей ОС Octave с оконным интерфейсом ([рис. @fig-003])

Далее перешли в окно редактора. Воспользовавшись комбинацией клавиш ```ctrl + n``` создали новый сценарий. Сохранили его в наш рабочий каталог с именем *plot_sin.m*. В окне редактора написали код по построению графика функции $$ y=sin(x)+\frac{1}{3}sin(3x)+\frac{1}{5}sin(5x) $$ на интервале [−10; 10]: 

```
% Формирование массива x:
x=-10:0.1:10;
% Формирование массива y.
y1=sin(x)+1/3*sin(3*x)+1/5*sin(5*x);
% Построение графика функции:
plot(x,y1, "-ok; y1=sin(x)+(1/3)*sin(3*x)+(1/5)*sin(5*x);","markersize",4)
% Отображение сетки на графике
grid on;
% Подпись оси X:
xlabel('x');
% Подпись оси Y:
ylabel('y');
% Название графика:
title('y1=sin x+ (1/3)sin(3x)+(1/5)sin(5x)');
% Экспорт рисунка в файл .eps:
print ("plot-sin.eps", "-mono", "-FArial:16", "-deps")
% Экспорт рисунка в файл .png:
print("plot-sin.png");
```

После этого запустили наш сценарий, воспользовавшись клавишей ```f5```. Открылось окно с построенным графиком и в нашем рабочем каталоге появились файлы с графиками в в форматах .eps, .png ([рис. @fig-004]), ([рис. @fig-005])

![Работа программы plot_sin.m](image/4.png){#fig-004 width=70%}

![График функции y](image/5.png){#fig-005 width=70%}

Далее сохранили сценарий под другим названием *plot_sic_cos.m* и изменили код так чтобы на одном графике располагались отличающиеся по типу линий графики функций $$ y1=sin(x)+\frac{1}{3}sin(3x)+\frac{1}{5}sin(5x) $$ и $$ y2=cos(x)+\frac{1}{3}cos(3x)+\frac{1}{5}cos(5x) $$ на интервале [−10; 10]:

```
% Формирование массива x:
x=-10:0.1:10;
% Формирование массива y.
y1=sin(x)+1/3*sin(3*x)+1/5*sin(5*x);
y2=cos(x)+1/3*cos(3*x)+1/5*cos(5*x);
% Построение графика функции:
plot(x,y1, "-ok; y1=sin(x)+(1/3)*sin(3*x)+(1/5)*sin(5*x);","markersize",4, x,y2,
"-k; y2=cos(x)+(1/3)*cos(3*x)+(1/5)*cos(5*x);","markersize",4)
% Отображение сетки на графике
grid on;
% Подпись оси X:
xlabel('x');
% Подпись оси Y:
ylabel('y');
% Название графика:
title('y1=sin x+ (1/3)sin(3x)+(1/5)sin(5x); y2=cos x+ (1/3)cos(3x)+(1/5)cos(5x)');
% Экспорт рисунка в файл .eps:
print ("plo_sin_cos.eps", "-mono", "-FArial:16", "-deps")
% Экспорт рисунка в файл .png:
print("plot_sin_cos.png");
```

И запустили сценарий ([рис. @fig-006]), ([рис. @fig-007])

![Работа программы plot_sin_cos.m](image/6.png){#fig-006 width=70%}

![График функций y1 и y2](image/7.png){#fig-007 width=70%}

## Разложение импульсного сигнала в частичный ряд Фурье

Далее создали новый сценарий и сохранили его в наш рабочий каталог с именем *meandr.m*. В нём реализовали код для реализации меандра через косинусы:

```
% meandr.m
% количество отсчетов (гармоник):
N=8;
% частота дискретизации:
t=-1:0.01:1;
% значение амплитуды:
A=1;
% период:
T=1;
% амплитуда гармоник
nh=(1:N)*2-1;
% массив коэффициентов для ряда, заданного через cos:
Am=2/pi ./ nh;
Am(2:2:end) = -Am(2:2:end);
% массив гармоник:
harmonics=cos(2 * pi * nh' * t/T);
% массив элементов ряда:
s1=harmonics.*repmat(Am',1,length(t));
% Суммирование ряда:
s2=cumsum(s1);
% Построение графиков:
for k=1:N
subplot(4,2,k)
plot(t, s2(k,:))
end
```

Запустили сценарий и получили график меандра через косинусы ([рис. @fig-008]), ([рис. @fig-009])

![Работа программы meandr.m (1)](image/8.png){#fig-008 width=70%}

![Графики меандра, содержащего различное число гармоник (через косинусы)](image/9.png){#fig-009 width=70%}

Далее скорректировали код для реализации меандра через синусы:

```
% meandr.m
% количество отсчетов (гармоник):
N=8;
% частота дискретизации:
t=-1:0.01:1;
% значение амплитуды:
A=1;
% период:
T=1;
% амплитуда гармоник
nh=(1:N)*2-1;
% массив коэффициентов для ряда, заданного через sin:
Am=2/pi ./ nh;
% Am(2:2:end) = -Am(2:2:end);
% массив гармоник:
harmonics=cos(2 * pi * nh' * t/T);
% массив элементов ряда:
s1=harmonics.*repmat(Am',1,length(t));
% Суммирование ряда:
s2=cumsum(s1);
% Построение графиков:
for k=1:N
  subplot(4,2,k)
  plot(t, s2(k,:))
end
% Экспорт рисунка в файл .png:
print("meandr2.png");
```

Запустили сценарий и получили график меандра через синусы ([рис. @fig-010]), ([рис. @fig-011])

![Работа программы meandr.m (2)](image/10.png){#fig-010 width=70%}

![Графики меандра, содержащего различное число гармоник (через синусы)](image/11.png){#fig-011 width=70%}

## Определение спектра и параметров сигнала

В нашем рабочем каталоге создали каталог *spectre1* и в нём новый сценарий с именем, *spectre.m*. Далее написали код для построения графика двух синусоидальных сигнала разной частоты:

```
% spectre1/spectre.m
% Создание каталогов signal и spectre для размещения графиков:
mkdir 'signal';
mkdir 'spectre';
% Длина сигнала (с):
tmax = 0.5;
% Частота дискретизации (Гц) (количество отсчётов):
fd = 512;
% Частота первого сигнала (Гц):
f1 = 10;
% Частота второго сигнала (Гц):
f2 = 40;
% Амплитуда первого сигнала:
a1 = 1;
% Амплитуда второго сигнала:
a2 = 0.7;
% Массив отсчётов времени:
t = 0:1./fd:tmax;
% Спектр сигнала:
fd2 = fd/2;
% Два сигнала разной частоты:
signal1 = a1*sin(2*pi*t*f1);
signal2 = a2*sin(2*pi*t*f2);
% График 1-го сигнала:
plot(signal1,'b');
% График 2-го сигнала:
hold on
plot(signal2,'r');
hold off
title('Signal')
% Экспорт графика в файл в каталоге signal:
print 'signal/spectre.png'
```

Зпустили сценарий и получили график сигналов ([рис. @fig-012]), ([рис. @fig-013])

![Работа программы spectre.m (1)](image/12.png){#fig-012 width=70%}

![Два синусоидальных сигнала разной частоты](image/13.png){#fig-013 width=70%}

Далее с помощью быстрого преобразования Фурье нашли спектры сигналов. Для этого добавили в файл *spectre.m* следующий код: 

```
% Посчитаем спектр
% Амплитуды преобразования Фурье сигнала 1:
spectre1 = abs(fft(signal1,fd));
% Амплитуды преобразования Фурье сигнала 2:
spectre2 = abs(fft(signal2,fd));
% Построение графиков спектров сигналов:
plot(spectre1,'b');
hold on
plot(spectre2,'r');
hold off
title('Spectre');
print 'spectre/spectre.png';
```

Запустили сценарий и получили график спектров ([рис. @fig-014]), ([рис. @fig-015])

![Работа программы spectre.m (2)](image/14.png){#fig-014 width=70%}
 
![График спектров синусоидальных сигналов](image/15.png){#fig-015 width=70%}

Учитывая реализацию преобразования Фурье, скорректировали график спектра: отбросили дублирующие отрицательные частоты, а также приняли в расчёт то, что на каждом шаге вычисления быстрого преобразования Фурье происходит суммирование амплитуд сигналов. Для этого добавили в файл *spectre.m* следующий код:  

```
% Исправление графика спектра
% Сетка частот:
f = 1000*(0:fd2)./(2*fd);
% Нормировка спектров по амплитуде:
spectre1 = 2*spectre1/fd2;
spectre2 = 2*spectre2/fd2;
% Построение графиков спектров сигналов:
plot(f,spectre1(1:fd2+1),'b');
hold on
plot(f,spectre2(1:fd2+1),'r');
hold off
xlim([0 100]);
title('Fixed spectre');
xlabel('Frequency (Hz)');
print 'spectre/spectre_fix.png';
```

Запустили сценарий и получили исправленный графк спекторов ([рис. @fig-016]), ([рис. @fig-017])

![Работа программы spectre.m (2)](image/16.png){#fig-016 width=70%}

![Исправленный график спектров синусоидальных сигналов](image/17.png){#fig-017 width=70%}

Далее нашли спектр суммы расмотренных сигналов, создав каталог *spectr_sum* и файл в нём *spectre_sum.m* со следующим кодом:

```
% spectr_sum/spectre_sum.m
% Создание каталогов signal и spectre для размещения графиков:
mkdir 'signal';
mkdir 'spectre';
% Длина сигнала (с):
tmax = 0.5;
% Частота дискретизации (Гц) (количество отсчётов):
fd = 512;
% Частота первого сигнала (Гц):
f1 = 10;
% Частота второго сигнала (Гц):
f2 = 40;
% Амплитуда первого сигнала:
a1 = 1;
% Амплитуда второго сигнала:
a2 = 0.7;
% Спектр сигнала
fd2 = fd/2;
% Сумма двух сигналов (синусоиды) разной частоты:
% Массив отсчётов времени:
t = 0:1./fd:tmax;
signal1 = a1*sin(2*pi*t*f1);
signal2 = a2*sin(2*pi*t*f2);
signal = signal1 + signal2;
plot(signal);
title('Signal');
print 'signal/spectre_sum.png';
% Подсчет спектра:
% Амплитуды преобразования Фурье сигнала:
spectre = fft(signal,fd);
% Сетка частот
f = 1000*(0:fd2)./(2*fd);
% Нормировка спектра по амплитуде:
spectre = 2*sqrt(spectre.*conj(spectre))./fd2;
% Построение графика спектра сигнала:
plot(f,spectre(1:fd2+1))
xlim([0 100]);
title('Spectre');
xlabel('Frequency (Hz)');
print 'spectre/spectre_sum.png';
```

Запустили сценарий и получили нужные графики ([рис. @fig-018]), ([рис. @fig-019]), ([рис.@fig-020]), ([рис. @fig-021])

![Работа программы spectre_sum.m (1)](image/18.png){#fig-018 width=70%}

![Суммарный сигнал](image/19.png){#fig-019 width=70%}

## Амплитудная модуляция

В нашем рабочем каталоге создали каталог *modulation* и в нём новый сценарий с именем *am.m*. В нём прописали следующий код: 

```
% modulation/am.m
% Создание каталогов signal и spectre для размещения графиков:
mkdir 'signal';
mkdir 'spectre';
% Модуляция синусоид с частотами 50 и 5
% Длина сигнала (с)
tmax = 0.5;
% Частота дискретизации (Гц) (количество отсчётов)
fd = 512;
% Частота сигнала (Гц)
f1 = 5;
% Частота несущей (Гц)
f2 = 50;
% Спектр сигнала
fd2 = fd/2;
% Построение графиков двух сигналов (синусоиды)
% разной частоты
% Массив отсчётов времени:
t = 0:1./fd:tmax;
signal1 = sin(2*pi*t*f1);
signal2 = sin(2*pi*t*f2);
signal = signal1 .* signal2;
plot(signal, 'b');
hold on
% Построение огибающей:
plot(signal1, 'r');
plot(-signal1, 'r');
hold off
title('Signal');
print 'signal/am.png';
% Расчет спектра:
% Амплитуды преобразования Фурье-сигнала:
spectre = fft(signal,fd);
% Сетка частот:
f = 1000*(0:fd2)./(2*fd);
% Нормировка спектра по амплитуде:
spectre = 2*sqrt(spectre.*conj(spectre))./fd2;
% Построение спектра:
plot(f,spectre(1:fd2+1), 'b')
xlim([0 100]);
title('Spectre');
xlabel('Frequency (Hz)');
print 'spectre/am.png';
```

Запустили и получили нужные нам графики ([рис. @fig-022]), ([рис. @fig-023]), ([рис. @fig-024]), ([рис. @fig-025])

![Работа программы am.m (1)](image/20.png){#fig-022 width=70%}

![Сигнал и огибающая при амплитудной модуляции](image/21.png){#fig-023 width=70%}

## Кодирование сигнала. Исследование свойства самосинхронизации сигнала

В окне интерпретатора команд проверили, установлен ли у нас пакет расширений signal: ```>> pkg list``` ([рис. @fig-026])

![Пакет расширений signal](image/26.png){#fig-026 width=70%}

В нашем рабочем каталоге создали каталог *coding* и в нём файлы *main.m*, *maptowave.m*, *unipolar.m*, *ami.m*, *bipolarnrz.m*, *bipolarrz.m*, *manchester.m*, *diffmanc.m*, *calcspectre.m* ([рис. @fig-027])

![Структура каталога](image/27.png){#fig-027 width=70%}

В файле *main.m* подключили пакет signal, задали входные кодовые последовательности, прописали вызовы функций для построения графиков модуляций кодированных сигналов для кодовой последовательности data, прописали вызовы функций для построения графиков модуляций кодированных сигналов для кодовой последовательности data_sync и прописали вызовы функций для построения графиков спектров:

```
% coding/main.m
% Подключение пакета signal:
pkg load signal;
% Входная кодовая последовательность:
data=[0 1 0 0 1 1 0 0 0 1 1 0];
% Входная кодовая последовательность для проверки свойства самосинхронизации:
data_sync=[0 0 0 0 0 0 0 1 1 1 1 1 1 1];
% Входная кодовая последовательность для построения спектра сигнала:
data_spectre=[0 1 0 1 0 1 0 1 0 1 0 1 0 1];
% Создание каталогов signal, sync и spectre для размещения графиков:
mkdir 'signal';
mkdir 'sync';
mkdir 'spectre';
axis("auto");

% Униполярное кодирование
wave=unipolar(data);
plot(wave);
ylim([-1 6]);
title('Unipolar');
print 'signal/unipolar.png';

% Кодирование ami
wave=ami(data);
plot(wave)
title('AMI');
print 'signal/ami.png';
% Кодирование NRZ
wave=bipolarnrz(data);
plot(wave);
title('Bipolar Non-Return to Zero');
print 'signal/bipolarnrz.png';
% Кодирование RZ
wave=bipolarrz(data);
plot(wave)
title('Bipolar Return to Zero');
print 'signal/bipolarrz.png';
% Манчестерское кодирование
wave=manchester(data);
plot(wave)
title('Manchester');
print 'signal/manchester.png';
% Дифференциальное манчестерское кодирование
wave=diffmanc(data);
plot(wave)
title('Differential Manchester');
print 'signal/diffmanc.png';

% Униполярное кодирование
wave=unipolar(data_sync);
plot(wave);
ylim([-1 6]);
title('Unipolar');
print 'sync/unipolar.png';
% Кодирование AMI
wave=ami(data_sync);
plot(wave)
title('AMI');
print 'sync/ami.png';
% Кодирование NRZ
wave=bipolarnrz(data_sync);
plot(wave);
title('Bipolar Non-Return to Zero');
print 'sync/bipolarnrz.png';
% Кодирование RZ
wave=bipolarrz(data_sync);
plot(wave)
title('Bipolar Return to Zero');
print 'sync/bipolarrz.png';
% Манчестерское кодирование
wave=manchester(data_sync);
plot(wave)
title('Manchester');
print 'sync/manchester.png';
% Дифференциальное манчестерское кодирование
wave=diffmanc(data_sync);
plot(wave)
title('Differential Manchester');
print 'sync/diffmanc.png';

% Униполярное кодирование:
wave=unipolar(data_spectre);
spectre=calcspectre(wave);
title('Unipolar');
print 'spectre/unipolar.png';
% Кодирование AMI:
wave=ami(data_spectre);
spectre=calcspectre(wave);
title('AMI');
print 'spectre/ami.png';
% Кодирование NRZ:
wave=bipolarnrz(data_spectre);
spectre=calcspectre(wave);
title('Bipolar Non-Return to Zero');
print 'spectre/bipolarnrz.png';
% Кодирование RZ:
wave=bipolarrz(data_spectre);
spectre=calcspectre(wave);
title('Bipolar Return to Zero');
print 'spectre/bipolarrz.png';
% Манчестерское кодирование:
wave=manchester(data_spectre);
spectre=calcspectre(wave);
title('Manchester');
print 'spectre/manchester.png';
% Дифференциальное манчестерское кодирование:
wave=diffmanc(data_spectre);
spectre=calcspectre(wave);
title('Differential Manchester');
print 'spectre/diffmanc.png';% coding/main.m
% Подключение пакета signal:
pkg load signal;
% Входная кодовая последовательность:
data=[0 1 0 0 1 1 0 0 0 1 1 0];
% Входная кодовая последовательность для проверки свойства самосинхронизации:
data_sync=[0 0 0 0 0 0 0 1 1 1 1 1 1 1];
% Входная кодовая последовательность для построения спектра сигнала:
data_spectre=[0 1 0 1 0 1 0 1 0 1 0 1 0 1];
% Создание каталогов signal, sync и spectre для размещения графиков:
mkdir 'signal';
mkdir 'sync';
mkdir 'spectre';
axis("auto");

% Униполярное кодирование
wave=unipolar(data);
plot(wave);
ylim([-1 6]);
title('Unipolar');
print 'signal/unipolar.png';

% Кодирование ami
wave=ami(data);
plot(wave)
title('AMI');
print 'signal/ami.png';
% Кодирование NRZ
wave=bipolarnrz(data);
plot(wave);
title('Bipolar Non-Return to Zero');
print 'signal/bipolarnrz.png';
% Кодирование RZ
wave=bipolarrz(data);
plot(wave)
title('Bipolar Return to Zero');
print 'signal/bipolarrz.png';
% Манчестерское кодирование
wave=manchester(data);
plot(wave)
title('Manchester');
print 'signal/manchester.png';
% Дифференциальное манчестерское кодирование
wave=diffmanc(data);
plot(wave)
title('Differential Manchester');
print 'signal/diffmanc.png';

% Униполярное кодирование
wave=unipolar(data_sync);
plot(wave);
ylim([-1 6]);
title('Unipolar');
print 'sync/unipolar.png';
% Кодирование AMI
wave=ami(data_sync);
plot(wave)
title('AMI');
print 'sync/ami.png';
% Кодирование NRZ
wave=bipolarnrz(data_sync);
plot(wave);
title('Bipolar Non-Return to Zero');
print 'sync/bipolarnrz.png';
% Кодирование RZ
wave=bipolarrz(data_sync);
plot(wave)
title('Bipolar Return to Zero');
print 'sync/bipolarrz.png';
% Манчестерское кодирование
wave=manchester(data_sync);
plot(wave)
title('Manchester');
print 'sync/manchester.png';
% Дифференциальное манчестерское кодирование
wave=diffmanc(data_sync);
plot(wave)
title('Differential Manchester');
print 'sync/diffmanc.png';

% Униполярное кодирование:
wave=unipolar(data_spectre);
spectre=calcspectre(wave);
title('Unipolar');
print 'spectre/unipolar.png';
% Кодирование AMI:
wave=ami(data_spectre);
spectre=calcspectre(wave);
title('AMI');
print 'spectre/ami.png';
% Кодирование NRZ:
wave=bipolarnrz(data_spectre);
spectre=calcspectre(wave);
title('Bipolar Non-Return to Zero');
print 'spectre/bipolarnrz.png';
% Кодирование RZ:
wave=bipolarrz(data_spectre);
spectre=calcspectre(wave);
title('Bipolar Return to Zero');
print 'spectre/bipolarrz.png';
% Манчестерское кодирование:
wave=manchester(data_spectre);
spectre=calcspectre(wave);
title('Manchester');
print 'spectre/manchester.png';
% Дифференциальное манчестерское кодирование:
wave=diffmanc(data_spectre);
spectre=calcspectre(wave);
title('Differential Manchester');
print 'spectre/diffmanc.png';
```

([рис. @fig-028])

![Файл main.m](image/28.png){#fig-028 width=70%}

Далее в файле *maptowave.m* прописали функцию, которая по входному битовому потоку строит график сигнала:

```
% coding/maptowave.m
function wave=maptowave(data)
	data=upsample(data,100);
	wave=filter(5*ones(1,100),1,data);
```

([рис. @fig-029])

![Файл maptowave.m](image/29.png){#fig-029 width=70%}

В файлах *unipolar.m*, *ami.m*, *bipolarnrz.m*, *bipolarrz.m*, *manchester.m*, *diffmanc.m* прописали соответствующие функции преобразования кодовой:

Униполярное кодирование:

```
% coding/unipolar.m
% Униполярное кодирование:
function wave=unipolar(data)
	wave=maptowave(data);

```

([рис. @fig-030])

![Файл unipolar.m, Униполярное кодирование](image/30.png){#fig-030 width=70%}

Кодирование AMI:

```
% coding/ami.m
% Кодирование AMI:
function wave=ami(data)
	am=mod(1:length(data(data==1)),2);
	am(am==0)=-1;
	data(data==1)=am;
	wave=maptowave(data);
```

([рис. @fig-031])

![Файл ami.m, Кодирование AMI](image/31.png){#fig-031 width=70%}

Кодирование NRZ:

```
% coding/bipolarnrz.m
% Кодирование NRZ:
function wave=bipolarnrz(data)
	data(data==0)=-1;
	wave=maptowave(data);
```



Кодирование RZ:

```
% coding/bipolarrz.m
% Кодирование RZ:
function wave=bipolarrz(data)
	data(data==0)=-1;
	data=upsample(data,2);
	wave=maptowave(data);
```

([рис. @fig-033])

![Файл bipolarrz.m, Кодирование RZ](image/33.png){#fig-033 width=70%}

Манчестерское кодирование:

```
% coding/manchester.m
% Манчестерское кодирование:
function wave=manchester(data)
	data(data==0)=-1;
	data=upsample(data,2);
	data=filter([-1 1],1,data);
	wave=maptowave(data);
```

([рис. @fig-034])

![Файл manchester.m, Манчестерское кодирование](image/34.png){#fig-034 width=70%}

Дифференциальное манчестерское кодирование:

```
% coding/diffmanc.m
% Дифференциальное манчестерское кодирование
function wave=diffmanc(data)
	data=filter(1,[1 1],data);
	data=mod(data,2);
	wave=manchester(data);
```

([рис. @fig-035])

![Файл diffmanc.m, Дифференциальное манчестерское кодировани](image/35.png){#fig-035 width=70%}

В файле calcspectre.m прописали функцию построения спектра сигнала:

```
% calcspectre.m
% Функция построения спектра сигнала:
function spectre = calcspectre(wave)
	% Частота дискретизации (Гц):
	Fd = 512;
	Fd2 = Fd/2;
	Fd3 = Fd/2 + 1;
	X = fft(wave,Fd);
	spectre = X.*conj(X)/Fd;
	f = 1000*(0:Fd2)/Fd;
	plot(f,spectre(1:Fd3));
	xlabel('Frequency (Hz)');

```

([рис. @fig-036])

![Файл calcspectre.m](image/36.png){#fig-036 width=70%}

Запустили главный скрипт main.m. В каталоге *signal* бфли получены файлы с графиками кодированного сигнала (рис. 3.40-3.45), в каталоге *sync* — файлы с графиками, иллюстрирующими свойства самосинхронизации (рис. 3.46–3.51), в каталоге *spectre* — файлы с графиками спектров сигналов (рис. 3.52–3.57) ([рис. @fig-037]), ([рис. @fig-038]), ([рис. @fig-039])

Полученные графики ([рис. @fig-040]), ([рис. @fig-041]), ([рис. @fig-042]), ([рис. @fig-043]), ([рис. @fig-044]), ([рис. @fig-045]), ([рис. @fig-046]), ([рис. @fig-047]), ([рис. @fig-048]), ([рис. @fig-049]), ([рис. @fig-050]), ([рис. @fig-051]), ([рис. @fig-052]), ([рис. @fig-053]), ([рис. @fig-054]), ([рис. @fig-055]), ([рис. @fig-056]), ([рис. @fig-057])

![Униполярное кодирование](image/40.png){#fig-040 width=70%}

![Кодирование AMI](image/41.png){#fig-041 width=70%}

![Кодирование NRZ](image/42.png){#fig-042 width=70%}

![Кодирование RZ](image/43.png){#fig-043 width=70%}

![Манчестерское кодирование](image/44.png){#fig-044 width=70%}

![Дифференциальное манчестерское кодирование](image/45.png){#fig-045 width=70%}

![Униполярное кодирование: нет самосинхронизации](image/46.png){#fig-046 width=70%}

![Кодирование AMI: самосинхронизация при наличии сигнала](image/47.png){#fig-047 width=70%}

![Кодирование NRZ: нет самосинхронизации](image/48.png){#fig-048 width=70%}

![Кодирование RZ: есть самосинхронизация](image/49.png){#fig-049 width=70%}

![Манчестерское кодирование: есть самосинхронизация](image/50.png){#fig-050 width=70%}

![Дифференциальное манчестерское кодирование: есть самосинхронизация](image/51.png){#fig-051 width=70%}

![Униполярное кодирование: спектр сигнала](image/52.png){#fig-052 width=70%}

![Кодирование AMI: спектр сигнала](image/53.png){#fig-053 width=70%}

![Кодирование NRZ: спектр сигнала](image/54.png){#fig-054 width=70%}

![Кодирование RZ: спектр сигнала](image/55.png){#fig-055 width=70%}

![Манчестерское кодирование: спектр сигнала](image/56.png){#fig-056 width=70%}

![Дифференциальное манчестерское кодирование: спектр сигнала](image/57.png){#fig-057 width=70%}

# Выводы

В хое выполнения лабораторной работы №1 мы изучили методы кодирования и модуляции сигналов с помощью высокоуровнего языка программирования Octave. Определили спектр и параметры сигнала. Продемонстрировали принципы модуляции сигнала на примере аналоговой амплитудной модуляции. Исследовали свойства самосинхронизации сигнала.

# Список литературы

1. [Лаборатораня работа №1](https://esystem.rudn.ru/pluginfile.php/2858347/mod_resource/content/3/001-lab_cod-mod-2.pdf)
