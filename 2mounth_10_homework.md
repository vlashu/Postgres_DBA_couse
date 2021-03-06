<details>
<summary>Логическая репликация - важные моменты</summary>
	
> **_NOTE:_** Ссылка на страницу в официальной документации - https://postgrespro.ru/docs/postgresql/10/logical-replication

В настоящее время публикации могут содержать только таблицы. Объекты в них нужно добавлять явным образом, если только публикация не создана для всех таблиц (ALL TABLES)
	
Чтобы можно было реплицировать операции UPDATE и DELETE, в публикуемой таблице должен быть настроен «репликационный идентификатор» для нахождения соответствующих строк для изменения или удаления на стороне подписчика. По умолчанию это первичный ключ, если он создан. Также репликационным идентификатором можно назначить другой уникальный индекс (с некоторыми дополнительными условиями). Если в таблице нет подходящего ключа, в качестве репликационного идентификатора можно задать «full», что будет означать, что ключом будет вся строка. Это, однако, очень неэффективно и должно применяться как крайняя мера, если другого решения нет. 
	
У каждой публикации может быть множество подписчиков.
	
В публикации можно динамически добавлять или удалять отдельные таблицы, используя команду ALTER PUBLICATION.
	
В случае конфликта выдаётся ошибка и репликация останавливается; разрешить возникшую проблему пользователь должен вручную. Подробности конфликта можно найти в журнале сервера-подписчика.
	
При репликации данные будут изменены, даже если они независимо изменялись на стороне подписчика. 
	
При репликации операций UPDATE или DELETE отсутствие данных не вызывает конфликта, так что такие операции просто пропускаются.
	
Разрешение может заключаться либо в изменении данных на стороне подписчика, чтобы они не конфликтовали с приходящим изменением, либо в пропуске транзакции, конфликтующей с существующими данными. Пропустить транзакцию можно, вызвав функцию pg_replication_origin_advance(), которой передаётся в node_name соответствующее имя подписки, а также позиция. Текущие позиции источников можно увидеть в системном представлении pg_replication_origin_status.
	
Схема базы данных и команды DDL не реплицируются.
	
Данные последовательностей не реплицируются (сама последовательность на подписчике будет сохранять стартовое значение)
	
Команды TRUNCATE не реплицируются. 
	
Большие объекты (см. Главу 34) не реплицируются.
	
Реплицировать данные возможно только из базовых таблиц в базовые таблицы. 
</details>



