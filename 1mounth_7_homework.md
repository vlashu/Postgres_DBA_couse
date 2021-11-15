После выполнения pg_banch хранятся 5 файлов журнала, каждый по 16МБ (80 МБ).
В среднем тест генерирует 16МБ на одну контрольную точку.

<details>
<summary>файлы WAL:</summary>

```console
postgres=# select * from pg_ls_waldir();
           name           |   size   |      modification      
--------------------------+----------+------------------------
 000000010000000000000086 | 16777216 | 2021-11-14 20:42:33+00
 000000010000000000000084 | 16777216 | 2021-11-14 20:41:34+00
 000000010000000000000082 | 16777216 | 2021-11-14 20:43:20+00
 000000010000000000000083 | 16777216 | 2021-11-14 20:42:00+00
 000000010000000000000085 | 16777216 | 2021-11-14 20:42:08+00
(5 rows)
```
</details>

> **_NOTE:_** В моем случае checkpoint выполнялся каждые 30 секунд. Все данные сбрасывались на диск до наступления следующей контрольной точки (синхронный режим)

<details>
<summary>пример лога postgres:</summary>

```console
2021-11-14 20:33:17.102 UTC [22067] LOG:  checkpoint complete: wrote 1970 buffers (12.0%); 0 WAL file(s) added, 0 removed, 1 recycled; write=14.489 s, sync=0.019 s, total=14.532 s; sync files=16, longest=0.006 s, average=0.002 s; distance=24231 kB, estimate=24231 kB
2021-11-14 20:33:32.115 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:33:47.029 UTC [22067] LOG:  checkpoint complete: wrote 2188 buffers (13.4%); 0 WAL file(s) added, 0 removed, 3 recycled; write=14.865 s, sync=0.010 s, total=14.915 s; sync files=14, longest=0.005 s, average=0.001 s; distance=38568 kB, estimate=38568 kB
2021-11-14 20:34:02.043 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:34:17.050 UTC [22067] LOG:  checkpoint complete: wrote 2155 buffers (13.2%); 0 WAL file(s) added, 0 removed, 2 recycled; write=14.971 s, sync=0.008 s, total=15.007 s; sync files=6, longest=0.005 s, average=0.002 s; distance=38715 kB, estimate=38715 kB
2021-11-14 20:34:32.063 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:34:47.057 UTC [22067] LOG:  checkpoint complete: wrote 2499 buffers (15.3%); 0 WAL file(s) added, 0 removed, 2 recycled; write=14.956 s, sync=0.010 s, total=14.994 s; sync files=14, longest=0.006 s, average=0.001 s; distance=39084 kB, estimate=39084 kB
2021-11-14 20:35:02.161 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:35:17.161 UTC [22067] LOG:  checkpoint complete: wrote 2078 buffers (12.7%); 0 WAL file(s) added, 0 removed, 2 recycled; write=14.838 s, sync=0.010 s, total=15.001 s; sync files=8, longest=0.005 s, average=0.002 s; distance=33309 kB, estimate=38506 kB
2021-11-14 20:35:32.175 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:35:47.167 UTC [22067] LOG:  checkpoint complete: wrote 2338 buffers (14.3%); 0 WAL file(s) added, 0 removed, 2 recycled; write=14.827 s, sync=0.011 s, total=14.993 s; sync files=14, longest=0.005 s, average=0.001 s; distance=25859 kB, estimate=37241 kB
2021-11-14 20:36:02.179 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:36:17.033 UTC [22067] LOG:  checkpoint complete: wrote 1976 buffers (12.1%); 0 WAL file(s) added, 0 removed, 1 recycled; write=14.824 s, sync=0.009 s, total=14.855 s; sync files=9, longest=0.004 s, average=0.001 s; distance=26072 kB, estimate=36124 kB
2021-11-14 20:36:32.161 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:36:47.034 UTC [22067] LOG:  checkpoint complete: wrote 2136 buffers (13.0%); 0 WAL file(s) added, 0 removed, 2 recycled; write=14.838 s, sync=0.007 s, total=14.873 s; sync files=15, longest=0.004 s, average=0.001 s; distance=26174 kB, estimate=35129 kB
2021-11-14 20:37:02.161 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:37:17.036 UTC [22067] LOG:  checkpoint complete: wrote 1972 buffers (12.0%); 0 WAL file(s) added, 0 removed, 2 recycled; write=14.838 s, sync=0.008 s, total=14.875 s; sync files=8, longest=0.004 s, average=0.001 s; distance=26073 kB, estimate=34224 kB
2021-11-14 20:37:32.161 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:37:47.032 UTC [22067] LOG:  checkpoint complete: wrote 2125 buffers (13.0%); 0 WAL file(s) added, 0 removed, 1 recycled; write=14.832 s, sync=0.008 s, total=14.871 s; sync files=13, longest=0.005 s, average=0.001 s; distance=26023 kB, estimate=33404 kB
2021-11-14 20:38:02.161 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:38:17.033 UTC [22067] LOG:  checkpoint complete: wrote 1967 buffers (12.0%); 0 WAL file(s) added, 0 removed, 2 recycled; write=14.837 s, sync=0.008 s, total=14.872 s; sync files=8, longest=0.004 s, average=0.001 s; distance=25844 kB, estimate=32648 kB
2021-11-14 20:38:32.161 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:38:47.035 UTC [22067] LOG:  checkpoint complete: wrote 2484 buffers (15.2%); 0 WAL file(s) added, 0 removed, 1 recycled; write=14.839 s, sync=0.010 s, total=14.875 s; sync files=14, longest=0.005 s, average=0.001 s; distance=26141 kB, estimate=31997 kB
2021-11-14 20:39:02.161 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:39:17.035 UTC [22067] LOG:  checkpoint complete: wrote 1974 buffers (12.0%); 0 WAL file(s) added, 0 removed, 2 recycled; write=14.843 s, sync=0.008 s, total=14.875 s; sync files=9, longest=0.004 s, average=0.001 s; distance=25826 kB, estimate=31380 kB
2021-11-14 20:39:32.161 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:39:47.032 UTC [22067] LOG:  checkpoint complete: wrote 2150 buffers (13.1%); 0 WAL file(s) added, 0 removed, 2 recycled; write=14.838 s, sync=0.007 s, total=14.871 s; sync files=12, longest=0.004 s, average=0.001 s; distance=26255 kB, estimate=30867 kB
2021-11-14 20:40:02.164 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:40:17.036 UTC [22067] LOG:  checkpoint complete: wrote 1983 buffers (12.1%); 0 WAL file(s) added, 0 removed, 1 recycled; write=14.837 s, sync=0.009 s, total=14.872 s; sync files=8, longest=0.005 s, average=0.002 s; distance=25935 kB, estimate=30374 kB
2021-11-14 20:40:32.179 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:40:47.034 UTC [22067] LOG:  checkpoint complete: wrote 2490 buffers (15.2%); 0 WAL file(s) added, 0 removed, 2 recycled; write=14.824 s, sync=0.008 s, total=14.855 s; sync files=14, longest=0.004 s, average=0.001 s; distance=26245 kB, estimate=29961 kB
2021-11-14 20:41:02.161 UTC [22067] LOG:  checkpoint starting: time
2021-11-14 20:41:17.031 UTC [22067] LOG:  checkpoint complete: wrote 1977 buffers (12.1%); 0 WAL file(s) added, 0 removed, 1 recycled; write=14.841 s, sync=0.009 s, total=14.871 s; sync files=8, longest=0.004 s, average=0.002 s; distance=25762 kB, estimate=29541 kB
```
</details>

