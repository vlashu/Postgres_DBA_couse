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
	

</details>



![изображение](https://user-images.githubusercontent.com/93687317/144709211-014a12ac-50de-4a08-a38e-4ac7d52873b4.png)


```sql
-- Создаем пользователя - владельца таблиц

CREATE ROLE test_user WITH LOGIN;

-- Создаем пользователя для репликации

CREATE ROLE replica_user WITH 
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