![изображение](https://user-images.githubusercontent.com/93687317/144709211-014a12ac-50de-4a08-a38e-4ac7d52873b4.png)


```sql
-- Создаем пользователя - владельца таблиц

CREATE ROLE test_user WITH LOGIN;

-- Создаем пользователя для репликации (сразу укажем пароль)

CREATE ROLE replica_user WITH PASSWORD '12345678'
	LOGIN
	REPLICATION;

-- Создаем таблицы согласно схеме

CREATE TABLE public.test1 (
	id integer NOT NULL,
	name varchar,
	related_obj_id integer,
	CONSTRAINT test1_pk PRIMARY KEY (id)
);

CREATE TABLE public.related_obj (
	id integer,
	name varchar,
	obj_value integer,
    CONSTRAINT related_obj_pk PRIMARY KEY (id)
);

CREATE TABLE public.test2 (
	id integer NOT NULL,
	name varchar,
	related_obj_id integer,
	CONSTRAINT test2_pk PRIMARY KEY (id)

);

-- назначаем владельцем таблиц пользователя test_user

ALTER TABLE public.test1 OWNER TO test_user;
ALTER TABLE public.related_obj OWNER TO test_user;
ALTER TABLE public.test2 OWNER TO test_user;

-- Создаем внешние ключи согласно схеме

ALTER TABLE public.test1 ADD CONSTRAINT fk_related_obj FOREIGN KEY (related_obj_id)
REFERENCES public.related_obj (id) MATCH FULL
ON DELETE NO ACTION ON UPDATE NO ACTION;

ALTER TABLE public.test2 ADD CONSTRAINT fk_rel_obj_test_2 FOREIGN KEY (related_obj_id)
REFERENCES public.related_obj (id) MATCH FULL
ON DELETE NO ACTION ON UPDATE NO ACTION;

-- Наполнение таблиц
INSERT INTO related_obj VALUES (1, 'ro_1', 1),(2, 'ro_2', 2),(3, 'ro_3', 3),(4, 'ro_4', 4);
INSERT INTO test1 VALUES (1, 'test1_1', 1),(2, 'test1_2', 1),(3, 'test1_3', 2),(4, 'test1_4', 2),(5, 'test1_5', 3);
INSERT INTO test2 VALUES (1, 'test2_1', 3),(2, 'test2_2', 3),(3, 'test2_3', 4),(4, 'test2_4', 4),(5, 'test2_5', 4);
```

Наполнение 1го сервера

```console
postgres=# select * from test1
postgres-# ;
 id |  name   | related_obj_id 
----+---------+----------------
  1 | test1_1 |              1
  2 | test1_2 |              1
  3 | test1_3 |              2
  4 | test1_4 |              2
  5 | test1_5 |              3
(5 rows)
postgres=# select * from test2;
 id |  name   | related_obj_id 
----+---------+----------------
  1 | test2_1 |              3
  2 | test2_2 |              3
  3 | test2_3 |              4
  4 | test2_4 |              4
  5 | test2_5 |              4
(5 rows)
postgres=# select * from related_obj;
 id | name | obj_value 
----+------+-----------
  1 | ro_1 |         1
  2 | ro_2 |         2
  3 | ro_3 |         3
  4 | ro_4 |         4
(4 rows)
```

Наполнение 2го сервера (таблица test1 пустая)

```console
postgres=# select * from test1;
 id | name | related_obj_id 
----+------+----------------
(0 rows)

postgres=# select * from test2;
 id |  name   | related_obj_id 
----+---------+----------------
  1 | test2_1 |              3
  2 | test2_2 |              3
  3 | test2_3 |              4
  4 | test2_4 |              4
  5 | test2_5 |              4
(5 rows)

postgres=# select * from related_obj;
 id | name | obj_value 
----+------+-----------
  1 | ro_1 |         1
  2 | ro_2 |         2
  3 | ro_3 |         3
  4 | ro_4 |         4
(4 rows)
postgres=# 
```

Наполнение 3го сервера (test1 и test2 пустые)

```console
postgres=# select * from test1;
 id | name | related_obj_id 
----+------+----------------
(0 rows)
postgres=# select * from test2;
 id | name | related_obj_id 
----+------+----------------
(0 rows)
postgres=# select * from related_obj;
 id | name | obj_value 
----+------+-----------
  1 | ro_1 |         1
  2 | ro_2 |         2
  3 | ro_3 |         3
  4 | ro_4 |         4
(4 rows)
```
<details>
<summary>Настройка логической репликации</summary>
	
<details>
<summary>Документация</summary>	
	
<details>
<summary>31.8. Параметры конфигурации </summary>
	
(https://postgrespro.ru/docs/postgresql/10/logical-replication-config)

Для осуществления логической репликации необходимо установить несколько параметров конфигурации.

На публикующем сервере параметр wal_level должен иметь значение logical, а в max_replication_slots должно быть задано число не меньше ожидаемого числа подписчиков плюс некоторый резерв для синхронизации таблиц. А в max_wal_senders должно быть значение как минимум равное max_replication_slots плюс число возможных физических реплик, работающих одновременно.

Также на стороне подписчика необходимо установить параметр max_replication_slots, задающий число источников репликации, которые могут отслеживаться. В данном случае он должен быть не меньше числа подписок, на которые будет подписываться данный подписчик. В max_logical_replication_workers необходимо установить значение не меньше числа подписок плюс некоторый резерв для синхронизации таблиц. Кроме того, может потребоваться изменить max_worker_processes, чтобы это число включало дополнительные рабочие процессы для репликации (как минимум max_logical_replication_workers + 1). Заметьте, что некоторые расширения и параллельные запросы также занимают слоты из числа max_worker_processes.
	
</details>
	
<details>	
<summary>31.9. Быстрая настройка</summary>
	
(https://postgrespro.ru/docs/postgresql/10/logical-replication-quick-setup)
	
Сначала установите параметры конфигурации в postgresql.conf:

wal_level = logical

Другие необходимые параметры по умолчанию имеют значения, подходящие для базовой настройки.

В файл pg_hba.conf необходимо внести изменения, чтобы разрешить репликацию (конкретные значения будут зависеть от фактической конфигурации сети и имени пользователя, с которым вы будете подключаться):

host     all     repuser     0.0.0.0/0     md5

Затем в базе данных публикации выполните:

CREATE PUBLICATION mypub FOR TABLE users, departments;

И в базе данных подписчика:

CREATE SUBSCRIPTION mysub CONNECTION 'dbname=foo host=bar user=repuser' PUBLICATION mypub;

Показанная выше команда запустит процесс репликации, который вначале синхронизирует исходное содержимого таблиц users и departments, а затем начнёт перенос инкрементальных изменений в этих таблицах.	
	
</details>
https://stackoverflow.com/questions/43884169/postresql-replication-pg-basebackup-no-pg-hbaconf-entry-for-replication-connecti
	
https://www.8host.com/blog/logicheskaya-replikaciya-postgresql-10-v-ubuntu-18-04/
	
https://infostart.ru/1c/articles/691958/
	
https://habr.com/ru/post/173623/	
</details>
	
```console
postgresql.conf    
listen_addresses = 'localhost, 10.128.0.10' - local master ip (internal ip)
wal_level = logical
```
	
```console
pg_hba.conf
host    replication     replica_user    10.128.0.11/32          md5 (internal ip 2nd)
host    replication     replica_user    10.128.0.12/32          md5 (internal ip 3rd)
```
	
```sql
GRANT ALL PRIVILEGES ON DATABASE postgres TO replica_user;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO replica_user;

-- 1st
CREATE PUBLICATION test1;
ALTER PUBLICATION test1 ADD TABLE test1;
-- 2nd
CREATE PUBLICATION test2;
ALTER PUBLICATION test2 ADD TABLE test2;
-- 1st
CREATE SUBSCRIPTION test2 CONNECTION 'host=10.128.0.11 port=5432 password=12345678 user=replica_user dbname=postgres' PUBLICATION test2;
-- 2nd
CREATE SUBSCRIPTION test1 CONNECTION 'host=10.128.0.10 port=5432 password=12345678 user=replica_user dbname=postgres' PUBLICATION test1;
-- 3rd
postgres=# CREATE SUBSCRIPTION test2 CONNECTION 'host=10.128.0.11 port=5432 password=12345678 user=replica_user dbname=postgres' PUBLICATION test2;
```
```console	
ERROR:  could not connect to the publisher: connection to server at "10.128.0.11", port 5432 failed: FATAL:  no pg_
hba.conf entry for replication connection from host "10.128.0.10", user "replica_user", SSL on
connection to server at "10.128.0.11", port 5432 failed: FATAL:  no pg_hba.conf entry for replication connection fr
om host "10.128.0.10", user "replica_user", SSL off
```
	
В блоке IPv4 дописываем строку с адресом тест2 (надо будет указать реплика и пользователя)
```console
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
host    all             all             10.128.0.11/32          md5
```
создаем подписку
	
```console
postgres=# CREATE SUBSCRIPTION test2 CONNECTION 'host=10.128.0.11 port=5432 password=12345678 user=replica_user dbname=postgres' PUBLICATION test2;
NOTICE:  created replication slot "test2" on publisher
CREATE SUBSCRIPTION
```
на тест2 тоже самое, проверяем тест2:
	
```console	
postgres=# select * from test1;
 id |  name   | related_obj_id 
----+---------+----------------
  1 | test1_1 |              1
  2 | test1_2 |              1
  3 | test1_3 |              2
  4 | test1_4 |              2
  5 | test1_5 |              3
(5 rows)
postgres=# 
```
репликация тест2 прошла.
	
Проблема!
```console		
postgres=# select * from test2;                                                                                    
 id |  name   | related_obj_id 
----+---------+----------------
  1 | test2_1 |              3
  2 | test2_2 |              3
  3 | test2_3 |              4
  4 | test2_4 |              4
  5 | test2_5 |              4
(5 rows)
	
postgres=# truncate test2;
TRUNCATE TABLE
	
postgres=# select * from test2;
 id |  name   | related_obj_id 
----+---------+----------------
  1 | test2_1 |              3
  2 | test2_2 |              3
  3 | test2_3 |              4
  4 | test2_4 |              4
  5 | test2_5 |              4
  6 | test2_6 |              4
(6 rows)
postgres=# 
```
	
```console		
postgres=# CREATE SUBSCRIPTION test4 CONNECTION 'host=10.128.0.10 port=5432 password=12345678 user=replica_user dbname=postgres' PUBLICATION test1;
NOTICE:  created replication slot "test4" on publisher
CREATE SUBSCRIPTION
postgres=# CREATE SUBSCRIPTION test5 CONNECTION 'host=10.128.0.11 port=5432 password=12345678 user=replica_user dbname=postgres' PUBLICATION test2;
NOTICE:  created replication slot "test5" on publisher
CREATE SUBSCRIPTION
	
postgres=# select * from test1;
 id |  name   | related_obj_id 
----+---------+----------------
  1 | test1_1 |              1
  2 | test1_2 |              1
  3 | test1_3 |              2
  4 | test1_4 |              2
  5 | test1_5 |              3
(5 rows)
postgres=# select * from test2;
 id |  name   | related_obj_id 
----+---------+----------------
  1 | test2_1 |              3
  2 | test2_2 |              3
  3 | test2_3 |              4
  4 | test2_4 |              4
  5 | test2_5 |              4
  6 | test2_6 |              4
(6 rows)
postgres=# 
```
	
	
Значение replication показывает, что запись соответствует, если запрашивается подключение для физической репликации (имейте в виду, что для таких подключений не выбирается какая-то конкретная база данных)
