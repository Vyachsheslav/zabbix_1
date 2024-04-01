# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Андрющенко Вячеслав`


---

### Задание 1  

Установите Zabbix Server с веб-интерфейсом.   

Процесс выполнения

Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.

Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.

Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.

Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

Требования к результаты

Прикрепите в файл README.md скриншот авторизации в админке.

Приложите в файл README.md текст использованных команд в GitHub.


### Решение 1  
![Авторизация](/img/auth.png)

#### Список команд  
1) wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb
2) dpkg -i zabbix-release_6.4-1+ubuntu22.04_all.deb
3) apt update
4) apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
5) apt install postgresql
6) sudo -u postgres createuser --pwprompt zabbix
7) sudo -u postgres createdb -O zabbix zabbix
8) zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
9) nano /etc/zabbix/zabbix_server.conf , редактируем DBPassword=password
10) systemctl restart zabbix-server zabbix-agent apache2
11) systemctl enable zabbix-server zabbix-agent apache2
---

### Задание 2 
Установите Zabbix Agent на два хоста.

Процесс выполнения

Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.

Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.

Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.

Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.

Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

Требования к результаты

Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу

Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером

Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.

Приложите в файл README.md текст использованных команд в GitHub

### Решение 2 
![Агенты](/img/agents.png) 
![Лог](/img/agent_log.png) 
![Data](/img/data.png) 


#### Список команд  
1) wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb 
2) dpkg -i zabbix-release_6.4-1+ubuntu22.04_all.deb 
3) apt update 
4) apt install zabbix-agent
5) nano /etc/zabbix/zabbix_agentd.conf , меняем строчку Server=ip заббикс сервера 
6) systemctl restart zabbix-agent
7) systemctl enable zabbix-agent 
