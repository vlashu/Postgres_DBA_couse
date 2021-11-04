### Домашнее задание: месяц 1 занятие 3

> :warning:20.04 LTS - Из репозитория ставиться 12 версия postgresql.

> **_NOTE:_**  Процесс создания виртуальных машин и установка postgresql рассмотрены в предидущем ДЗ


провека кластера:
```console
sudo -u postgres pg_lsclusters
Ver Cluster Port Status Owner    Data directory              Log file
12  main    5432 online postgres /var/lib/postgresql/12/main /var/log/postgresql/postgresql-12-main.log
```
зайдите из под пользователя postgres в psql и сделайте произвольную таблицу
```sql
create table test(c1 text); insert into test values('1'); \q
```

остановите postgres
```console
sudo -u postgres pg_ctlcluster 12 main stop
Warning: stopping the cluster using pg_ctlcluster will mark the systemd unit as failed. Consider using systemctl:
  sudo systemctl stop postgresql@12-main
```
создание нового диска и его монтирование:
установка утилиты parted
```console
sudo apt-get update
sudo apt-get install parted
```  
идентификация нового диска
```console
user@host:~$     sudo parted -l | grep Error
Error: /dev/sdb: unrecognised disk label
```  
партиционирование диска
```console  
user@host:~$ sudo parted /dev/sdb mklabel gpt
Information: You may need to update /etc/fstab.
user@host:~$ sudo parted /dev/sdb mklabel gpt
Warning: The existing disk label on /dev/sdb will be destroyed and all data on this disk will be lost. Do you want to continue?
Yes/No? Yes                                                               
Information: You may need to update /etc/fstab.
user@host:~$ sudo parted -a opt /dev/sdb mkpart primary ext4 0% 100%
Information: You may need to update /etc/fstab.
user@host:~$ lsblk                                  
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0     7:0    0  55.4M  1 loop /snap/core18/2128
loop1     7:1    0  61.8M  1 loop /snap/core20/1081
loop2     7:2    0 248.8M  1 loop /snap/google-cloud-sdk/199
loop3     7:3    0  67.3M  1 loop /snap/lxd/21545
loop4     7:4    0  32.3M  1 loop /snap/snapd/13170
sda       8:0    0    10G  0 disk 
├─sda1    8:1    0   9.9G  0 part /
├─sda14   8:14   0     4M  0 part 
└─sda15   8:15   0   106M  0 part /boot/efi
sdb       8:16   0    10G  0 disk 
└─sdb1    8:17   0    10G  0 part 
```
создание файловой системы
```console  
user@host:~$ sudo mkfs.ext4 -L datapartition /dev/sdb1
mke2fs 1.45.5 (07-Jan-2020)
Discarding device blocks: done                            
Creating filesystem with 2620928 4k blocks and 655360 inodes
Filesystem UUID: b789fdca-f3e7-48cd-b527-b41fc7391387
Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632
Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done 
```
монтирование
```console 
user@host:~$ sudo mkdir -p /mnt/data
user@host:~$ sudo mount -o defaults /dev/sdb1 /mnt/data
user@host:~$ sudo nano /etc/fstab
user@host:~$ df -h -x tmpfs -x devtmpfs
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       9.6G  2.0G  7.6G  21% /
/dev/loop0       56M   56M     0 100% /snap/core18/2128
/dev/loop1       62M   62M     0 100% /snap/core20/1081
/dev/loop2      249M  249M     0 100% /snap/google-cloud-sdk/199
/dev/loop3       68M   68M     0 100% /snap/lxd/21545
/dev/loop4       33M   33M     0 100% /snap/snapd/13170
/dev/sda15      105M  5.2M  100M   5% /boot/efi
/dev/sdb1       9.8G   37M  9.3G   1% /mnt/data
```
выделение прав и перенос данных
```console 
user@host:~$ sudo chown -R postgres:postgres /mnt/data/
user@host:~$ sudo mv /var/lib/postgresql/12 /mnt/data
```
попытка запуска
```console 
user@host:~$ sudo -u postgres pg_ctlcluster 12 main start
Error: /var/lib/postgresql/12/main is not accessible or does not exist
```

> :warning:Попытка запуска не удалась т.к. искомая папка отсутствует по пути поиска. Для исправления данной ошибки скорректирован путь в файле postgresql.conf (параметр data_directory)


