создал кластер PostgresSQL 13 GCE
создал БД testdb


<details>
<summary>зашел под postgres:</summary>

```sql
    testdb=# create table t1 (c1 integer);
    CREATE TABLE
    testdb=# insert into t1 values (1)
    testdb-# ;
    INSERT 0 1
    testdb=# create role readonly;
    CREATE ROLE
    testdb=# GRANT CONNECT ON DATABASE testdb TO readonly;
    GRANT
```
</details>

<details>
<summary>отвлекся и забыл создать схему (также вместо testread создал пользователя test123 с паролем 1234, команды прокидывал блоком):</summary>

```sql
    testdb=# GRANT USAGE ON SCHEMA testnm TO readonly;
    ERROR:  schema "testnm" does not exist
    testdb=# GRANT SELECT ON ALL TABLES IN SCHEMA testnm TO readonly;
    ERROR:  schema "testnm" does not exist
    testdb=# create user test123 with encrypted password '1234';
    CREATE ROLE
    testdb=# GRANT readonly to test123;
    GRANT ROLE
```
</details>


<details>
<summary>досоздал схему:</summary>

```sql
    testdb=# create schema testnm;
    CREATE SCHEMA
```
</details>

<details>
<summary>переназначил таблице t1 схему testnm:</summary>

```sql
    testdb=# ALTER TABLE t1 SET SCHEMA testnm;
    ALTER TABLE
```
</details>

<details>
<summary>проверил через select, что t1 в схеме testnm:</summary>

```sql
    testdb=# select * from testnm.t1;
     c1 
    ----
      1
    (1 row)
```
</details>

<details>
<summary>довыдал права на роль:</summary>

```sql
    testdb=# GRANT USAGE ON SCHEMA testnm TO readonly;
    GRANT
    testdb=# GRANT SELECT ON ALL TABLES IN SCHEMA testnm TO readonly;
    GRANT
```
</details>


<details>
<summary>попытался подключиться пользователем testread :</summary>

```console
    user@host:/etc/postgresql/13/main$ psql -p 5432 -h localhost -U testread -W -d testdb
    Password: 
    psql: error: connection to server at "localhost" (127.0.0.1), port 5432 failed: FATAL:  password authentication failed for user "testread"
    connection to server at "localhost" (127.0.0.1), port 5432 failed: FATAL:  password authentication failed for user "testread"
```
</details>



<details>
<summary>попытался подключиться пользователем postgres (вот тут удивился):</summary>

```console
    user@host:/etc/postgresql/13/main$ psql -p 5432 -h localhost -U postgres -W -d postgres
    Password: 
    psql: error: connection to server at "localhost" (127.0.0.1), port 5432 failed: FATAL:  password authentication failed for user "postgres"
    connection to server at "localhost" (127.0.0.1), port 5432 failed: FATAL:  password authentication failed for user "postgres"
```
</details>

<details>
<summary>переназначил пароль postgres:</summary>

```sql
    postgres=# ALTER USER postgres PASSWORD 'postgres';
    ALTER ROLE
```
</details>

cмог подключиться пользователем postgres и осознал проблему с testread - вместо него я создал test123, под ним успешно зашел

<details>
<summary>cделал select * from t1; увидел ошибку (логично, я явно указал схему для t1, запрос select * from testnm.t1; успешно отработал):</summary>

```sql
    testdb=> select * from t1;
    ERROR:  relation "t1" does not exist
    LINE 1: select * from t1;
                          ^
    testdb=> select * from testnm.t1;
     c1 
    ----
      1
    (1 row)
    testdb=> 
```
</details>

с п.18 по п.21 пропустил, т.к. все работает как должно, кажется...
и с п.22 по п.33 тоже пропустил

<details>
<summary>выполнил команды create table t2(c1 integer); insert into t2 values (2); (без явного указания схемы таблица создалась в схеме public)</summary>

```sql
    testdb=> create table t2(c1 integer);
    CREATE TABLE
    testdb=> insert into t2 values (2);
    INSERT 0 1
    testdb=> select * from t2
    testdb-> ;
     c1 
    ----
      2
    (1 row)
    testdb=> 
```
</details>


<details>
<summary>выполнил команду create table t3(c1 integer); insert into t2 values (2);</summary>

```sql
        testdb=> create table t3(c1 integer); insert into t2 values (2);
        CREATE TABLE
        INSERT 0 1
        testdb=> select * from t2                                       
        ;
         c1 
        ----
          2
          2
        (2 rows)
        testdb=> select * from t3
        ;
         c1 
        ----
        (0 rows)
        testdb=> 
```
</details>

в схеме public создалась таблица t3
в таблицу t2 записалось значение 2 (получилось 2 одинаковых значения), т.к. столбец c1 не pk и отсутствует ограничение UNIQUE
