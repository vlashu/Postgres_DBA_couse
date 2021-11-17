
> :warning: запрос для удобства мониторинга
>```sql
>select 
>    pgclass.relname as "Таблица",
>    pdb.datname as "БД",
>    pg_locks.pid as "Process ID",
>    pg_locks.mode as "Блокировка",
>    pg_locks.granted as "Блокировка получена",
>    pg_locks.fastpath as "Блокировка по короткому пути"
>from 
>    pg_locks
>join pg_database as pdb on pg_locks.database = pdb.oid
>join pg_class as pgclass on pg_locks.relation = pgclass.oid
>;
>```

