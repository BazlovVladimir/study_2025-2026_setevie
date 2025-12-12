---
## Front matter
title: "Отчёт по лабораторной работе №5"
subtitle: "Простые сети в GNS3. Анализ трафика"
author: "Владимир Базлов"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true
toc-depth: 2
lof: true
lot: true
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
    - spelling=modern
    - babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float}
  - \floatplacement{figure}{H}
---

# Цель работы

Построение простейших моделей сети на базе коммутатора и маршрутизаторов FRR и VyOS в GNS3, анализ трафика посредством Wireshark.

# Выполнение задания

## Построение простой сети в GNS3 и анализ трафика

В GNS3 создан новый проект, после чего в рабочей области размещены два узла VPCS и коммутатор Ethernet. Всем устройствам назначены имена, содержащие имя пользователя, согласно требованиям задания. Коммутатору присвоено имя msk-vabazlov-sw-01, а VPCS — PC1-vabazlov и PC2-vabazlov.

Топология после соединения устройств представлена на рисунке ниже.

![Топология сети](Screenshot_1.png){ #fig:001 width=80% }

Интерфейсы соединений отображены в соответствии с требованиями лабораторной работы.

### Настройка IPv4-адресов на PC-1 и PC-2

После запуска VPCS через Start и открытия консоли командой Console была выполнена настройка IP-адресации.

### Настройка PC1-vabazlov

PC-1 получил IP-адрес 192.168.1.11/24 и шлюз 192.168.1.1. Команда для просмотра синтаксиса ip /? использована перед вводом параметров.

![Настройка PC1](Screenshot_2.png){ #fig:002 width=80% }

### Настройка PC2-vabazlov

PC-2 был настроен с адресом 192.168.1.12/24 и шлюзом 192.168.1.1. После сохранения конфигурации выполнено тестирование доступности PC-1, пинг прошёл успешно.

![Настройка PC2](Screenshot_3.png){ #fig:003 width=80% }

## Анализ ARP-трафика в Wireshark

Для анализа ARP-кадров произведён запуск захвата на линии между PC-1 и коммутатором. После включения узлов Wireshark начал фиксировать ARP-трафик, возникший при назначении IP-адресов и выполнении первых запросов.

На снимке отображён обмен Gratuitous ARP и ARP-запросами с указанием MAC-адресов, IP-адресов отправителя и назначения.

![ARP-захват](Screenshot_4.png){ #fig:004 width=80% }

Gratuitous ARP используется для проверки отсутствия конфликта IP, а стандартные ARP-запросы выполняют разрешение MAC-адресов.

### Анализ ICMP-трафика

Перед выполнением ICMP-эхо-запроса на PC-2 были изучены параметры команды ping.

![Ping options](Screenshot_5.png){ #fig:005 width=80% }

Выполнен один ICMP-эхо-запрос к узлу PC-1. В Wireshark зафиксированы кадры типа Echo Request и Echo Reply, содержащие идентификатор, TTL, последовательные номера и полезную нагрузку.

![ICMP-анализ](Screenshot_6.png){ #fig:006 width=80% }

### UDP-эхо-запрос

Выполнена отправка одного echo-пакета в UDP-режиме. В Wireshark отображается пакет с протоколом UDP, случайным исходным портом и портом назначения 7, который используется службой echo.

![UDP-анализ](Screenshot_7.png){ #fig:007 width=80% }

UDP-пакет не устанавливает соединение, содержит только заголовок транспортного уровня и данные.

### TCP-эхо-запрос

При отправке echo-запроса в TCP-режиме фиксируется трёхстороннее рукопожатие SYN → SYN/ACK → ACK. Далее передаются данные и соединение завершается.

Такой обмен соответствует требованиям TCP, который обеспечивает установление соединения перед отправкой данных.

## Построение сети с маршрутизатором FRR в GNS3 и анализ трафика

В GNS3 создан новый проект, после чего на рабочем поле размещены устройства: оконечный узел PC1, коммутатор Ethernet и маршрутизатор FRR. Им присвоены имена согласно требованиям: PC1-vabazlov, msk-vabazlov-sw-01 и msk-vabazlov-gw-01. Устройства соединены в единую топологию.

![Топология сети](Screenshot_8.png){ #fig:008 width=80% }

На узле PC1-vabazlov выполнена настройка IPv4-адреса. Устройству назначен адрес 192.168.1.10/24 и шлюз 192.168.1.1. После сохранения конфигурации была выполнена проверка параметров.

![Настройка PC1](Screenshot_9.png){ #fig:009 width=80% }

Маршрутизатору присвоено имя msk-vabazlov-gw-01.  
На интерфейсе eth0 настроен адрес 192.168.1.1/24. Интерфейс активирован, а конфигурация сохранена.

![Настройка FRR](Screenshot_10.png){ #fig:010 width=80% }

Проверка конфигурации показывает корректно настроенные параметры, включая IP-адрес интерфейса eth0.

![Конфигурация FRR](Screenshot_11.png){ #fig:011 width=80% }

Сводка по интерфейсам предоставляет подтверждение, что интерфейс eth0 находится в состоянии up.

![Интерфейсы FRR](Screenshot_12.png){ #fig:012 width=80% }

На PC1-vabazlov выполнена отправка ICMP-эхо-запросов на адрес маршрутизатора 192.168.1.1. Узел успешно отвечает, что подтверждает корректность настроек.

![Пинг FRR](Screenshot_13.png){ #fig:013 width=80% }

В захвате Wireshark отображаются ICMP Echo Request и Echo Reply между PC1 и маршрутизатором.

![ICMP-трафик FRR](Screenshot_14.png){ #fig:014 width=80% }

## Построение сети с маршрутизатором VyOS

В GNS3 создан новый проект, на рабочей области размещены VPCS, коммутатор Ethernet и маршрутизатор VyOS.  
Устройствам присвоены имена: PC1-vabazlov, msk-vabazlov-sw-01 и msk-vabazlov-gw-01. Устройства соединены в топологию.

![Топология сети VyOS](Screenshot_15.png){ #fig:015 width=80% }

## Настройка PC1

Узел PC1 получил адрес 192.168.1.10/24 с шлюзом 192.168.1.1.

## Настройка маршрутизатора VyOS

На маршрутизаторе после установки образа выполнены следующие операции:

– устройство переведено в режим конфигурации  
– присвоено имя msk-vabazlov-gw-01  
– интерфейсу eth0 задан адрес 192.168.1.1/24  
– изменения применены и сохранены  

![Настройка VyOS](Screenshot_16.png){ #fig:016 width=80% }

Просмотр информации об интерфейсах подтверждает корректность настройки адреса.

![Интерфейсы VyOS](Screenshot_17.png){ #fig:017 width=80% }

## Проверка работоспособности сети

PC1-vabazlov успешно отправляет ICMP-эхо-запросы на маршрутизатор VyOS по адресу 192.168.1.1.

![Пинг VyOS](Screenshot_18.png){ #fig:018 width=80% }

В окне Wireshark видны ICMP Echo Request / Echo Reply между устройствами.

![ICMP-трафик VyOS](Screenshot_19.png){ #fig:019 width=80% }

# Заключение

В ходе работы была построена простейшая сеть в GNS3 на базе коммутатора, маршрутизаторов FRR и VyOS, а также оконечного узла VPCS. Для всех устройств выполнена настройка IPv4-адресации, после чего проведена проверка связности между узлом PC1 и шлюзом. На обоих вариантах маршрутизаторов подтверждена корректная работа сети — эхо-запросы успешно достигали адреса 192.168.1.1, что фиксировалось как в терминале, так и в захваченных пакетах Wireshark.

Захват трафика позволил проанализировать последовательность ARP-обращений при первом обращении к шлюзу и структуру ICMP-пакетов на этапах обмена Echo Request и Echo Reply. Полученные данные демонстрируют корректное разрешение адресов, формирование ARP-таблицы и стабильную передачу ICMP-сообщений.