---
lang: ru-RU
title: Лабораторная работа №5
subtitle: Простые сети в GNS3. Анализ трафика
author:
  - Владимир Базлов
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 03 декабря 2025

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

Построить простые модели сетей в GNS3  
на базе коммутатора, маршрутизаторов FRR и VyOS,  
а также выполнить анализ трафика с помощью Wireshark.

# Простая сеть в GNS3

## Топология сети

- **PC1:** 192.168.1.11/24, шлюз 192.168.1.1  
- **PC2:** 192.168.1.12/24, шлюз 192.168.1.1  
![Топология сети](Screenshot_1.png){ width=70% }

## Настройка PC1 и PC2

![Настройка PC1](Screenshot_2.png){ width=70% }

## Настройка PC1 и PC2

![Настройка PC2](Screenshot_3.png){ width=70% }

# Анализ трафика Wireshark

## ARP-трафик

- Gratuitous ARP  
- ARP Request / Reply  
- Разрешение MAC-адресов

![ARP](Screenshot_4.png){ width=70% }

## ICMP-трафик

- Echo Request / Echo Reply  
- TTL, идентификаторы, полезная нагрузка

![ICMP](Screenshot_6.png){ width=70% }

## UDP Echo

- Исходный порт — случайный  
- Порт назначения — 7  
- Без установления соединения

![UDP](Screenshot_7.png){ width=70% }

## TCP Echo

- Трёхстороннее рукопожатие  
- Передача данных  
- Закрытие соединения

# Сеть с маршрутизатором FRR

## Топология

- PC1: 192.168.1.10/24  
- FRR eth0: 192.168.1.1/24  

![Топология FRR](Screenshot_8.png){ width=70% }

## Настройка PC1 и маршрутизатора

![PC1](Screenshot_9.png){ width=70% }

## Настройка PC1 и маршрутизатора

![FRR настройки](Screenshot_10.png){ width=70% }

## Проверка работоспособности

![ICMP FRR](Screenshot_14.png){ width=70% }

# Сеть с маршрутизатором VyOS

## Топология

- PC1: 192.168.1.10/24  
- VyOS eth0: 192.168.1.1/24  

![Топология VyOS](Screenshot_15.png){ width=70% }

## Настройка устройств

![VyOS конфигурация](Screenshot_16.png){ width=70% }

## Проверка связности

![Пинг VyOS](Screenshot_18.png){ width=70% }

# Итоги работы

## Выводы

- Построены три сетевые топологии в GNS3  
- Настроена IPv4-адресация на всех устройствах  
- Выполнена проверка ICMP-доступности  
- Проанализированы ARP, ICMP, UDP, TCP-пакеты  
- Подтверждена корректная работа маршрутизаторов FRR и VyOS  
- Захват трафика показал правильное формирование ARP-таблицы и передачу ICMP-пакетов
