<details>
<summary>Проверяем, какие роли есть в pg:</summary>
  
```sql

    postgres=# \du
                                       List of roles
     Role name |                         Attributes                         | Member of 
    -----------+------------------------------------------------------------+-----------
     postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```
  
</details>

<details>
<summary>Создаем 2 роли:</summary>
  
```sql

    CREATE ROLE role1 with LOGIN ENCRYPTED PASSWORD '1234';
    CREATE ROLE role2 with LOGIN ENCRYPTED PASSWORD '1234';
```

</details>


<details>
<summary>Проверяем роли:</summary>
  
```sql

    postgres=# \du
                                       List of roles
     Role name |                         Attributes                         | Member of 
    -----------+------------------------------------------------------------+-----------
     postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
     role1     |                                                            | {}
     role2     |                                                            | {}
    postgres=# 
```

</details>
<details>
<summary>Даем права на ДБ и таблицы(максимально):</summary>
  
```sql

    postgres=# GRANT ALL PRIVILEGES ON DATABASE postgres TO role1;
    GRANT
    postgres=# GRANT ALL PRIVILEGES ON DATABASE postgres TO role2;
    GRANT 
    postgres=# GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO role1;
    GRANT
    postgres=# GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO role2;
    GRANT
```

</details>
<details>
<summary>Создаем MV:</summary>
  
```sql

    CREATE MATERIALIZED VIEW testview AS SELECT * FROM test;
```

</details> 
<details>
<summary>Проверяем:</summary>
  
```sql

    postgres=> select * from testview;
     id | name  
    ----+-------
      1 | Petja
      2 | Vasja
    (2 rows)
```

</details>
<details>
<summary>Заходим под 2й ролью:</summary>
  
```sql

    postgres=> select * from testview;
    ERROR:  permission denied for materialized view testview
```

</details>
<details>
<summary>Выделяем права (от первой роли):</summary>
  
```sql

    postgres=> GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO role2;
    WARNING:  no privileges were granted for "test"
    GRANT
    postgres=> 
```

</details>
<details>
<summary>Проверяем (от второй роли):</summary>
  
```sql

    postgres=> select * from testview;
     id | name  
    ----+-------
      1 | Petja
      2 | Vasja
    (2 rows)
    postgres=> 
```

</details> 
<details>
<summary>INSERT из под 2й роли:</summary>
  
```sql

    postgres=> select * from testview;
     id | name  
    ----+-------
      1 | Petja
      2 | Vasja
    (2 rows)
    postgres=> insert into test values (3, 'Kolja');
    INSERT 0 1
    
    postgres=> insert into test values (3, 'Kolja');
    INSERT 0 1
    postgres=> select * from test;
     id | name  
    ----+-------
      1 | Petja
      2 | Vasja
      3 | Kolja
    (3 rows)    
```

</details>
<details>
<summary>REFRESH из под 2й роли:</summary>
  
```sql

    postgres=> REFRESH MATERIALIZED VIEW testview;
    ERROR:  must be owner of materialized view testview
    postgres=> ALTER TABLE testview OWNER TO test2;
    ERROR:  must be owner of materialized view testview
    postgres=> 
```

</details>
<details>
<summary>Создаем функцию из под 1й роли:</summary>
  
```sql
    
    CREATE OR REPLACE FUNCTION refresh_mv()
    RETURNS void
    SECURITY DEFINER
    AS $$
    BEGIN
    REFRESH MATERIALIZED VIEW testview with data;
    RETURN;
    END;
    $$ LANGUAGE plpgsql; 
```

</details>
<details>
<summary>Нарезаем права из под 1й роли:</summary>
  
```sql

    revoke all on function refresh_mv() from public;
    grant execute on function refresh_mv() to role2;
```

</details>
<details>
<summary>Выполняем REFRESH из под 2й роли:</summary>
  
```sql
    
    postgres=> select refresh_mv();
     refresh_mv 
    ------------
     
    (1 row)
    postgres=> select * from testview;
     id | name  
    ----+-------
      1 | Petja
      2 | Vasja
      3 | Kolja
    (3 rows)
    postgres=> 
```

</details>
