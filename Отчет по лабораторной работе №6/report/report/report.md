---
# Front matter
lang: ru-RU
title: " Отчёта по лабораторной работе №6"
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

Изучить задачу об эпидемии, построить графики изменения числа особей.
Рассмотреть, как будет протекать эпидемия в двух случаях.

# Задание

**Задача об эпидемии**

Вариант 7

На одном острове вспыхнула эпидемия. Известно, что из всех проживающих
на острове (N=13000) в момент начала эпидемии (t=0) число заболевших людей
(являющихся распространителями инфекции) I(0)=113, А число здоровых людей с
иммунитетом к болезни R(0)=13. Таким образом, число людей восприимчивых к
болезни, но пока здоровых, в начальный момент времени S(0)=N-I(0)- R(0).

Постройте графики изменения числа особей в каждой из трех групп.
Рассмотрите, как будет протекать эпидемия в случае:

1) если I(0)<=I*

2) если I(0)>I*



# Выполнение лабораторной работы

**Постановка задачи**

Предположим, что некая популяция, состоящая из N=13000 особей, (считаем, что популяция изолирована)
подразделяется на три группы. Первая группа - это восприимчивые к болезни, но
пока здоровые особи, обозначим их через S(t)=12874. Вторая группа – это число
инфицированных особей, которые также при этом являются распространителями
инфекции, обозначим их I(t)=113. А третья группа, обозначающаяся через R(t)=13 – это
здоровые особи с иммунитетом к болезни.
До того, как число заболевших не превышает критического значения I*, считаем, 
что все больные изолированы и не заражают здоровых. Когда I(t)>I*,
тогда инфицирование способны заражать восприимчивых к болезни особей.
Таким образом, скорость изменения числа S(t) меняется по следующему
закону:

![](image/1.png){ #fig:001 width=50% }

Поскольку каждая восприимчивая к болезни особь, которая, в конце концов,
заболевает, сама становится инфекционной, то скорость изменения числа
инфекционных особей представляет разность за единицу времени между
заразившимися и теми, кто уже болеет и лечится, т.е.:

![](image/2.png){ #fig:002 width=50% }

А скорость изменения выздоравливающих особей (при этом приобретающие
иммунитет к болезни)

![](image/3.png){ #fig:003 width=25% }

Постоянные пропорциональности $α$ и $β$, - это коэффициенты заболеваемости
и выздоровления соответственно.
Для того, чтобы решения соответствующих уравнений определялось
однозначно, необходимо задать начальные условия .Считаем, что на начало
эпидемии в момент времени t=0 нет особей с иммунитетом к болезни R(0)=0, а
число инфицированных и восприимчивых к болезни особей I(0) и S(0)
соответственно. Для анализа картины протекания эпидемии необходимо
рассмотреть два случая: I(0)<=I* и I(0)>I*.

**Построение графиков** 

Написали прогрмму на Python и получили два графика:

#Программа

import math

import numpy as np

from scipy.integrate import odeint

import matplotlib.pyplot as plt


a = 0.01 #коэффициент заболеваемости

b = 0.02 #коэффициент выздоровления

N = 13000 #общая численность популяции

I0 = 113 #количество инфицированных особей в начальный момент времени


R0 = 13 #количество здоровых особей с иммунитетом в начальный момент времени

S0 = N - I0 - R0 #количество восприимчивых к болезни особей в начальный момент времени

x0 = [S0, I0, R0] #начальные значения
 

#Время

t0 = 0

tmax = 200

dt = 0.01

t = np.arange(t0, tmax, dt)


#случай, когда I(0)<=I*

def dx1(x, t):
    dx1_1 = 0
    dx1_2 = -b*x[1]
    dx1_3 = b*x[1]
    return dx1_1, dx1_2, dx1_3


#случай, когда I(0)>I*

def dx2(x, t):
    dx2_1 = -a*x[0]
    dx2_2 = a*x[0] - b*x[1]
    dx2_3 = b*x[1]
    return dx2_1, dx2_2, dx2_3

#Решение системы

y1 = odeint(dx1, x0, t)

y2 = odeint(dx2, x0, t)



#Построение графика, когда I(0)<=I*

plt.plot(t, y1[:,0], label='S(t)')

plt.plot(t, y1[:,1], label='I(t)')

plt.plot(t, y1[:,2], label='R(t)')

plt.legend()


#Построение графика, когда I(0)>I*

plt.plot(t, y2[:,0], label='S(t)')

plt.plot(t, y2[:,1], label='I(t)')

plt.plot(t, y2[:,2], label='R(t)')

plt.legend()



**Графики**

В итоге получили график изменения числа особей, при I(0)<=I* (см.Рис. -@fig:004).

![График изменения числа особей, при I(0)<=I*](image/4.png){ #fig:004 width=70% }


А также график изменения числа особей, при I(0)>I* (см.Рис. -@fig:005).

![Графики изменения числа особей, при I(0)>I*](image/5.png){ #fig:005 width=70% }


# Выводы

После выполнения Лабораторной работы №6 мы изучили задачу об эпидемии, 
построили графики изменения числа особей.
Рассмотрели, как будет протекать эпидемия в двух случаях.

