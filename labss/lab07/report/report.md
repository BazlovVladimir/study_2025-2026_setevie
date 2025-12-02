---
## Front matter
title: "Отчёт по лабораторной работе №7"
subtitle: "Адресация IPv4 и IPv6. Настройка DHCP"
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

Получение навыков настройки службы DHCP на сетевом оборудовании для распределения адресов IPv4 и IPv6.

# Выполнение задания

## Создание проекта и размещение устройств в топологии

В GNS3 создан новый проект и на рабочем поле размещены устройства в соответствии с заданной схемой: маршрутизатор VyOS, коммутатор и хост VPCS. Устройствам присвоены имена по установленным правилам:
– PC1-vabazlov  
– vabazlov-sw-01  
– vabazlov-gw-01  

![Топология сети](Screenshot_1.png){ #fig:001 width=60% }

На соединении между коммутатором и маршрутизатором включён захват трафика для анализа DHCP-обмена.

## Настройка маршрутизатора VyOS

После загрузки маршрутизатор был установлен командой install image и перезагружен. В режиме конфигурирования заданы имя устройства, доменное имя и создан пользователь vabazlov. Затем пользователь vyos удалён.

![Настройка системных параметров VyOS](Screenshot_2.png){ #fig:002 width=80% }

## Настройка IPv4-адресации и DHCP на маршрутизаторе

На интерфейсе eth0 настроен адрес 10.0.0.1/24. Далее добавлена конфигурация DHCP-сервера: доменное имя, DNS-сервер, шлюз и диапазон выдаваемых адресов 10.0.0.2–10.0.0.253.

![Настройка интерфейсов и DHCP](Screenshot_3.png){ #fig:003 width=80% }

Проверка работы DHCP-службы:

![Статистика DHCP-сервера](Screenshot_4.png){ #fig:004 width=80% }

## Получение IP-адреса на PC1

На PC1 выполнено получение адреса по DHCP c декодированием пакетов. Клиент успешно получил параметры сети:

– IP-адрес: 10.0.0.2/24  
– Шлюз: 10.0.0.1  
– DNS-сервер: 10.0.0.1  
– Домен: vabazlov.net  

![Выдача адреса PC1](Screenshot_5.png){ #fig:005 width=80% }

### Пояснение данных DHCP

На экране PC1 отображён полный цикл DHCP:

– Discover — поиск сервера  
– Offer — предложение адреса  
– Request — запрос предложенного адреса  
– ACK — подтверждение выделения IP  

Выведены параметры: маска, шлюз, DNS и доменное имя.

## Проверка конфигурации и связности

Параметры IP на PC1 отображаются корректно.  
Проверка связности с маршрутизатором проходит успешно.

![Проверка IP и ping](Screenshot_6.png){ #fig:006 width=80% }

## Статистика DHCP после выдачи адреса

DHCP-сервер отображает один активный lease.

![Выданные адреса DHCP](Screenshot_7.png){ #fig:007 width=80% }

## Просмотр журнала DHCP-сервера

В журнале VyOS зафиксированы все этапы DHCP-обмена: Discover, Offer, Request, ACK, включая MAC-адрес клиента и интерфейс eth0.

![Логи DHCP](Screenshot_8.png){ #fig:008 width=80% }

## Анализ пакетов DHCP в анализаторе трафика

Захваченные пакеты включают полный цикл DHCP. В примере Request указаны:

– Client IP address: 10.0.0.2  
– Requested IP address: 10.0.0.2  
– Сервер идентификатор: 10.0.0.1  
– Hostname клиента: PC1-vabazlov  

![Анализ DHCP-трафика](Screenshot_9.png){ #fig:009 width=85% }

## Дополнение топологии и размещение устройств

В существующий проект добавлены дополнительные коммутаторы и узлы, включая PC2-vabazlov и PC3-vabazlov, а также Kali Linux CLI, необходимый для работы DHCPv6. Устройства соединены в соответствии с заданной топологией.

![Топология сети](Screenshot_10.png){ #fig:010 width=75% }

Имя устройств изменено в соответствии с правилами:
– Коммутаторы: vabazlov-sw-01, vabazlov-sw-02, vabazlov-sw-03  
– Маршрутизатор: vabazlov-gw-01  
– Узлы: PC1-vabazlov, PC2-vabazlov, PC3-vabazlov  

На соединениях между gw-01 и sw-02/sw-03 включён захват трафика.

## Настройка IPv6 на маршрутизаторе

На маршрутизаторе настроены IPv6-адреса на интерфейсах eth1 и eth2:

– eth1: 2000::1/64  
– eth2: 2001::1/64

![Настройка интерфейсов IPv6](Screenshot_11.png){ #fig:011 width=80% }

Конфигурация сохранена.

## Настройка Router Advertisements и DHCPv6 Stateless

Для интерфейса eth1 включены объявления маршрутизатора (RA) и параметр other-config-flag, указывающий на использование статeless DHCPv6.

DHCPv6 Stateless настроен с общими параметрами:
– DNS-сервер: 2000::1  
– domain-search: vabazlov.net  

![Настройка DHCPv6 Stateless](Screenshot_12.png){ #fig:012 width=80% }

В конфигурации отображается созданная shared-network-name, а также RA-настройки.

![Конфигурация DHCPv6 и RA](Screenshot_13.png){ #fig:013 width=80% }

## Проверка IPv6-конфигурации на PC2

На узле PC2-vabazlov отображаются:
– Link-local адрес fe80::…  
– Автоматически сгенерированный global unicast IPv6-адрес в сети 2000::/64  
– Таблица маршрутизации с маршрутами по умолчанию ::/0 через link-local маршрутизатора  

![Параметры PC2](Screenshot_14.png){ #fig:014 width=80% }

Проверка связности подтверждена успешными ICMPv6-ответами от 2000::1.

DNS-конфигурация включает:
– search vabazlov.net  
– nameserver 2000::1  

## Получение параметров через DHCPv6 Stateless

На PC2 выполнен запрос параметров с использованием DHCPv6:
получены параметры DNS и domain-search. Адрес не назначается, поскольку используется Stateless-режим.

![DHCPv6 запрос PC2](Screenshot_15.png){ #fig:015 width=80% }


## Проверка DHCPv6 leases на маршрутизаторе

На маршрутизаторе отображается таблица выдачи DHCPv6, которая в Stateless-режиме не содержит адресов — так как адреса не назначаются, а предоставляются только параметры.

![DHCPv6 leases](Screenshot_16.png){ #fig:016 width=80% }

## Анализ захваченного трафика DHCPv6

В захваченном трафике присутствуют:
– Router Advertisement от маршрутизатора  
– DHCPv6 Information-Request от PC2  
– DHCPv6 Reply от маршрутизатора  

Пакет Information-Request содержит запрос:
– DNS recursive name server  
– Domain search list  
– NTP server  
– UID клиента  

Ответ сервера корректно предоставляет требуемые параметры.

![Анализ DHCPv6 пакетов](Screenshot_17.png){ #fig:017 width=85% }

## Настройка DHCPv6 Stateful на маршрутизаторе

На интерфейсе eth2 включено объявление маршрутизатора (RA) с флагом managed-flag. Это указывает, что узлы сети должны получать IPv6-адреса с отслеживанием состояния через DHCPv6.

Далее создана разделяемая сеть vabazlov-stateful и настроены:
– подсеть 2001::/64  
– DNS-сервер 2001::1  
– domain-search: vabazlov.net  
– диапазон выделяемых адресов: 2001::100 – 2001::199  

![Настройка DHCPv6 Stateful](Screenshot_18.png){ #fig:018 width=80% }

Конфигурация сохранена.

## Проверка IPv6-конфигурации на PC3

После загрузки PC3 получает адрес через SLAAC и видит параметры RA:

![Проверка IPv6 на PC3](Screenshot_19.png){ #fig:019 width=80% }

В таблице маршрутизации присутствует маршрут по умолчанию через link-local адрес маршрутизатора. DNS настроен в соответствии с параметрами RA.

## Получение адреса по DHCPv6 Stateful

Команда dhclient -6 инициирует полный процесс DHCPv6 (Solicit → Advertise → Request → Reply). Клиент получает:
– IA_NA адрес: из диапазона stateful DHCP  
– DNS-сервер 2001::1  
– доменное имя для поиска  

![Процесс DHCPv6 на PC3](Screenshot_20.png){ #fig:020 width=80% }

После завершения хосту назначен адрес, например 2001::199.

## Повторная проверка настроек на PC3

Проверка интерфейса, маршрутов и DNS подтверждает получение stateful-адреса.

![Параметры сети после получения stateful-адреса](Screenshot_21.png){ #fig:021 width=80% }

Пинг маршрутизатора по адресу 2001::1 выполняется успешно.

Настройки DNS также соответствуют параметрам DHCPv6.

## Статистика DHCPv6 на маршрутизаторе

На маршрутизаторе отображаются активные аренды адресов:

![DHCPv6 leases](Screenshot_22.png){ #fig:022 width=85% }

Выданные адреса, пример:
– 2001::198 — активен, принадлежит первому клиенту  
– 2001::199 — активен, принадлежит PC3  

Каждая запись содержит:
– IAID/DUID клиента  
– время последней связи  
– время окончания аренды  

## Анализ захваченного DHCPv6-трафика

В пакете DHCPv6 Request содержится:
– Client Identifier (DUID, MAC-адрес клиента)  
– Server Identifier  
– IA_NA с запрошенным адресом  
– Параметры: DNS recursive server, Domain Search, Client FQDN  

![Анализ DHCPv6 Request](Screenshot_23.png){ #fig:023 width=85% }

Процесс обмена соответствует последовательности:
1. Solicit от клиента  
2. Advertise от сервера  
3. Request от клиента  
4. Reply с назначением адреса  

Всё соответствует работе DHCPv6 stateful: адреса назначаются сервером, а не генерируются автономно.

# Заключение

В ходе работы рассмотрены способы организации IPv6-адресного пространства и выполнено разбиение сети двумя методами — через Subnet ID и через Interface ID. Сеть /48 даёт возможность формировать иерархию подсетей, изменяя идентификатор подсети, тогда как сеть /64 позволяет разделять пространство только за счёт структуры идентификатора интерфейса. Оба варианта обеспечивают гибкое распределение адресов и позволяют адаптировать архитектуру сети под конкретные задачи.
