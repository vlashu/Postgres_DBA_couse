
> :warning: запрос для удобства мониторинга
>```sql
>select 
>    pgclass.relname as "Таблица",
>    pdb.datname as "БД",
>    pg_locks.pid as "Process ID",
>    pg_locks.transactionid as "Транзакция",
>    pg_locks.mode as "Блокировка",
>    pg_locks.granted as "Блокировка получена",
>    pg_locks.fastpath as "Блокировка по короткому пути"
>from 
>    pg_locks
>left join pg_database as pdb on pg_locks.database = pdb.oid
>left join pg_class as pgclass on pg_locks.relation = pgclass.oid
>order by pg_locks.pid
>;
>```

log_lock_waits = on
deadlock_timeout = 200

test=# select * from pg_locks;

  locktype  | database | relation | page | tuple | virtualxid | transactionid | classid | objid | objsubid | virtualtransaction |  pid  |      mode       | granted | fastpath 
------------+----------+----------+------+-------+------------+---------------+---------+-------+----------+--------------------+-------+-----------------+---------+----------
 relation   |    16384 |    12141 |      |       |            |               |         |       |          | 7/2                | 20598 | AccessShareLock | t       | t
 virtualxid |          |          |      |       | 7/2        |               |         |       |          | 7/2                | 20598 | ExclusiveLock   | t       | t
 virtualxid |          |          |      |       | 5/2        |               |         |       |          | 5/2                | 20593 | ExclusiveLock   | t       | t
 virtualxid |          |          |      |       | 4/4        |               |         |       |          | 4/4                | 20592 | ExclusiveLock   | t       | t
 virtualxid |          |          |      |       | 3/8        |               |         |       |          | 3/8                | 20590 | ExclusiveLock   | t       | t
(5 rows)


3 сеанса UPDATE

   locktype    | database | relation | page | tuple | virtualxid | transactionid | classid | objid | objsubid | virtualtransaction |  pid  |       mode       | granted | fastpath 
---------------+----------+----------+------+-------+------------+---------------+---------+-------+----------+--------------------+-------+------------------+---------+----------
 relation      |    16384 |    12141 |      |       |            |               |         |       |          | 7/3                | 20598 | AccessShareLock  | t       | t
 virtualxid    |          |          |      |       | 7/3        |               |         |       |          | 7/3                | 20598 | ExclusiveLock    | t       | t
 relation      |    16384 |    16385 |      |       |            |               |         |       |          | 5/2                | 20593 | RowExclusiveLock | t       | t
 virtualxid    |          |          |      |       | 5/2        |               |         |       |          | 5/2                | 20593 | ExclusiveLock    | t       | t
 relation      |    16384 |    16385 |      |       |            |               |         |       |          | 4/4                | 20592 | RowExclusiveLock | t       | t
 virtualxid    |          |          |      |       | 4/4        |               |         |       |          | 4/4                | 20592 | ExclusiveLock    | t       | t
 relation      |    16384 |    16385 |      |       |            |               |         |       |          | 3/8                | 20590 | RowExclusiveLock | t       | t
 virtualxid    |          |          |      |       | 3/8        |               |         |       |          | 3/8                | 20590 | ExclusiveLock    | t       | t
 transactionid |          |          |      |       |            |           491 |         |       |          | 4/4                | 20592 | ShareLock        | f       | f
 transactionid |          |          |      |       |            |           491 |         |       |          | 3/8                | 20590 | ExclusiveLock    | t       | f
 tuple         |    16384 |    16385 |    0 |     2 |            |               |         |       |          | 5/2                | 20593 | ExclusiveLock    | f       | f
 transactionid |          |          |      |       |            |           492 |         |       |          | 4/4                | 20592 | ExclusiveLock    | t       | f
 tuple         |    16384 |    16385 |    0 |     2 |            |               |         |       |          | 4/4                | 20592 | ExclusiveLock    | t       | f
 transactionid |          |          |      |       |            |           493 |         |       |          | 5/2                | 20593 | ExclusiveLock    | t       | f
(14 rows)