> **_NOTE:_** При включении асинхронного режима tps вырос почти в 2 раза в следствии отсутствия ожидания локального сброса WAL на диск
> 
> :warning: изменение: ALTER SYSTEM SET synchronous_commit = off; 
> 
> Требуется рестарт кластера
> 
> :warning: просмотр: show synchronous_commit;

<details>
<summary>pg_banch синхронно:</summary>

```console
starting vacuum...end.
progress: 10.0 s, 710.2 tps, lat 11.197 ms stddev 8.366
progress: 20.0 s, 716.8 tps, lat 11.158 ms stddev 7.935
progress: 30.0 s, 708.9 tps, lat 11.276 ms stddev 8.193
progress: 40.0 s, 720.8 tps, lat 11.111 ms stddev 7.751
progress: 50.0 s, 734.6 tps, lat 10.887 ms stddev 7.375
progress: 60.0 s, 702.2 tps, lat 11.393 ms stddev 7.648
progress: 70.0 s, 729.7 tps, lat 10.956 ms stddev 7.262
progress: 80.0 s, 702.9 tps, lat 11.382 ms stddev 7.663
progress: 90.0 s, 691.7 tps, lat 11.569 ms stddev 7.672
progress: 100.0 s, 716.5 tps, lat 11.164 ms stddev 7.183
progress: 110.0 s, 701.0 tps, lat 11.406 ms stddev 7.199
progress: 120.0 s, 686.0 tps, lat 11.659 ms stddev 7.389
progress: 130.0 s, 711.6 tps, lat 11.247 ms stddev 7.013
progress: 140.0 s, 717.6 tps, lat 11.147 ms stddev 6.866
progress: 150.0 s, 671.5 tps, lat 11.909 ms stddev 7.546
progress: 160.0 s, 708.4 tps, lat 11.295 ms stddev 6.680
progress: 170.0 s, 710.5 tps, lat 11.259 ms stddev 6.883
progress: 180.0 s, 695.8 tps, lat 11.495 ms stddev 7.030
progress: 190.0 s, 695.3 tps, lat 11.504 ms stddev 6.305
progress: 200.0 s, 713.4 tps, lat 11.215 ms stddev 7.896
progress: 210.0 s, 697.9 tps, lat 11.461 ms stddev 8.303
progress: 220.0 s, 709.0 tps, lat 11.282 ms stddev 8.147
progress: 230.0 s, 717.4 tps, lat 11.149 ms stddev 8.139
progress: 240.0 s, 706.3 tps, lat 11.325 ms stddev 8.322
progress: 250.0 s, 714.8 tps, lat 11.189 ms stddev 8.227
progress: 260.0 s, 718.7 tps, lat 11.132 ms stddev 8.277
progress: 270.0 s, 701.2 tps, lat 11.406 ms stddev 8.666
progress: 280.0 s, 687.5 tps, lat 11.628 ms stddev 8.898
progress: 290.0 s, 648.8 tps, lat 12.334 ms stddev 9.409
progress: 300.0 s, 654.3 tps, lat 12.227 ms stddev 9.069
progress: 310.0 s, 720.7 tps, lat 11.101 ms stddev 8.070
progress: 320.0 s, 726.9 tps, lat 11.002 ms stddev 8.125
progress: 330.0 s, 708.4 tps, lat 11.295 ms stddev 8.288
progress: 340.0 s, 718.7 tps, lat 11.130 ms stddev 7.887
progress: 350.0 s, 716.8 tps, lat 11.159 ms stddev 7.560
progress: 360.0 s, 711.2 tps, lat 11.248 ms stddev 7.690
progress: 370.0 s, 721.1 tps, lat 11.090 ms stddev 7.666
progress: 380.0 s, 732.8 tps, lat 10.918 ms stddev 7.209
progress: 390.0 s, 719.1 tps, lat 11.126 ms stddev 7.610
progress: 400.0 s, 727.4 tps, lat 10.992 ms stddev 7.306
progress: 410.0 s, 728.9 tps, lat 10.977 ms stddev 7.303
progress: 420.0 s, 710.3 tps, lat 11.263 ms stddev 7.242
progress: 430.0 s, 708.6 tps, lat 11.247 ms stddev 8.035
progress: 440.0 s, 480.7 tps, lat 16.636 ms stddev 23.234
progress: 450.0 s, 465.3 tps, lat 17.207 ms stddev 24.080
progress: 460.0 s, 470.3 tps, lat 16.996 ms stddev 23.815
progress: 470.0 s, 488.4 tps, lat 16.367 ms stddev 23.170
progress: 480.0 s, 462.1 tps, lat 17.307 ms stddev 24.562
progress: 490.0 s, 456.5 tps, lat 17.549 ms stddev 25.135
progress: 500.0 s, 469.3 tps, lat 17.024 ms stddev 24.764
progress: 510.0 s, 457.9 tps, lat 17.469 ms stddev 25.155
progress: 520.0 s, 456.9 tps, lat 17.513 ms stddev 25.037
progress: 530.0 s, 459.6 tps, lat 17.376 ms stddev 25.287
progress: 540.0 s, 454.3 tps, lat 17.632 ms stddev 24.947
progress: 550.0 s, 467.6 tps, lat 17.109 ms stddev 25.115
progress: 560.0 s, 459.6 tps, lat 17.394 ms stddev 24.539
progress: 570.0 s, 454.6 tps, lat 17.602 ms stddev 25.844
progress: 580.0 s, 467.8 tps, lat 17.107 ms stddev 25.036
progress: 590.0 s, 460.0 tps, lat 17.408 ms stddev 24.671
progress: 600.0 s, 444.7 tps, lat 17.964 ms stddev 24.709
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 1
query mode: simple
number of clients: 8
number of threads: 1
duration: 600 s
number of transactions actually processed: 383286
latency average = 12.521 ms
latency stddev = 13.372 ms
tps = 638.783381 (including connections establishing)
tps = 638.789998 (excluding connections establishing)
```
</details>

