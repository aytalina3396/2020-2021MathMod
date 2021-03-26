---
# Front matter
lang: ru-RU
title: " Отчёта по лабораторной работе №7"
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
  - \usepackage{amsmath}
---

# Цель работы

Изучить эффективность рекламы, построить графики распространения рекламы.

# Задание

Вариант 7

Постройте график распространения рекламы, математическая модель которой описывается
следующим уравнением:

1. $$\frac{\partial n}{\partial t} = (0.81+0.0003n(t))(N-n(t))$$

2. $$\frac{\partial n}{\partial t} = (0.00008+0.8n(t))(N-n(t))$$

3. $$\frac{\partial n}{\partial t} = (0.8|\sin (8t)|+0.8|\cos (t)|n(t))(N-n(t))$$

При этом объем аудитории N = 888, в начальный момент о товаре знает 18 человек. Для
случая 2 определите в какой момент времени скорость распространения рекламы будет
иметь максимальное значение.


# Выполнение лабораторной работы

**Постановка задачи**

Модель рекламной кампании описывается следующими величинами.
Считаем, что $$\frac{\partial n}{\partial t}$$ - скорость изменения со временем числа потребителей,
узнавших о товаре и готовых его купить, t - время, прошедшее с начала рекламной
кампании, n(t) - число уже информированных клиентов. Эта величина
пропорциональна числу покупателей, еще не знающих о нем, это описывается
следующим образом: $α1(t)(N-n(t))$, где N - общее число потенциальных
платежеспособных покупателей, $α1(t)>0$ - характеризует интенсивность
рекламной кампании (зависит от затрат на рекламу в данный момент времени).
Помимо этого, узнавшие о товаре потребители также распространяют полученную
информацию среди потенциальных покупателей, не знающих о нем (в этом случае
работает т.н. сарафанное радио). Этот вклад в рекламу описывается величиной
$α2(t)n(t)(N-n(t))$, эта величина увеличивается с увеличением потребителей
узнавших о товаре. Математическая модель распространения рекламы описывается
уравнением:

$$\frac{\partial n}{\partial t} = (α1(t)+α2(t)n(t))(N-n(t))$$


Обозначим начальные условия:

N = 888 - общее число потенциальных платежеспособных покупателей;
x0 = 18 - количество людей, знающих о товаре в начальный момент времени;
t0 = 0 - начальный момент времени.

И приступим к написанию программы.

**Построение графиков** 

Написали прогрмму на Python и получили три графика:

#Программа

import math

import numpy as np

from scipy.integrate import odeint

import matplotlib.pyplot as plt


x0 = 18 #количество людей, знающих о товаре в начальный момент времени

N = 888 #максимальное количество людей, которых может заинтересовать товар


#время

t0 = 0

tmax = 30

dt = 0.1

t = np.arange(t0, tmax, dt)


#функция, отвечающая за платную рекламу

def k1(t):
    g = 0.81
    return g


def k2(t):
    g = 0.00008
    return g


def k3(t):
    g = 0.8*np.sin(8*t)
    return g


#функция, описывающая сарафанное радио

def p1(t):
    v = 0.0003
    return v


def p2(t):
    v = 0.8
    return v


def p3(t):
    v = 0.8*np.cos(t)
    return v


#уравнение, описывающее распространение рекламы

def f1(x, t):
    xd = (k1(t) + p1(t)*x)*(N - x)
    return xd


def f2(x, t):
    xd = (k2(t) + p2(t)*x)*(N - x)
    return xd


def f3(x, t):
    xd = (k3(t) + p3(t)*x)*(N - x)
    return xd

#решение ОДУ

x1 = odeint(f1, x0, t)

x2 = odeint(f2, x0, t)

x3 = odeint(f3, x0, t)


#Построение графика решения

plt.plot(t, x1)

plt.plot(t, x2)

#момент времени, где скорость распространения рекламы будет иметь максимальное значение

t[np.argmax(x2[1:].transpose()/t[1:])+1]

plt.plot(t, x3)

**Графики**

В итоге получили график распространения рекламы для первого случая (см.Рис. -@fig:001).

![График распространения рекламы](image/1.png){ #fig:001 width=70% }


В итоге получили график распространения рекламы для второго случая (см.Рис. -@fig:002).

![График распространения рекламы](image/2.png){ #fig:002 width=70% }


В итоге получили график распространения рекламы для третьего случая (см.Рис. -@fig:003).

![График распространения рекламы](image/3.png){ #fig:003 width=70% }


# Выводы

После выполнения Лабораторной работы №7 мы изучили эффективность рекламы, 
построили графики распространения рекламы. А также вывели момент времени, 
где скорость распространения рекламы будет иметь максимальное значение - 0.1.

