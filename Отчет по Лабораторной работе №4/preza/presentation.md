---
## Front matter
lang: ru-RU
title: Отчет по Лабораторной работе №4
author: |
	Шапошникова Айталина НПИбд-02-18\inst{1}
institute: |
	\inst{1}RUDN University, Moscow, Russian Federation
date: 3 March, 2021 Moscow, Russian Federation

## Formatting
toc: false
slide_level: 2
theme: metropolis
header-includes: 
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
aspectratio: 43
section-titles: true
---

## Цель работы
Изучить модель гармонических колебаний, 
а также построить фазовый портрет для трех случав.

## Задание
Постройте фазовый портрет гармонического осциллятора и решение уравнения
гармонического осциллятора для следующих случаев 

1. Колебания гармонического осциллятора без затуханий и без действий внешней силы
	$\ddot{x}+7x=0$

2. Колебания гармонического осциллятора c затуханием и без действий внешней силы
	$\ddot{x}+2\dot{x}+6x=0$

3. Колебания гармонического осциллятора c затуханием и под действием внешней силы
	$\ddot{x}+5\dot{x}+x=|\cos (3t)|$
	
На интервале от 0 до 25 (шаг 0.05) с начальными условиями $x_{0} = -1$, $y_{0} = -1$

# Выполнение лабораторной работы

## Постановка задачи

Уравнение свободных колебаний гармонического осциллятора имеет следующий вид:
	$\ddot{x}+2γ\dot{x}+ω^2_{0}x=0$,

где $x$ – переменная, описывающая состояние системы (смещение грузика, заряд
конденсатора и т.д.), $γ$ – параметр, характеризующий потери энергии (трение в
механической системе, сопротивление в контуре), $ω$– собственная частота колебаний, $t$ – время.

Обозначим начальные условия: $x_{0} = -1$, $y_{0} = -1$.
Интервал на котором будет решаться задача: от 0 до 25 (шаг 0.05).
$ω$– собственная частота колебаний: 7, 6, 1.
$γ$ – параметр, характеризующий потери энергии: 0, 2, 5.


## **Построение модели**

На языке Python написали программу для численного решения задачи, используя шаблон из методических материалов.
Туда включаем:

1. Начальные условия

2. Правую часть уравнения f(t)

3. Вектор начальных условий x(t0) = x0

4. Интервал на котором будет решаться задача

5. Преображение уравнение второго порядка в уравнение первого порядка

6. Решение дифференциального уравнения

7. Построение фазового портрета


## Фазовый портрет

![Колебания гармонического осциллятора без затуханий и без действий внешней силы](image/1.png){ #fig:001 width=90% }

## Фазовый портрет
![Колебания гармонического осциллятора c затуханием и без действий внешней силы](image/2.png){ #fig:002 width=90% }

## Фазовый портрет
![Колебания гармонического осциллятора c затуханием и под действием внешней силы](image/3.png){ #fig:003 width=70% }

## Вывод

После выполнения Лабораторной работы №4 мы изучили модель гармонических колебаний, 
а также построить фазовый портрет для трех случав.


## {.standout}

Спасибо за внимание!
