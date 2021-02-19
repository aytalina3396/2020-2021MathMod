---
# Front matter
lang: ru-RU
title: " Отчёта по лабораторной работе №1"
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

Ознакомиться с GitHub, ее интерфейском и как с ней работать. 
Также познакомиться с основными возможностями разметки Markdown.

# Задание

Создать аккаунт на GitHub, создать репозиторий, релиз. п
Подготовиться к работе с git, попробовать основные команды.
Создать ssh-ключ и подключиться к git с ее помощью.


# Выполнение лабораторной работы

1. Создали аккаунт на GitHub, подтвердили наш мейл. (см.Рис. -@fig:001)

![Регистрация на GitHub](image/1.png){ #fig:001 width=70% }

2. Создали репозиторий "2020-2021MathMod" на GitHub. (см.Рис. -@fig:002)

![Репозитоия](image/2.png){ #fig:002 width=70% }

3. Подготовили к работе с git. Установили имя и электронную почту. 
Также параметры установки окончаний строк и установили отображения unicode. (см.Рис. -@fig:003)

![Подготовили к работе с git.](image/3.png){ #fig:003 width=70% }

4. Создали файла README.md, добавили ее в git репозиторий и сделали commit. (см.Рис. -@fig:004)

![Создание файла](image/4.png){ #fig:004 width=70% }

5. Добавили созданный файл в GitHub. (см.Рис. -@fig:005)

![Файла в GitHub](image/5.png){ #fig:005 width=70% }

6. Создали ssh-ключ. (см.Рис. -@fig:006)

![Создание ssh-ключ](image/6.png){ #fig:006 width=70% }

7. Добавили созданный ключ в GitHub. (см.Рис. -@fig:007)

![Ssh-ключ в GitHub](image/7.png){ #fig:007 width=70% }

8. Подключились к git с помощью ssh-ключа. (см.Рис. -@fig:008)

![Подключение](image/8.png){ #fig:008 width=70% }

9. Сделали релиз на GitHub. (см.Рис. -@fig:009)

![Релиз](image/9.png){ #fig:009 width=70% }

10. Разобрались с разметками Markdown.(см.Рис. -@fig:010)

![Разметки Markdown](image/10.png){ #fig:010 width=70% }

# Выводы

После выполнения Лабораторной работы №1 мы ознакомились с GitHub, ее интерфейском и как с ней работать. 
Также познакомились с основными возможностями разметки Markdown.
