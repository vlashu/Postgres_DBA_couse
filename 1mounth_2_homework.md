
Уровень изоляции -  read committed

1st:

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
        
2nd

         id | first_name | second_name 
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
        (2 rows)
        postgres=*# 
        
видите ли вы новую запись и если да то почему? Не вижу. 

1st:
        commit;

2nd:
         id | first_name | second_name 
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
          3 | sergey     | sergeev
        (3 rows)
        postgres=*# 
        Page down
видите ли вы новую запись и если да то почему? 
Вижу. Была выполнена фиксация транзакции. Уровень изоляции допускает аномалию "Неповторяемое чтение"

начать новые но уже repeatable read транзации        
        
1st:
        postgres=# set transaction isolation level repeatable read;
        SET
        postgres=*# show transaction isolation level
        ;
         transaction_isolation
        -----------------------
         repeatable read
        (1 row)

        postgres=*#
    
2nd:
        postgres=# set transaction isolation level repeatable read;
        SET
        postgres=*# show transaction isolation level
        postgres-*# ;
         transaction_isolation 
        -----------------------
         repeatable read
        (1 row)
        postgres=*# 
        
        
        
1st:
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
        
2nd:

        postgres=*# select * from persons                           
        ;
         id | first_name | second_name 
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
          3 | sergey     | sergeev
        (3 rows)
        postgres=*# 
        
видите ли вы новую запись и если да то почему? 
Не вижу

1st:
        commit;
        
2nd:
         id | first_name | second_name 
        ----+------------+-------------
          1 | ivan       | ivanov
          2 | petr       | petrov
          3 | sergey     | sergeev
        (3 rows)
        postgres=*# 

видите ли вы новую запись и если да то почему? 
Не вижу

2nd:

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
        
видите ли вы новую запись и если да то почему? 
Да, вижу. Уровень изоляции не допускает аномалию "Неповторяемое чтение". 
Запись становится видна в новой транзакции, открытой после завершения транзакции, выполнившей изменение данных.
