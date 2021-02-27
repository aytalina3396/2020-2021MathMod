---
# Front matter
lang: ru-RU
title: " Отчёта по лабораторной работе №3"
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

Изучить модель боевых действий в различный случаях ведения боя, 
а также вывести графики изменения численности армии.

# Задание

**Модель боевых действий**

Вариант 7

Между страной Х и страной У идет война. Численность состава войск
исчисляется от начала войны, и являются временными функциями
$x(t)$ и $y(t)$. В начальный момент времени страна Х имеет армию численностью 24 000 человек, 
а в распоряжении страны У армия численностью в 9 500 человек. 
Для упрощения модели считаем, что коэффициенты $a, b, c, h$ постоянны. 
Также считаем $P(t)$ и $Q(t)$ непрерывные функции.

Постройте графики изменения численности войск армии Х и армии У для
следующих случаев:

1. Модель боевых действий между регулярными войсками

	 $$\frac{\partial x}{\partial t} = -0,3x(t)-0,87y(t)+|\sin (2t)|+1$$
	 $$\frac{\partial y}{\partial t} = -0,5x(t)-0,41y(t)+|\cos (3t)|+1$$

2. Модель ведение боевых действий с участием регулярных войск и партизанских отрядов 

	$$\frac{\partial x}{\partial t} = -0,25x(t)-0,64y(t)+|\sin (2t+4)|$$
	$$\frac{\partial y}{\partial t} = -0,2x(t)y(t)-0,52y(t)+|\cos (t+4)|$$


# Выполнение лабораторной работы

**Постановка задачи**

1. Модель боевых действий между регулярными войсками. 

Зададим коэффициент смертности, не связанный с боевыми действиями у первой
армии 0,3, у второй 0,41. Коэффициенты эффективности первой и второй армии 0,5
и 0,87 соответственно. Функция, описывающая подход подкрепление первой армии,
$P(t) = |\sin (2t)|$, подкрепление второй армии описывается функцией $Q(t) = |\cos (3t)|$. 
Зададим начальные условия: $x_{0} = 24000$, $y_{0} = 9500$.

2. Модель ведение боевых действий с участием регулярных войск и партизанских отрядов.

Зададим коэффициент смертности, не связанный с боевыми действиями у первой
армии 0,25, у второй 0,52. Коэффициенты эффективности первой и второй армии 0,2
и 0,64 соответственно. Функция, описывающая подход подкрепление первой армии,
$P(t) = |\sin (2t+4)|$, подкрепление второй армии описывается функцией $Q(t) = |\cos (t+4)|$. 
Зададим начальные условия: $x_{0} = 24000$, $y_{0} = 9500$.

**Построение модели боевых действий** 

Написали прогрмму на Python и получили два графика:

#1. Модель боевых действий между регулярными войсками

import math

import numpy as np

from scipy.integrate import odeint

import matplotlib.pyplot as plt


#Начальные условия

x0 = 24000 #численность первой армии

y0 = 9500 #численность второй армии


a = 0.3 #константа, характеризующая степень влияния различных факторов на потери

b = 0.87 #эффективность боевых действий армии у

c = 0.5 #эффективность боевых действий армии х

h = 0.41 #константа, характеризующая степень влияния различных факторов на потери


#Время

t0 = 0 #начальный моент времени

tmax = 1 #предельный момент времени

dt = 0.05 #шаг изменения времени

t = np.arange(t0, tmax, dt)


#возможность подхода подкрепления к армии х

def P(t):
    p = np.sin(2*t)
    return p

#возможность подхода подкрепления к армии у

def Q(t):
    q = np.cos(3*t)
    return q

#Система дифференциальных уравнений

def syst(f, t):
    dy_1 = -a*f[0] - b*f[1] + P(t) + 1
    dy_2 = -c*f[0] - h*f[1] + Q(t) + 1
    return dy_1, dy_2


#Вектор начальных условий

v = np.array([x0, y0])


#Решение системы

f = odeint(syst, v, t)


#Построение графиков решений

plt.plot(t, f)

plt.ylabel('Численность армии')

plt.xlabel('Время')

plt.legend(['Армия X','Армия Y'])



В итоге получили график изменения численности армии X и Y в процессе боевых действий для первого случая (см.Рис. -@fig:001).

![График изменения численности армии X и Y в процессе боевых действий для первого случая](image/1.png){ #fig:001 width=100% }


#2. Модель ведение боевых действий с участием регулярных войск и партизанских отрядов

import math

import numpy as np

from scipy.integrate import odeint

import matplotlib.pyplot as plt


#Начальные условия

x0 = 24000 #численность первой армии

y0 = 9500 #численность второй армии


a = 0.25 #константа, характеризующая степень влияния различных факторов на потери

b = 0.64 #эффективность боевых действий армии у

c = 0.2 #эффективность боевых действий армии х

h = 0.52 #константа, характеризующая степень влияния различных факторов на потери


#Время

t0 = 0 #начальный моент времени

tmax = 1 #предельный момент времени

dt = 0.05 #шаг изменения времени

t = np.arange(t0, tmax, dt)


#возможность подхода подкрепления к армии х

def P(t):
    p = np.fabs(np.sin(2*t+4))
    return p

#возможность подхода подкрепления к армии у

def Q(t):
    q = np.fabs(np.cos(t+4))
    return q


#Система дифференциальных уравнений

def syst(f, t):
    dy_1 = -a*f[0] - b*f[1] + P(t)
    dy_2 = -c*f[0]*f[1] - h*f[1] + Q(t)
    return dy_1, dy_2


#Вектор начальных условий

v = np.array([x0, y0])


#Решение системы

f = odeint(syst, v, t)


#Построение графиков решений

plt.plot(t, f)

plt.ylabel('Численность армии')

plt.xlabel('Время')

plt.legend(['Армия X','Армия Y'])



В итоге получили график изменения численности армии X и Y в процессе боевых действий для второго случая (см.Рис. -@fig:002).

![График изменения численности армии X и Y в процессе боевых действий для второго случая](image/2.png){ #fig:002 width=100% }



# Выводы

После выполнения Лабораторной работы №3 мы изучили модель боевых действий в различный случаях ведения боя, 
а также вывели графики изменения численности армии.

