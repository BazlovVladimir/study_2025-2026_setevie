---
lang: ru-RU
title: Лабораторная работа №6
subtitle: Адресация IPv4 и IPv6. Двойной стек
author:
  - Владимир Базлов
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 17 ноября 2025

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Цель работы

## Основная цель

Изучить принципы распределения IPv4- и IPv6-адресов  
и выполнить настройку адресного пространства на устройствах сети.

# Настройка в GNS3

## Назначение адресов

![Топология сети](Screenshot_1.png){ width=70% }

## Проверка сетевой связности

![Проверка ping и trace](Screenshot_8.png){ width=70% }

## Адреса узлов

![PC3 IPv6](Screenshot_9.png){ width=70% }

## Маршрутизатор VyOS

![VyOS IPv6 config](Screenshot_12.png){ width=70% }

## PC3 → PC4 и сервер

![PC3 ping IPv6](Screenshot_13.png){ width=70% }

# Анализ сетевого трафика

## ARP (IPv4)

![ARP traffic](Screenshot_15.png){ width=70% }

## ICMPv4

![ICMP IPv4](Screenshot_16.png){ width=70% }

## ICMPv6

![ICMPv6](Screenshot_17.png){ width=70% }

# Самостоятельная часть

## Используемые подсети

IPv4
- Подсеть 1: **10.10.1.96/27**  
- Подсеть 2: **10.10.1.16/28**

IPv6
- 2001:db8:1:1::/64  
- 2001:db8:1:4::/64

## Топология подсети

![Топология сети](Screenshot_18.png){ width=70% }

## Проверка устройств

![Проверка ping IPv4 и IPv6](Screenshot_23.png){ width=70% }

# Итоги работы

## Выводы

- Выполнено разбиение подсетей IPv4 и IPv6  
- Настроена адресация в топологии GNS3  
- Проверена связность для обоих протоколов  
- Изучены механизмы ARP, ICMP и ICMPv6  
- Реализована работа сети с **двойным стеком IPv4/IPv6**