<details>
<summary>pg_banch асинхронно:</summary>

```console
starting vacuum...end.
progress: 10.0 s, 1745.2 tps, lat 4.571 ms stddev 1.417
progress: 20.0 s, 1770.4 tps, lat 4.518 ms stddev 1.402
progress: 30.0 s, 1771.1 tps, lat 4.516 ms stddev 1.374
progress: 40.0 s, 1785.0 tps, lat 4.481 ms stddev 1.359
progress: 50.0 s, 1734.8 tps, lat 4.611 ms stddev 1.493
progress: 60.0 s, 1756.5 tps, lat 4.554 ms stddev 1.451
progress: 70.0 s, 1764.0 tps, lat 4.534 ms stddev 1.369
progress: 80.0 s, 1732.4 tps, lat 4.617 ms stddev 1.454
progress: 90.0 s, 1760.8 tps, lat 4.542 ms stddev 1.453
progress: 100.0 s, 1763.5 tps, lat 4.536 ms stddev 1.427
progress: 110.0 s, 1729.0 tps, lat 4.626 ms stddev 1.529
progress: 120.0 s, 1762.0 tps, lat 4.540 ms stddev 1.404
progress: 130.0 s, 894.9 tps, lat 8.939 ms stddev 23.860
progress: 140.0 s, 877.5 tps, lat 9.115 ms stddev 24.237
progress: 150.0 s, 886.3 tps, lat 9.026 ms stddev 24.079
progress: 160.0 s, 880.8 tps, lat 9.081 ms stddev 24.059
progress: 170.0 s, 873.8 tps, lat 9.156 ms stddev 24.172
progress: 180.0 s, 886.0 tps, lat 9.000 ms stddev 24.133
progress: 190.0 s, 855.4 tps, lat 9.351 ms stddev 24.428
progress: 200.0 s, 859.1 tps, lat 9.311 ms stddev 24.400
progress: 210.0 s, 893.1 tps, lat 8.957 ms stddev 23.917
progress: 220.0 s, 879.1 tps, lat 9.099 ms stddev 24.094
progress: 230.0 s, 860.3 tps, lat 9.298 ms stddev 24.326
progress: 240.0 s, 870.8 tps, lat 9.186 ms stddev 24.272
progress: 250.0 s, 892.4 tps, lat 8.962 ms stddev 24.001
progress: 260.0 s, 866.2 tps, lat 9.236 ms stddev 24.630
progress: 270.0 s, 877.4 tps, lat 9.116 ms stddev 24.310
progress: 280.0 s, 873.8 tps, lat 9.154 ms stddev 24.232
progress: 290.0 s, 857.2 tps, lat 9.332 ms stddev 24.532
progress: 300.0 s, 881.0 tps, lat 9.080 ms stddev 24.030
progress: 310.0 s, 868.2 tps, lat 9.214 ms stddev 24.213
progress: 320.0 s, 862.0 tps, lat 9.280 ms stddev 24.555
progress: 330.0 s, 897.0 tps, lat 8.918 ms stddev 24.112
progress: 340.0 s, 885.4 tps, lat 9.034 ms stddev 24.119
progress: 350.0 s, 872.3 tps, lat 9.156 ms stddev 24.208
progress: 360.0 s, 860.7 tps, lat 9.293 ms stddev 24.775
progress: 370.0 s, 898.5 tps, lat 8.903 ms stddev 23.915
progress: 380.0 s, 884.5 tps, lat 9.044 ms stddev 24.008
progress: 390.0 s, 882.2 tps, lat 9.067 ms stddev 24.062
progress: 400.0 s, 877.7 tps, lat 9.113 ms stddev 24.155
progress: 410.0 s, 870.9 tps, lat 9.185 ms stddev 24.430
progress: 420.0 s, 876.5 tps, lat 9.126 ms stddev 24.489
progress: 430.0 s, 873.9 tps, lat 9.154 ms stddev 24.155
progress: 440.0 s, 872.8 tps, lat 9.151 ms stddev 24.120
progress: 450.0 s, 888.0 tps, lat 9.009 ms stddev 24.148
progress: 460.0 s, 883.2 tps, lat 9.056 ms stddev 24.009
progress: 470.0 s, 889.8 tps, lat 8.990 ms stddev 24.313
progress: 480.0 s, 896.2 tps, lat 8.925 ms stddev 23.951
progress: 490.0 s, 895.7 tps, lat 8.930 ms stddev 24.043
progress: 500.0 s, 890.2 tps, lat 8.987 ms stddev 24.009
progress: 510.0 s, 891.0 tps, lat 8.978 ms stddev 23.964
progress: 520.0 s, 892.7 tps, lat 8.961 ms stddev 24.000
progress: 530.0 s, 869.9 tps, lat 9.195 ms stddev 24.420
progress: 540.0 s, 916.1 tps, lat 8.732 ms stddev 23.792
progress: 550.0 s, 903.8 tps, lat 8.851 ms stddev 23.774
progress: 560.0 s, 877.2 tps, lat 9.118 ms stddev 24.217
progress: 570.0 s, 894.8 tps, lat 8.940 ms stddev 23.908
progress: 580.0 s, 889.0 tps, lat 8.985 ms stddev 23.956
progress: 590.0 s, 868.5 tps, lat 9.210 ms stddev 24.319
progress: 600.0 s, 893.4 tps, lat 8.939 ms stddev 23.933
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 1
query mode: simple
number of clients: 8
number of threads: 1
duration: 600 s
number of transactions actually processed: 633627
latency average = 7.573 ms
latency stddev = 19.870 ms
tps = 1056.005230 (including connections establishing)
```
</details>




