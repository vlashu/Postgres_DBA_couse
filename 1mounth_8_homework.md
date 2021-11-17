
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


              Таблица              |  БД  | Process ID |    Блокировка    | Блокировка получена | Блокировка по короткому пути 
-----------------------------------+------+------------+------------------+---------------------+------------------------------
 test                              | test |      20381 | RowExclusiveLock | t                   | t
 pg_class_tblspc_relfilenode_index | test |      20391 | AccessShareLock  | t                   | t
 pg_class_relname_nsp_index        | test |      20391 | AccessShareLock  | t                   | t
 pg_class_oid_index                | test |      20391 | AccessShareLock  | t                   | t
 pg_class                          | test |      20391 | AccessShareLock  | t                   | t
 pg_locks                          | test |      20391 | AccessShareLock  | t                   | t
 test                              | test |      20382 | RowExclusiveLock | t                   | t
 test                              | test |      20379 | RowExclusiveLock | t                   | t
 test                              | test |      20382 | ExclusiveLock    | f                   | f
 test                              | test |      20381 | ExclusiveLock    | t                   | f
(10 rows)
