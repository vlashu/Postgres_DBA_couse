
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
	value integer
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
```
