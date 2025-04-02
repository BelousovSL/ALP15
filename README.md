# Название выполняемого задания;
Настройка мониторинга

# Текст задания
Настроить дашборд с 4-мя графиками

память;
процессор;
диск;
сеть.

# Описание
С prometeus достаточно плотно работаем на работе а вот с на Zabbix было интересно посмотреть.

Путь. Я создал 4 костомных метрики, на агенете. Почему именно кастомные... Как универсаольный способ..  

```bash
vagrant@belousovZabbix2:~$ ll /etc/zabbix/zabbix_agent2.d/
total 16
drwxr-xr-x 3 root root 4096 Apr  2 18:52 ./
drwxr-xr-x 3 root root 4096 Apr  2 17:20 ../
drwxr-xr-x 2 root root 4096 Apr  2 17:03 plugins.d/
-rw-r--r-- 1 root root  228 Apr  2 18:52 test.conf
```

```bash
vagrant@belousovZabbix2:~$ cat /etc/zabbix/zabbix_agent2.d/test.conf 
UserParameter=my.test,/usr/local/test111.sh
UserParameter=my.test.cpu,/usr/local/mycpy.sh
UserParameter=my.test.df,/usr/local/mydf.sh
UserParameter=my.test.free,/usr/local/myfree.sh
UserParameter=my.test.net,/usr/local/mynet.sh
```

Пример одного из скрипта
```bash
vagrant@belousovZabbix2:~$ cat /usr/local/mycpy.sh

#!/bin/bash

echo $(top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1}')
exit 0
```

Далее, зарегистрировал, Host, потом прописал свои метрики (Items). Потом "нарисовал" dashbord.

Скрин присутствует.