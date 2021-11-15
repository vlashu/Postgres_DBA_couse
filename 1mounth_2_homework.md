
### Уровень изоляции -  read committed

1st:
```console
        WARNING:  there is already a transaction in progress
        BEGIN
        postgres=*# insert into persons(first_name, second_name) values('sergey', 'sergeev');
        INSERT 0 1
        postgres=*# select * from persons
        ;
         id | first_name | second_name
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
          3 | sergey     | sergeev
        (3 rows)

        postgres=*#

```
2nd
```console
         id | first_name | second_name 
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
        (2 rows)
        postgres=*# 

```
видите ли вы новую запись и если да то почему? 

Не вижу. 

1st:
```console
        commit;

```
2nd:
```console
         id | first_name | second_name 
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
          3 | sergey     | sergeev
        (3 rows)
        postgres=*# 
        Page down

```
видите ли вы новую запись и если да то почему? 

Вижу. 

> **_NOTE:_**  Была выполнена фиксация транзакции. Уровень изоляции допускает аномалию "Неповторяемое чтение"



### Уровень изоляции -  repeatable read

начать новые но уже repeatable read транзации        
        
1st:

```console
        postgres=# set transaction isolation level repeatable read;
        SET
        postgres=*# show transaction isolation level
        ;
         transaction_isolation
        -----------------------
         repeatable read
        (1 row)

        postgres=*#
```
2nd:

```console
        postgres=# set transaction isolation level repeatable read;
        SET
        postgres=*# show transaction isolation level
        postgres-*# ;
         transaction_isolation 
        -----------------------
         repeatable read
        (1 row)
        postgres=*# 
```
        
        
1st:

```console
        postgres=*#  insert into persons(first_name, second_name) values('sveta', 'svetova');
        INSERT 0 1
        postgres=*# select * from persons
        ;
         id | first_name | second_name
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
          3 | sergey     | sergeev
          4 | sveta      | svetova
        (4 rows)

        postgres=*#
```
2nd:

```console
        postgres=*# select * from persons                           
        ;
         id | first_name | second_name 
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
          3 | sergey     | sergeev
        (3 rows)
        postgres=*# 
```
видите ли вы новую запись и если да то почему? 
Не вижу

1st:
```console
        commit;
```
2nd:
```console
         id | first_name | second_name 
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
          3 | sergey     | sergeev
        (3 rows)
        postgres=*# 
```
видите ли вы новую запись и если да то почему? 
Не вижу

2nd:
```console
        postgres=*# rollback;
        ROLLBACK
        postgres=# begin;
        BEGIN
        postgres=*# select * from persons
        ;
         id | first_name | second_name 
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
          3 | sergey     | sergeev
          4 | sveta      | svetova
        (4 rows)
        postgres=*# 
```      
видите ли вы новую запись и если да то почему? 
Да, вижу. 
> **_NOTE:_**  Уровень изоляции не допускает аномалию "Неповторяемое чтение". 
Запись становится видна в новой транзакции, открытой после завершения транзакции, выполнившей изменение данных.
