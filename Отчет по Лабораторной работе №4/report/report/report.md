---
# Front matter
lang: ru-RU
title: " Отчёта по лабораторной работе №4"
subtitle: "дисциплина: Математическое моделирование"
author: "Шапошникова Айталина Степановна НПИбд-02-18"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучить модель гармонических колебаний, 
а также построить фазовый портрет для трех случав. 

# Задание

**Модель гармонических колебаний**

Вариант 7

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

**Постановка задачи**

Уравнение свободных колебаний гармонического осциллятора имеет следующий вид:
	$\ddot{x}+2γ\dot{x}+ω^2_{0}x = 0$,

где $x$ – переменная, описывающая состояние системы (смещение грузика, заряд
конденсатора и т.д.), $γ$ – параметр, характеризующий потери энергии (трение в
механической системе, сопротивление в контуре), $ω$– собственная частота колебаний, $t$ – время.

Обозначим начальные условия: $x_{0} = -1$, $y_{0} = -1$.
Интервал на котором будет решаться задача: от 0 до 25 (шаг 0.05).
$ω$– собственная частота колебаний: 7, 6, 1.
$γ$ – параметр, характеризующий потери энергии: 0, 2, 5.

Уравнение второго порядка можно представить в виде системы двух уравнений первого порядка (при $γ = 0$):
$\dot{x} = y$,
$\dot{y} = ω^2_{0}x$.

Независимые переменные x, y определяют пространство, в котором
«движется» решение. Это фазовое пространство системы, поскольку оно двумерно
будем называть его фазовой плоскостью.

Значение фазовых координат x, y в любой момент времени полностью
определяет состояние системы. Решению уравнения движения как функции
времени отвечает гладкая кривая в фазовой плоскости. Она называется фазовой
траекторией. Если множество различных решений (соответствующих различным 
начальным условиям) изобразить на одной фазовой плоскости, возникает общая
картина поведения системы. Такую картину, образованную набором фазовых
траекторий, называют фазовым портретом.

**Построение модели** 

Написали прогрмму на Python и получили три графика:

#1. Колебания гармонического осциллятора без затуханий и без действий внешней силы

import math

import numpy as np

from scipy.integrate import odeint

import matplotlib.pyplot as plt


#w - частота

w_1 = 7.0

w_2 = 6.0

w_3 = 1.0

#g - затухание

g_1 = 0.0

g_2 = 2.0

g_3 = 5.0

#Правая часть уравнения fun(t)

def F(t):
    f = 0
    return f

def FF(t):
    f = np.cos(3*t)
    return f

#Вектор начальных условий x(t0) = x0

x0 = np.array([-1.0, -1.0])


#Интервал на котором будет решаться задача

t = np.arange(0, 25, 0.05)


#Преображаем уравнение второго порядка в уравнение первого порядка

def y_1(x, t):
    dx_1_1 = x[1]
    dx_1_2 = -w_1*x[0] - g_1*x[1] - F(t)
    return dx_1_1, dx_1_2


def y_2(x, t):
    dx_2_1 = x[1]
    dx_2_2 = -w_2*x[0] - g_2*x[1] - F(t)
    return dx_2_1, dx_2_2


def y_3(x, t):
    dx_3_1 = x[1]
    dx_3_2 = -w_3*x[0] - g_3*x[1] - FF(t)
    return dx_3_1, dx_3_2

#Решаем дифференциальные уравнения с начальным условием x(t0) = x0 на интервале t с правой частью, 

#заданной y и записываем решение в матрицу x

X_1 = odeint(y_1, x0, t)

X_2 = odeint(y_2, x0, t)

X_3 = odeint(y_3, x0, t)


#Переписываем отдельно x в y_1, x' в y_2

y_1_1 = X_1[:, 0]

y_1_2 = X_1[:, 1]


y_2_1 = X_2[:, 0]

y_2_2 = X_2[:, 1]


y_3_1 = X_3[:, 0]

y_3_2 = X_3[:, 1]


plt.plot(y_1_1, y_1_2)

**Фазовый портрет**

В итоге получили график для первого случая (см.Рис. -@fig:001).

![Колебания гармонического осциллятора без затуханий и без действий внешней силы](image/1.png){ #fig:001 width=70% }


В итоге получили график для второго случая (см.Рис. -@fig:002).

![Колебания гармонического осциллятора c затуханием и без действий внешней силы](image/2.png){ #fig:002 width=70% }


В итоге получили график для третьего случая (см.Рис. -@fig:003).

![Колебания гармонического осциллятора c затуханием и под действием внешней силы](image/3.png){ #fig:003 width=70% }




# Выводы

После выполнения Лабораторной работы №4 мы изучили модель гармонических колебаний, 
а также построить фазовый портрет для трех случав.


# Ответы на вопросы к лабораторной работе

1. Запишите простейшую модель гармонических колебаний*

Простейшим видом колебательного процесса являются простые гармонические колебания, которые описываются уравнением $x = x_m cos (\omega t + \varphi _0)$. 

2. Дайте определение осциллятора*

Осциллятор — система, совершающая колебания, то есть показатели которой периодически повторяются во времени.

3. Запишите модель математического маятника*

Уравнение динамики принимает вид: 
$$\frac{\partial ^2 \alpha}{\partial t^2} + \frac{g}{L} sin{\alpha} = 0$$ 
В случае малых колебаний полагают $\sin(\alpha ) ≈ \alpha$. В результате возникает линейное дифференциальное уравнение 
$$\frac{\partial ^2 \alpha}{\partial t^2} + \frac{g}{L} \alpha = 0$$ или $$\frac{\partial ^2 \alpha}{\partial t^2} + \omega ^2 \alpha = 0$$

4. Запишите алгоритм перехода от дифференциального уравнения второго порядка к двум дифференциальным уравнениям первого порядка*

Пусть у нас есть дифференциальное уравнение 2-го порядка:
$\ddot{x}+2γ\dot{x}+ω^2_{0}x = 0$

Для перехода к системе уравнений первого порядка сделаем замену (это метод Ранге-Кутты):
$$ y = \dot{x} $$

Тогда получим систему уравнений:
$\dot{x} = y$,
$\dot{y} = ω^2_{0}x$. 

5. Что такое фазовый портрет и фазовая траектория?*

Фазовый портрет — это то, как величины, описывающие состояние системы (= динамические переменные), зависят друг от друга.

Фазовая траектория — кривая в фазовом пространстве, составленная из точек, представляющих состояние динамической системы в последовательные моменты времени 
в течение всего времени эволюции.