```console 
user@host:~$ sudo nano /etc/postgresql/12/main/postgresql.conf 
data_directory = '/mnt/data/12/main'            # use data in another directory
```
кластер поднялся
```console 
user@host:~$ sudo -u postgres pg_lsclusters
Ver Cluster Port Status Owner    Data directory    Log file
12  main    5432 online postgres /mnt/data/12/main /var/log/postgresql/postgresql-12-main.log
```

выполнение запроса к таблице
```sql
user@host:~$ sudo -u postgres psql
psql (12.8 (Ubuntu 12.8-0ubuntu0.20.04.1))
Type "help" for help.
postgres=# select * from test;
 c1 
----
 1
 1
(2 rows)
postgres=# 
```

### Часть со "*"

> **_NOTE:_**  Процесс создания виртуальных машин и установка postgresql рассмотрены в предидущем ДЗ


удаление /var/lib/postgresql/
```console 
user@host:~$ cd /var/lib/postgresql/
user@host:/var/lib/postgresql$ sudo rm -rf  12/
user@host:/var/lib/postgresql$ ls
```
попытка запуска кластера
```console 
user@host:/var/lib/postgresql$ sudo -u postgres pg_lsclusters
Ver Cluster Port Status Owner     Data directory              Log file
12  main    5432 online <unknown> /var/lib/postgresql/12/main /var/log/postgresql/postgresql-12-main.log
user@host:/var/lib/postgresql$ sudo systemctl stop postgresql@12-main
user@host:/var/lib/postgresql$ sudo -u postgres pg_lsclusters
Ver Cluster Port Status Owner     Data directory              Log file
12  main    5432 down   <unknown> /var/lib/postgresql/12/main /var/log/postgresql/postgresql-12-main.log
user@host:/var/lib/postgresql$ sudo systemctl start postgresql@12-main
Job for postgresql@12-main.service failed because the service did not take the steps required by its unit configuration.
See "systemctl status postgresql@12-main.service" and "journalctl -xe" for details.
```
> :warning: Кластер не поднялся, примечательно, что Owner - \<unknown>

установка parted
```console 
user@host:/var/lib/postgresql$ sudo apt-get install parted
user@host:/var/lib/postgresql$ sudo parted -l | grep Error
```
исправление путей в postgresql.conf и попытка запуска
```console 
user@host:/$ sudo nano /etc/postgresql/12/main/postgresql.conf 
user@host:/$ sudo systemctl start postgresql@12-main
Job for postgresql@12-main.service failed because the service did not take the steps required by its unit configuration.
See "systemctl status postgresql@12-main.service" and "journalctl -xe" for details.
```
> :warning: Кластер не поднялся, диск не смонтирован

процесс монтирования диска
```console 
user@host:/mnt$ lsblk
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0     7:0    0  55.4M  1 loop /snap/core18/2128
loop1     7:1    0  61.8M  1 loop /snap/core20/1081
loop2     7:2    0 248.8M  1 loop /snap/google-cloud-sdk/199
loop3     7:3    0  67.3M  1 loop /snap/lxd/21545
loop4     7:4    0  32.3M  1 loop /snap/snapd/13170
sda       8:0    0    10G  0 disk 
├─sda1    8:1    0   9.9G  0 part /
├─sda14   8:14   0     4M  0 part 
└─sda15   8:15   0   106M  0 part /boot/efi
sdb       8:16   0    10G  0 disk 
└─sdb1    8:17   0    10G  0 part 
user@host:/mnt$     sudo mkdir -p /mnt/data
user@host:/mnt$ sudo mount -o defaults /dev/sdb1 /mnt/data
```
попытка запуска кластера
```console 
user@host:/mnt$ sudo systemctl start postgresql@12-main
user@host:/mnt$ sudo -u postgres psql
psql (12.8 (Ubuntu 12.8-0ubuntu0.20.04.1))
Type "help" for help.

postgres=# \l
                              List of databases
   Name    |  Owner   | Encoding | Collate |  Ctype  |   Access privileges   
-----------+----------+----------+---------+---------+-----------------------
 postgres  | postgres | UTF8     | C.UTF-8 | C.UTF-8 | 
 template0 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
 template1 | postgres | UTF8     | C.UTF-8 | C.UTF-8 | =c/postgres          +
           |          |          |         |         | postgres=CTc/postgres
(3 rows)

postgres=# select * from test;
 c1 
----
 1
 1
(2 rows)
```








