---
# Front matter
lang: ru-RU
title: " Отчёта по лабораторной работе №5"
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

Изучить модель хищник-жертва, построить график зависимости $x$ от $y$ 
и графики функций x(t), y(t). 

# Задание

**Модель хищник-жертва**

Вариант 7

Для модели «хищник-жертва»:

\begin{equation*}
 \begin{cases}
   \frac{\partial x}{\partial t} = -0.18x(t)+0.04x(t)y(t), 
   \\
   \frac{\partial y}{\partial t}= 0.38y(t)-0.035x(t)y(t).
 \end{cases}
\end{equation*}

Постройте график зависимости численности хищников от численности жертв,
а также графики изменения численности хищников и численности жертв при
следующих начальных условиях: $x_{0} = 12$, $y_{0} = 17$.Найдите стационарное
состояние системы.


# Выполнение лабораторной работы

**Постановка задачи**

Предположим в лесу у нас $x_{0} = 12$ хищников и $y_{0} = 17$ жертв.
Пока число жертв достаточно велико, для прокормки всех хищников,
численность хищников растет до тех пор, пока не наступит момент, что корма
перестанет хватать на всех. Тогда хищники начнут умирать, и их численность будет
уменьшаться. В этом случае в какой-то момент времени численность жертв снова
начнет увеличиваться, что повлечет за собой новый рост популяции хищников. Такой
цикл будет повторяться, пока обе популяции будут существовать. Помимо этого,
на численность хищников влияют болезни и старение.
Обозначим коэффициенты: a = 0.18, d = 0.035 - коэффициенты смертности, 
b = 0.047, c = 0.38 - коэффициенты прироста популяции


**Построение модели** 

Написали прогрмму на Python и получили графики:

#Программа

import math

import numpy as np

from scipy.integrate import odeint

import matplotlib.pyplot as plt


a = 0.18  #коэффициент естественной смертности хищников

b = 0.047  #коэффициент естественного прироста жертв

c = 0.38  #коэффициент увеличения числа хищников

d = 0.035  #коэффициент смертности жертв


def dx(x, t):
    dx_1 = -a*x[0] + b*x[0]*x[1]
    dx_2 = c*x[1] - d*x[0]*x[1]
    return dx_1, dx_2

t0 = 0


x0 = [12, 17] #начальное значение x и у (популяция хищников и популяция жертв)


t = np.arange(0, 100, 0.1)


y = odeint(dx, x0, t)


y1 = y[:,0]

y2 = y[:,1]


#построение графика колебаний изменения числа популяции хищников

plt.plot(t, y1)

#построение графика колебаний изменения числа популяции жертв

plt.plot(t, y2)

plt.grid(axis = 'both')


#построение графика зависимости изменения численности хищников от изменения численности жертв

plt.plot(y1, y2)

plt.plot(x0[0], x0[1], 'ro')

plt.grid(axis = 'both')


**Графики**

В итоге получили график колебаний изменения числа популяции хищников и жертв (см.Рис. -@fig:001).

![График колебаний изменения числа популяции хищников и жертв](image/1.png){ #fig:001 width=70% }


А также график зависимости численности хищников от численности жертв с начальными значениями у=17, х=12 (см.Рис. -@fig:002).

![Графики зависимости численности хищников от численности жертв](image/2.png){ #fig:002 width=70% }


# Выводы

После выполнения Лабораторной работы №5 мы изучили модель хищник-жертва, 
построили график зависимости $x$ от $y$ и графики функций x(t), y(t). .

