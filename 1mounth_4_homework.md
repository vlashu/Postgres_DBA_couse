#### ЛОКАЛЬНОЕ ПОДКЛЮЧЕНИЕ - УСТАНОВКА DOCKER:

        ssh_gcp:~$ sudo sh get-docker.sh
        # Executing docker install script, commit: 93d2499759296ac1f9c510605fef85052a2c32be
        + sh -c apt-get update -qq >/dev/null
        + sh -c DEBIAN_FRONTEND=noninteractive apt-get install -y -qq apt-transport-https ca-certificates curl >/dev/null
        + sh -c curl -fsSL "https://download.docker.com/linux/ubuntu/gpg" | gpg --dearmor --yes -o /usr/share/keyrings/docker-archive-keyring.gpg
        + sh -c echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu focal stable" > /etc/apt/sources.list.d/docker.list
        + sh -c apt-get update -qq >/dev/null
        + sh -c DEBIAN_FRONTEND=noninteractive apt-get install -y -qq --no-install-recommends  docker-ce-cli docker-scan-plugin docker-ce >/dev/null
        + version_gte 20.10
        + [ -z  ]
        + return 0
        + sh -c DEBIAN_FRONTEND=noninteractive apt-get install -y -qq docker-ce-rootless-extras >/dev/null
        + sh -c docker version
        Client: Docker Engine - Community
         Version:           20.10.10
         API version:       1.41
         Go version:        go1.16.9
         Git commit:        b485636
         Built:             Mon Oct 25 07:42:59 2021
         OS/Arch:           linux/amd64
         Context:           default
         Experimental:      true

        Server: Docker Engine - Community
         Engine:
          Version:          20.10.10
          API version:      1.41 (minimum version 1.12)
          Go version:       go1.16.9
          Git commit:       e2f740d
          Built:            Mon Oct 25 07:41:08 2021
          OS/Arch:          linux/amd64
          Experimental:     false
         containerd:
          Version:          1.4.11
          GitCommit:        5b46e404f6b9f661a205e28d59c982d3634148f8
         runc:
          Version:          1.0.2
          GitCommit:        v1.0.2-0-g52b36a2
         docker-init:
          Version:          0.19.0
          GitCommit:        de40ad0

        ================================================================================

        To run Docker as a non-privileged user, consider setting up the
        Docker daemon in rootless mode for your user:

            dockerd-rootless-setuptool.sh install

        Visit https://docs.docker.com/go/rootless/ to learn about rootless mode.


        To run the Docker daemon as a fully privileged service, but granting non-root
        users access, refer to https://docs.docker.com/go/daemon-access/

        WARNING: Access to the remote API on a privileged Docker daemon is equivalent
                 to root access on the host. Refer to the 'Docker daemon attack surface'
                 documentation for details: https://docs.docker.com/go/attack-surface/

        ================================================================================

        ssh_gcp:~$ sudo docker network create pg-net
        2f1b0138003bb52867b1a18bc3265e3e4280340cc388b275ec10261423f186bb

        ssh_gcp:~$ sudo docker run --name pg-docker --network pg-net -e POSTGRES_PASSWORD=postgres -d -p 5432:5432 -v /var/lib/postgres:/var/lib/postgresql/data postgres:13
        Unable to find image 'postgres:13' locally
        13: Pulling from library/postgres
        7d63c13d9b9b: Pull complete 
        cad0f9d5f5fe: Pull complete 
        ff74a7a559cb: Pull complete 
        c43dfd845683: Pull complete 
        e554331369f5: Pull complete 
        d25d54a3ac3a: Pull complete 
        bbc6df00588c: Pull complete 
        d4deb2e86480: Pull complete 
        d4132927c0d9: Pull complete 
        3d03efa70ed1: Pull complete 
        645312b7d892: Pull complete 
        3cc7074f2000: Pull complete 
        4e6d0469c332: Pull complete 
        Digest: sha256:1adb50e5c24f550a9e68457a2ce60e9e4103dfc43c3b36e98310168165b443a1
        Status: Downloaded newer image for postgres:13
        10df41bb23e5c532a5fc24757005db366331c037b9ac4560ff18daaa671a2c02

#### КОНТЕЙНЕР С КЛИЕНТОМ - СОЗДАНИЕ ТЕСТОВОЙ ТАБЛИЦЫ С ДАННЫМИ ИЗ КОНТЕЙНЕРА-КЛИЕНТА:

        ssh_gcp:~$ sudo docker run -it --rm --network pg-net --name pg-client postgres:13 psql -h pg-docker -U postgres

        psql (13.4 (Debian 13.4-4.pgdg110+1))
        Type "help" for help.
        postgres=# create table test (id int, name varchar);
        CREATE TABLE
        postgres=# insert into test (id, name) values (1,'Petja'),(2, 'Vasja');
        INSERT 0 2
        postgres=# select * from test
        postgres-# ;
         id | name  
        ----+-------
          1 | Petja
          2 | Vasja
        (2 rows)
        postgres=# 

