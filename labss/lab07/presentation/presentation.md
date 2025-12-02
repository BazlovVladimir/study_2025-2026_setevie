---
lang: ru-RU
title: Лабораторная работа №7
subtitle: Настройка DHCP для IPv4 и IPv6
author:
  - Владимир Базлов
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 29 ноября 2025

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

Получить практические навыки настройки DHCP  
для IPv4 и IPv6 на маршрутизаторе VyOS.

# Настройка IPv4

## Начальная топология

![Топология сети](Screenshot_1.png){ width=70% }

## Конфигурация маршрутизатора

![Системные параметры](Screenshot_2.png){ width=70% }

## DHCP-сервер IPv4

![Настройка DHCP IPv4](Screenshot_3.png){ width=70% }

## Проверка работы DHCP

![DHCP статистика](Screenshot_4.png){ width=70% }

## Адресация PC1

![Выдача адреса PC1](Screenshot_5.png){ width=70% }

## Проверка связности

![Проверка ping](Screenshot_6.png){ width=70% }

## Журнал DHCP и анализ трафика

![DHCP трафик](Screenshot_9.png){ width=70% }

# Настройка IPv6 Stateless

## Расширенная топология

![Топология сети](Screenshot_10.png){ width=70% }

## IPv6-адреса маршрутизатора

![Интерфейсы IPv6](Screenshot_11.png){ width=70% }

## Router Advertisements и DHCPv6 Stateless

![DHCPv6 Stateless](Screenshot_12.png){ width=70% }

## Конфигурация RA и DHCPv6

![Конфиг VyOS](Screenshot_13.png){ width=70% }

## Адресация PC2

![PC2 IPv6](Screenshot_14.png){ width=70% }

## DHCPv6 Stateless — запрос параметров

![DHCPv6 PC2](Screenshot_15.png){ width=70% }

## DHCPv6 leases

![DHCPv6 leases Stateless](Screenshot_16.png){ width=70% }

## Анализ DHCPv6 Stateless

![DHCPv6 трафик](Screenshot_17.png){ width=70% }

# Настройка IPv6 Stateful

## DHCPv6 Stateful — конфигурация маршрутизатора

![DHCPv6 Stateful настройки](Screenshot_18.png){ width=70% }

## Адресация PC3 (SLAAC)

![PC3 SLAAC](Screenshot_19.png){ width=70% }

## DHCPv6 Stateful — получение адреса

![Процесс DHCPv6](Screenshot_20.png){ width=70% }

## Проверка настроек PC3

![Параметры PC3](Screenshot_21.png){ width=70% }

## DHCPv6 Stateful — leases

![DHCPv6 leases Stateful](Screenshot_22.png){ width=70% }

## Анализ DHCPv6 Stateful

![DHCPv6 Request](Screenshot_23.png){ width=70% }

# Итоги работы

## Выводы

- Настроена сеть с поддержкой IPv4 и IPv6  
- Реализованы DHCP, DHCPv6 Stateless и DHCPv6 Stateful  
- Проверена автонастройка IPv6 через RA и DHCPv6  
- Выполнен анализ DHCP-трафика для обеих версий протокола  
- Подтверждена корректная работа распределения адресов в сети