#### Включение контрольных сумм на кластере:

    postgres=# show data_checksums;
     data_checksums 
    ----------------
     off
    (1 row)
    
    user@host:/$ sudo service postgresql stop
    
    user@host:/$ sudo /usr/lib/postgresql/13/bin/pg_checksums -e --pgdata='/var/lib/postgresql/13/main'
    Checksum operation completed
    Files scanned:  931
    Blocks scanned: 9123
    pg_checksums: syncing data directory
    pg_checksums: updating control file
    Checksums enabled in cluster
    
    user@host:/$ sudo service postgresql start
    
    user@host:/$ sudo -u postgres psql
    
    postgres=# show data_checksums;
     data_checksums 
    ----------------
     on
    (1 row)
    postgres=# 



Создание таблицы с наполнением

    postgres=# create table test2 (test integer);
    \CREATE TABLE
    postgres=# insert into test2 values (1),(2),(3);
    INSERT 0 3
    postgres=# select * from test2;
     test 
    ----
      1
      2
      3
    (3 rows)
    postgres=# 

Запрос данных

    postgres=# select * from test2;
    WARNING:  page verification failed, calculated checksum 32801 but expected 28563
    ERROR:  invalid page in block 0 of relation base/13414/16444
    postgres=# 

Выключение проверки контрольных сумм:
> **_NOTE:_** Данные доступны не в полном объеме 
  
    postgres=# show ignore_checksum_failure
    ;
     ignore_checksum_failure 
    -------------------------
     off
    (1 row)
    postgres=# set ignore_checksum_failure = on
    ;
    SET
    postgres=# show ignore_checksum_failure
    ;
     ignore_checksum_failure 
    -------------------------
     on
    (1 row)
    postgres=# select * from test2;
    WARNING:  page verification failed, calculated checksum 32801 but expected 28563
     test 
    ------
        2
        3
    (2 rows)
    postgres=# 
