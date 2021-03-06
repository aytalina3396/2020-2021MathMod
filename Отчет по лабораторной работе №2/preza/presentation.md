---
## Front matter
lang: ru-RU
title: Отчет по Лабораторной работе №2
author: |
	Шапошникова Айталина НПИбд-02-18\inst{1}
institute: |
	\inst{1}RUDN University, Moscow, Russian Federation
date: 20 February, 2021 Moscow, Russian Federation

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
Разобраться как основываются задачи о погоне и как ее решать, 
а также вывести траекторию на графике.

## Задание
Решить задачу о погоне, сделать постановку задачи, вывести дифференциальные уравнения.
Построить траекторию движения катера и лодки для двух случаев.
Определить по графику точку пересечения катера и лодки.

# Выполнение лабораторной работы
## **Задача о погоне: Постановка задачи**
Принимаем за $t_{0} = 0$, $x_{Л0} = 0$ - место нахождения лодки браконьеров в момент обнаружения,
$x_{К0} = 6,4$ км  - место нахождения катера береговой охраны относительно лодки браконьеров в момент обнаружения лодки.

Введем полярные координаты. Считаем, что полюс - это точка обнаружения
лодки браконьеров $x_{Л0} (θ = x_{Л0} = 0)$, а полярная ось $r$ проходит через точку нахождения катера береговой охраны.

![Положение катера и лодки в начальный момент времени](image/1.png){ #fig:001 width=50% }

## **Задача о погоне: Постановка задачи**
Находим расстояние $x$ (расстояние после которого катер начнет двигаться вокруг полюса).

После того, как катер береговой охраны окажется на одном расстоянии от полюса, что и лодка, 
он должен сменить прямолинейную траекторию и начать двигаться вокруг полюса удаляясь от него со скоростью лодки $v$.
Для этого скорость катера раскладываем на две составляющие:

$v_{r}$ - радиальная скорость и $v_{τ}$ - тангенциальная скорость

![Разложение скорости катера на тангенциальную и радиальную составляющие](image/2.png){ #fig:002 width=30% }

Радиальная скорость - это скорость, с которой катер удаляется от полюса, $v_{r} = \frac{\partial r}{\partial t} = v$.

Тангенциальная скорость – то линейная скорость вращения катера относительно полюса,$v_{τ} = r\frac{\partial θ}{\partial t}$.

По Теореме Пифагора вычисляем тангенциальная скорость, $v_{τ} = \sqrt{5,76v^2 - v^2} = \sqrt{4,76}v = \frac{\sqrt{119}}{5}v$.

Тогда получаем $r\frac{\partial θ}{\partial t} = \frac{\sqrt{119}}{5}v$.

## Решение системы из двух дифференциальных уравнений
$\frac{\partial r}{\partial t} = v$

$r\frac{\partial θ}{\partial t} = \frac{\sqrt{119}}{5}v$

Исключая из полученной системы производную по t, можно перейти к следующему уравнению:
$$ \frac{\partial r}{\partial θ} = \frac{5r}{\sqrt{119}} $$

Начальные условия остаются прежними.

## Написание программы для вывода графика траектории движения катера и лодки в полярных координатах
![График траектории движения катера и лодки в полярных координатах для первого случая](image/3.png){ #fig:003 width=50% }

##
![График траектории движения катера и лодки в полярных координатах для оторого случая](image/4.png){ #fig:004 width=50% }

## Вывод

После выполнения Лабораторной работы №2 мы разобрались как основываются задачи о погоне и как ее решать, 
а также вывели траекторию на графике.


## {.standout}

Спасибо за внимание!