#### ЛОКАЛЬНОЕ ПОДКЛЮЧЕНИЕ - ПРОВЕРКА ДОСТУПНОСТИ ВНЕ КОНТЕЙНЕРА:

        ssh_gcp:~$ psql -p 5432 -h localhost -U postgres -W -d postgres
        Password: 
        psql (13.4 (Ubuntu 13.4-4.pgdg20.04+1))
        Type "help" for help.
        postgres=# select * from test;
         id | name  
        ----+-------
          1 | Petja
          2 | Vasja
        (2 rows)
        postgres=# 

#### УДАЛЕННОЕ ПОДКЛЮЧЕНИЕ - ПОПЫТКА ПОДКЛЮЧЕНИЯ ИЗ ВНЕ:

        my_pc:/mnt/c/Users/Work$ psql -p 5432 -U postgres -h 34.83.255.24 -d postgres -W
        Password:
        psql: error: connection to server at "34.83.255.24", port 5432 failed: Connection timed out
                Is the server running on that host and accepting TCP/IP connections?

#### ЛОКАЛЬНОЕ ПОДКЛЮЧЕНИЕ - ПРОВЕРКА ДОСТУПНОСТИ ВНЕ КОНТЕЙНЕРА:

        ssh_gcp:~$ psql -p 5432 -h localhost -U postgres -W -d postgres
        Password: 
        psql (13.4 (Ubuntu 13.4-4.pgdg20.04+1))
        Type "help" for help.
        postgres=# select * from test;
         id | name  
        ----+-------
          1 | Petja
          2 | Vasja
        (2 rows)
        postgres=# 
     
#### ДЕЙСТВИЯ:

        VPC network > Firewall > default-allow-internal = 0.0.0.0/0  (Убираю огранечение доступа: всем на все порты)

#### УДАЛЕННОЕ ПОДКЛЮЧЕНИЕ - ПОПЫТКА ПОДКЛЮЧЕНИЯ ИЗ ВНЕ №2:        
        
        my_pc:/mnt/c/Users/Work$ psql -p 5432 -U postgres -h 34.83.255.24 -d postgres -W
        Password:
        psql (13.4 (Ubuntu 13.4-4.pgdg20.04+1))
        Type "help" for help.

        postgres=# select * from test; 
         id | name
        ----+-------
          1 | Petja
          2 | Vasja
        (2 rows)


#### ЛОКАЛЬНОЕ ПОДКЛЮЧЕНИЕ - УДАЛЕНИЕ КОНТЕЙНЕРА С POSTGRESQL:

        ssh_gcp:~$ sudo docker ps
        CONTAINER ID   IMAGE         COMMAND                  CREATED        STATUS        PORTS                                       NAMES
        10df41bb23e5   postgres:13   "docker-entrypoint.s…"   16 hours ago   Up 16 hours   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   pg-doc
        ker
        ssh_gcp:~$ sudo docker stop 10df41bb23e5
        10df41bb23e5
        ssh_gcp:~$ sudo docker ps
        CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
        ssh_gcp:~$ sudo docker rm 10df41bb23e5
        10df41bb23e5


#### УДАЛЕННОЕ ПОДКЛЮЧЕНИЕ - ПРОВЕРКА, ЧТО БЕДЕТ ПРИ ОТКРЫТОЙ СЕССИИ И УДАЛЕННОМ КОНТЕЙНЕРЕ:

        postgres=# select * from test;
        FATAL:  terminating connection due to administrator command
        server closed the connection unexpectedly
                This probably means the server terminated abnormally
                before or while processing the request.
        The connection to the server was lost. Attempting reset: Failed.
        !?>


#### ЛОКАЛЬНОЕ ПОДКЛЮЧЕНИЕ - СОЗДАНИЕ НОВОГО КОНТЕЙНЕРА С POSTGRESQL (имя pg-docker-2):

        ssh_gcp:~$ sudo docker run --name pg-docker-2 --network pg-net -e POSTGRES_PASSWORD=postgres -d -p 5432:5432 -v /var/lib/postgres:/var/lib/postgresql/data postgres:
        13
        16fadc30fb7157ef00c9a11082fd8b8e35aa9ab7a6e1d2eef3c354b80c260c38
        
#### КОНТЕЙНЕР КЛИЕНТ - ДАННЫЕ ДОСТУПНЫ:

        ssh_gcp:~$ sudo docker run -it --rm --network pg-net --name pg-client postgres:13 psql -h pg-docker -U postgres
        Password for user postgres: 
        psql (13.4 (Debian 13.4-4.pgdg110+1))
        Type "help" for help.
        postgres=# select * from test;
         id | name  
        ----+-------
          1 | Petja
          2 | Vasja
        (2 rows)
        postgres=# 
        Page down

#### УДАЛЕННОЕ ПОДКЛЮЧЕНИЕ - ДАННЫЕ ДОСТУПНЫ:

        my_pc:/mnt/c/Users/Work$ psql -p 5432 -U postgres -h 34.83.255.24 -d postgres -W
        Password:
        psql (13.4 (Ubuntu 13.4-4.pgdg20.04+1))
        Type "help" for help.

        postgres=# select * from test;
         id | name
        ----+-------
          1 | Petja
          2 | Vasja
        (2 rows)

        postgres=#
