
# Домашнее задание к занятию "5.2. Применение принципов IaaC в работе с виртуальными машинами"

## Задача 1

- Опишите своими словами основные преимущества применения на практике IaaC паттернов.  
<b>Основные преимущества - скорость предоставления инфраструктуры для разработки, тестирования и масштабирования, а также гарантия получения одного и того же результата при разворачивании инфраструктуры для любой из вышеперечисленных задач. </b>
- Какой из принципов IaaC является основополагающим?  
<b>Основополагающий принцип - идемпотентность</b>

## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?  
<b>Не требует установки PKI-окружения, использует текущую SSH инфраструктуру.</b>
- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?  
<b>С точки зрения построения инфраструктуры более надежен и удобен push т.к. есть некий хост-менеджер (и несколько хостов с репликами, готовые его подменить), с которого происходит быстрое управление и на котором находится вся актуальная информация об инфраструктуре</b>

## Задача 3

Установить на личный компьютер:

- VirtualBox  
<b>6.1.32r149290</b>
- Vagrant  
<b>Vagrant 2.2.19</b>
- Ansible  
<b>Ansible 2.9.6</b>

*Приложить вывод команд установленных версий каждой из программ, оформленный в markdown.*