Журнал:
```console
 datname | usename  |          xact_start           | wait_event_type |     wait_event      |        state        | backend_xid | backend_xmin |                      query                       |         backend_type         
---------+----------+-------------------------------+-----------------+---------------------+---------------------+-------------+--------------+--------------------------------------------------+------------------------------
         |          |                               | Activity        | AutoVacuumMain      |                     |             |              |                                                  | autovacuum launcher
         | postgres |                               | Activity        | LogicalLauncherMain |                     |             |              |                                                  | logical replication launcher
 test    | postgres | 2021-11-17 21:31:39.540788+00 | Client          | ClientRead          | idle in transaction |         491 |              | UPDATE test SET name = 'updated_1' WHERE id = 2; | client backend
 test    | postgres | 2021-11-17 21:31:45.625634+00 | Lock            | transactionid       | active              |         492 |          491 | UPDATE test SET name = 'updated_2' WHERE id = 2; | client backend
 test    | postgres | 2021-11-17 21:31:50.75125+00  | Lock            | tuple               | active              |         493 |          491 | UPDATE test SET name = 'updated_3' WHERE id = 2; | client backend
 test    | postgres | 2021-11-17 21:48:27.301815+00 |                 |                     | active              |             |          491 | select                                          +| client backend
         |          |                               |                 |                     |                     |             |              | datname,                                        +| 
         |          |                               |                 |                     |                     |             |              | usename,                                        +| 
         |          |                               |                 |                     |                     |             |              | xact_start,                                     +| 
         |          |                               |                 |                     |                     |             |              | wait_event_type,                                +| 
         |          |                               |                 |                     |                     |             |              | wait_event,                                     +| 
         |          |                               |                 |                     |                     |             |              | state,                                          +| 
         |          |                               |                 |                     |                     |             |              | backend_xid,                                    +| 
         |          |                               |                 |                     |                     |             |              | backend_xmin,                                   +| 
         |          |                               |                 |                     |                     |             |              | query,                                          +| 
         |          |                               |                 |                     |                     |             |              | backend_type                                    +| 
         |          |                               |                 |                     |                     |             |              | from pg_stat_activity;                           | 
         |          |                               | Activity        | BgWriterHibernate   |                     |             |              |                                                  | background writer
         |          |                               | Activity        | CheckpointerMain    |                     |             |              |                                                  | checkpointer
         |          |                               | Activity        | WalWriterMain       |                     |             |              |                                                  | walwriter
(9 rows)
```


LOG
```console
2021-11-17 21:33:29.637 UTC [20592] postgres@test LOG:  process 20592 still waiting for ShareLock on transaction 491 after 200.210 ms
2021-11-17 21:33:29.637 UTC [20592] postgres@test DETAIL:  Process holding the lock: 20590. Wait queue: 20592.
2021-11-17 21:33:29.637 UTC [20592] postgres@test CONTEXT:  while updating tuple (0,2) in relation "test"
2021-11-17 21:33:29.637 UTC [20592] postgres@test STATEMENT:  UPDATE test SET name = 'updated_2' WHERE id = 2;
2021-11-17 21:33:34.555 UTC [20593] postgres@test LOG:  process 20593 still waiting for ExclusiveLock on tuple (0,2) of relation 16385 of database 16384 after 200.223 ms
2021-11-17 21:33:34.555 UTC [20593] postgres@test DETAIL:  Process holding the lock: 20592. Wait queue: 20593.
2021-11-17 21:33:34.555 UTC [20593] postgres@test STATEMENT:  UPDATE test SET name = 'updated_3' WHERE id = 2;
2021-11-17 21:52:18.588 UTC [20592] postgres@test LOG:  process 20592 acquired ShareLock on transaction 491 after 1129150.774 ms
2021-11-17 21:52:18.588 UTC [20592] postgres@test CONTEXT:  while updating tuple (0,2) in relation "test"
2021-11-17 21:52:18.588 UTC [20592] postgres@test STATEMENT:  UPDATE test SET name = 'updated_2' WHERE id = 2;
2021-11-17 21:52:18.588 UTC [20593] postgres@test LOG:  process 20593 acquired ExclusiveLock on tuple (0,2) of relation 16385 of database 16384 after 1124233.003 ms
2021-11-17 21:52:18.588 UTC [20593] postgres@test STATEMENT:  UPDATE test SET name = 'updated_3' WHERE id = 2;
2021-11-17 21:52:18.789 UTC [20593] postgres@test LOG:  process 20593 still waiting for ShareLock on transaction 492 after 200.204 ms
2021-11-17 21:52:18.789 UTC [20593] postgres@test DETAIL:  Process holding the lock: 20592. Wait queue: 20593.
2021-11-17 21:52:18.789 UTC [20593] postgres@test CONTEXT:  while rechecking updated tuple (0,6) in relation "test"
2021-11-17 21:52:18.789 UTC [20593] postgres@test STATEMENT:  UPDATE test SET name = 'updated_3' WHERE id = 2;
2021-11-17 21:52:25.725 UTC [20593] postgres@test LOG:  process 20593 acquired ShareLock on transaction 492 after 7136.679 ms
2021-11-17 21:52:25.725 UTC [20593] postgres@test CONTEXT:  while rechecking updated tuple (0,6) in relation "test"
2021-11-17 21:52:25.725 UTC [20593] postgres@test STATEMENT:  UPDATE test SET name = 'updated_3' WHERE id = 2;
```
