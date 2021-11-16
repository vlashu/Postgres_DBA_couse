> **_NOTE:_** Все параметры менялись в /etc/postgresql/13/main/postgresql.conf

> :warning: запуск: sudo service postgresql restart&&sudo -u postgres psql -c "select name as \"Параметр\", setting as \"Значение\", short_desc  as \"Описание\" from pg_settings where name like '%autovacuum%';"&&pgbench -c8 -P 10 -T 600 -U postgres p
ostgres

### Стандартные параметры:

<details>
<summary>Сет параметров:</summary>

```console
Параметр                | Значение  |                                         Описание                                          
---------------------------------------+-----------+-------------------------------------------------------------------------------------------
 autovacuum                            | on        | Starts the autovacuum subprocess.
 autovacuum_analyze_scale_factor       | 0.1       | Number of tuple inserts, updates, or deletes prior to analyze as a fraction of reltuples.
 autovacuum_analyze_threshold          | 50        | Minimum number of tuple inserts, updates, or deletes prior to analyze.
 autovacuum_freeze_max_age             | 200000000 | Age at which to autovacuum a table to prevent transaction ID wraparound.
 autovacuum_max_workers                | 3         | Sets the maximum number of simultaneously running autovacuum worker processes.
 autovacuum_multixact_freeze_max_age   | 400000000 | Multixact age at which to autovacuum a table to prevent multixact wraparound.
 autovacuum_naptime                    | 60        | Time to sleep between autovacuum runs.
 autovacuum_vacuum_cost_delay          | 2         | Vacuum cost delay in milliseconds, for autovacuum.
 autovacuum_vacuum_cost_limit          | -1        | Vacuum cost amount available before napping, for autovacuum.
 autovacuum_vacuum_insert_scale_factor | 0.2       | Number of tuple inserts prior to vacuum as a fraction of reltuples.
 autovacuum_vacuum_insert_threshold    | 1000      | Minimum number of tuple inserts prior to vacuum, or -1 to disable insert vacuums.
 autovacuum_vacuum_scale_factor        | 0.2       | Number of tuple updates or deletes prior to vacuum as a fraction of reltuples.
 autovacuum_vacuum_threshold           | 50        | Minimum number of tuple updates or deletes prior to vacuum.
 autovacuum_work_mem                   | -1        | Sets the maximum memory to be used by each autovacuum worker process.
 log_autovacuum_min_duration           | -1        | Sets the minimum execution time above which autovacuum actions will be logged.
(15 rows)
```
</details>


<details>
<summary>Выполнение pg_banch:</summary>

```console
starting vacuum...end.
progress: 10.0 s, 888.0 tps, lat 8.979 ms stddev 6.720
progress: 20.0 s, 901.4 tps, lat 8.872 ms stddev 6.907
progress: 30.0 s, 895.1 tps, lat 8.936 ms stddev 6.959
progress: 40.0 s, 897.9 tps, lat 8.912 ms stddev 6.604
progress: 50.0 s, 907.6 tps, lat 8.812 ms stddev 6.629
progress: 60.0 s, 899.8 tps, lat 8.891 ms stddev 6.771
progress: 70.0 s, 897.5 tps, lat 8.913 ms stddev 6.460
progress: 80.0 s, 894.8 tps, lat 8.937 ms stddev 6.490
progress: 90.0 s, 872.0 tps, lat 9.175 ms stddev 6.573
progress: 100.0 s, 880.9 tps, lat 9.076 ms stddev 6.506
progress: 110.0 s, 861.4 tps, lat 9.289 ms stddev 6.157
progress: 120.0 s, 889.0 tps, lat 8.997 ms stddev 6.086
progress: 130.0 s, 900.7 tps, lat 8.880 ms stddev 6.191
progress: 140.0 s, 894.6 tps, lat 8.947 ms stddev 6.009
progress: 150.0 s, 888.2 tps, lat 9.006 ms stddev 6.054
progress: 160.0 s, 910.9 tps, lat 8.783 ms stddev 5.899
progress: 170.0 s, 896.5 tps, lat 8.923 ms stddev 6.161
progress: 180.0 s, 874.0 tps, lat 9.152 ms stddev 6.617
progress: 190.0 s, 832.7 tps, lat 9.603 ms stddev 7.201
progress: 200.0 s, 902.2 tps, lat 8.871 ms stddev 6.118
progress: 210.0 s, 906.8 tps, lat 8.821 ms stddev 5.692
progress: 220.0 s, 904.7 tps, lat 8.840 ms stddev 5.542
progress: 230.0 s, 882.1 tps, lat 9.066 ms stddev 6.170
progress: 240.0 s, 925.5 tps, lat 8.646 ms stddev 6.905
progress: 250.0 s, 915.0 tps, lat 8.744 ms stddev 5.575
progress: 260.0 s, 900.1 tps, lat 8.878 ms stddev 5.891
progress: 270.0 s, 903.7 tps, lat 8.860 ms stddev 7.179
progress: 280.0 s, 896.1 tps, lat 8.926 ms stddev 7.174
progress: 290.0 s, 899.3 tps, lat 8.895 ms stddev 6.998
progress: 300.0 s, 897.8 tps, lat 8.911 ms stddev 7.285
progress: 310.0 s, 888.9 tps, lat 8.998 ms stddev 7.069
progress: 320.0 s, 882.4 tps, lat 9.067 ms stddev 7.269
progress: 330.0 s, 881.8 tps, lat 9.069 ms stddev 7.249
progress: 340.0 s, 897.1 tps, lat 8.920 ms stddev 7.017
progress: 350.0 s, 774.5 tps, lat 10.327 ms stddev 14.143
progress: 360.0 s, 538.4 tps, lat 14.858 ms stddev 26.243
progress: 370.0 s, 563.4 tps, lat 14.196 ms stddev 23.908
progress: 380.0 s, 561.8 tps, lat 14.238 ms stddev 23.549
progress: 390.0 s, 558.3 tps, lat 14.315 ms stddev 24.653
progress: 400.0 s, 566.2 tps, lat 14.122 ms stddev 23.979
progress: 410.0 s, 563.4 tps, lat 14.202 ms stddev 23.965
progress: 420.0 s, 531.4 tps, lat 15.055 ms stddev 26.201
progress: 430.0 s, 564.7 tps, lat 14.165 ms stddev 24.264
progress: 440.0 s, 568.5 tps, lat 14.066 ms stddev 24.775
progress: 450.0 s, 564.5 tps, lat 14.177 ms stddev 23.445
progress: 460.0 s, 568.0 tps, lat 14.083 ms stddev 23.514
progress: 470.0 s, 569.4 tps, lat 14.048 ms stddev 23.247
progress: 480.0 s, 574.0 tps, lat 13.930 ms stddev 24.690
progress: 490.0 s, 551.5 tps, lat 14.506 ms stddev 23.422
progress: 500.0 s, 536.1 tps, lat 14.925 ms stddev 24.115
progress: 510.0 s, 570.4 tps, lat 14.026 ms stddev 22.907
progress: 520.0 s, 561.7 tps, lat 14.241 ms stddev 23.045
progress: 530.0 s, 562.3 tps, lat 14.211 ms stddev 23.130
progress: 540.0 s, 544.5 tps, lat 14.693 ms stddev 25.696
progress: 550.0 s, 566.4 tps, lat 14.120 ms stddev 23.622
progress: 560.0 s, 573.3 tps, lat 13.957 ms stddev 22.840
progress: 570.0 s, 571.3 tps, lat 14.001 ms stddev 23.078
progress: 580.0 s, 565.1 tps, lat 14.148 ms stddev 23.409
progress: 590.0 s, 564.8 tps, lat 14.170 ms stddev 23.689
progress: 600.0 s, 551.9 tps, lat 14.491 ms stddev 24.014
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 1
query mode: simple
number of clients: 8
number of threads: 1
duration: 600 s
number of transactions actually processed: 451531
latency average = 10.629 ms
latency stddev = 14.724 ms
tps = 752.528022 (including connections establishing)
tps = 752.532201 (excluding connections establishing)
```
</details>

### Autovacuum отключен:
  
<details>
<summary>Сет параметров:</summary>

```console
               Параметр                | Значение  |                                         Описание                                          
---------------------------------------+-----------+-------------------------------------------------------------------------------------------
 autovacuum                            | off       | Starts the autovacuum subprocess.
 autovacuum_analyze_scale_factor       | 0.1       | Number of tuple inserts, updates, or deletes prior to analyze as a fraction of reltuples.
 autovacuum_analyze_threshold          | 50        | Minimum number of tuple inserts, updates, or deletes prior to analyze.
 autovacuum_freeze_max_age             | 200000000 | Age at which to autovacuum a table to prevent transaction ID wraparound.
 autovacuum_max_workers                | 3         | Sets the maximum number of simultaneously running autovacuum worker processes.
 autovacuum_multixact_freeze_max_age   | 400000000 | Multixact age at which to autovacuum a table to prevent multixact wraparound.
 autovacuum_naptime                    | 60        | Time to sleep between autovacuum runs.
 autovacuum_vacuum_cost_delay          | 2         | Vacuum cost delay in milliseconds, for autovacuum.
 autovacuum_vacuum_cost_limit          | -1        | Vacuum cost amount available before napping, for autovacuum.
 autovacuum_vacuum_insert_scale_factor | 0.2       | Number of tuple inserts prior to vacuum as a fraction of reltuples.
 autovacuum_vacuum_insert_threshold    | 1000      | Minimum number of tuple inserts prior to vacuum, or -1 to disable insert vacuums.
 autovacuum_vacuum_scale_factor        | 0.2       | Number of tuple updates or deletes prior to vacuum as a fraction of reltuples.
 autovacuum_vacuum_threshold           | 50        | Minimum number of tuple updates or deletes prior to vacuum.
 autovacuum_work_mem                   | -1        | Sets the maximum memory to be used by each autovacuum worker process.
 log_autovacuum_min_duration           | -1        | Sets the minimum execution time above which autovacuum actions will be logged.
(15 rows)
```
</details>

<details>
<summary>Выполнение pg_banch:</summary>

```console
starting vacuum...end.
progress: 10.0 s, 893.1 tps, lat 8.929 ms stddev 6.901
progress: 20.0 s, 912.6 tps, lat 8.762 ms stddev 6.627
progress: 30.0 s, 908.8 tps, lat 8.803 ms stddev 6.825
progress: 40.0 s, 908.9 tps, lat 8.803 ms stddev 6.599
progress: 50.0 s, 921.3 tps, lat 8.682 ms stddev 6.485
progress: 60.0 s, 910.5 tps, lat 8.785 ms stddev 6.683
progress: 70.0 s, 896.2 tps, lat 8.929 ms stddev 6.690
progress: 80.0 s, 881.0 tps, lat 9.075 ms stddev 6.590
progress: 90.0 s, 876.0 tps, lat 9.134 ms stddev 6.870
progress: 100.0 s, 911.3 tps, lat 8.779 ms stddev 6.224
progress: 110.0 s, 909.1 tps, lat 8.796 ms stddev 6.469
progress: 120.0 s, 922.4 tps, lat 8.675 ms stddev 6.165
progress: 130.0 s, 916.5 tps, lat 8.728 ms stddev 6.275
progress: 140.0 s, 909.9 tps, lat 8.790 ms stddev 6.142
progress: 150.0 s, 921.9 tps, lat 8.679 ms stddev 6.088
progress: 160.0 s, 908.3 tps, lat 8.803 ms stddev 6.192
progress: 170.0 s, 912.9 tps, lat 8.765 ms stddev 6.345
progress: 180.0 s, 926.0 tps, lat 8.640 ms stddev 5.964
progress: 190.0 s, 908.2 tps, lat 8.807 ms stddev 5.889
progress: 200.0 s, 918.5 tps, lat 8.709 ms stddev 6.200
progress: 210.0 s, 921.9 tps, lat 8.675 ms stddev 6.085
progress: 220.0 s, 891.1 tps, lat 8.979 ms stddev 6.095
progress: 230.0 s, 918.0 tps, lat 8.711 ms stddev 6.373
progress: 240.0 s, 897.9 tps, lat 8.910 ms stddev 6.949
progress: 250.0 s, 894.3 tps, lat 8.945 ms stddev 6.666
progress: 260.0 s, 873.1 tps, lat 9.160 ms stddev 7.102
progress: 270.0 s, 887.0 tps, lat 9.017 ms stddev 6.520
progress: 280.0 s, 885.1 tps, lat 9.041 ms stddev 6.976
progress: 290.0 s, 888.0 tps, lat 9.005 ms stddev 7.118
progress: 300.0 s, 913.9 tps, lat 8.756 ms stddev 6.941
progress: 310.0 s, 908.2 tps, lat 8.809 ms stddev 6.996
progress: 320.0 s, 911.8 tps, lat 8.772 ms stddev 7.041
progress: 330.0 s, 920.4 tps, lat 8.690 ms stddev 7.155
progress: 340.0 s, 914.3 tps, lat 8.746 ms stddev 6.989
progress: 350.0 s, 614.8 tps, lat 13.022 ms stddev 21.643
progress: 360.0 s, 572.1 tps, lat 13.980 ms stddev 23.556
progress: 370.0 s, 567.6 tps, lat 14.093 ms stddev 23.541
progress: 380.0 s, 579.5 tps, lat 13.802 ms stddev 23.541
progress: 390.0 s, 555.7 tps, lat 14.388 ms stddev 23.199
progress: 400.0 s, 553.4 tps, lat 14.462 ms stddev 23.642
progress: 410.0 s, 579.0 tps, lat 13.815 ms stddev 22.990
progress: 420.0 s, 589.4 tps, lat 13.565 ms stddev 22.764
progress: 430.0 s, 584.0 tps, lat 13.706 ms stddev 23.203
progress: 440.0 s, 582.6 tps, lat 13.726 ms stddev 23.026
progress: 450.0 s, 579.0 tps, lat 13.819 ms stddev 23.361
progress: 460.0 s, 578.2 tps, lat 13.822 ms stddev 23.041
progress: 470.0 s, 590.1 tps, lat 13.559 ms stddev 22.579
progress: 480.0 s, 582.9 tps, lat 13.720 ms stddev 22.753
progress: 490.0 s, 580.6 tps, lat 13.776 ms stddev 22.643
progress: 500.0 s, 581.6 tps, lat 13.754 ms stddev 22.872
progress: 510.0 s, 583.3 tps, lat 13.709 ms stddev 22.546
progress: 520.0 s, 579.3 tps, lat 13.812 ms stddev 22.668
progress: 530.0 s, 587.5 tps, lat 13.618 ms stddev 21.964
progress: 540.0 s, 584.5 tps, lat 13.682 ms stddev 22.872
progress: 550.0 s, 582.7 tps, lat 13.733 ms stddev 22.341
progress: 560.0 s, 578.8 tps, lat 13.822 ms stddev 22.917
progress: 570.0 s, 580.5 tps, lat 13.780 ms stddev 22.968
progress: 580.0 s, 575.2 tps, lat 13.903 ms stddev 23.615
progress: 590.0 s, 581.2 tps, lat 13.768 ms stddev 23.132
progress: 600.0 s, 573.8 tps, lat 13.938 ms stddev 23.317
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 1
query mode: simple
number of clients: 8
number of threads: 1
duration: 600 s
number of transactions actually processed: 458764
latency average = 10.462 ms
latency stddev = 14.407 ms
tps = 764.571777 (including connections establishing)
tps = 764.575541 (excluding connections establishing)
```
</details>
  
 ### Агрессивные настройки Autovacuum:
  
<details>
<summary>Сет параметров:</summary>

```console
               Параметр                | Значение |                                         Описание                                          
---------------------------------------+----------+-------------------------------------------------------------------------------------------
 autovacuum                            | on       | Starts the autovacuum subprocess.
 autovacuum_analyze_scale_factor       | 0.02     | Number of tuple inserts, updates, or deletes prior to analyze as a fraction of reltuples.
 autovacuum_analyze_threshold          | 10       | Minimum number of tuple inserts, updates, or deletes prior to analyze.
 autovacuum_freeze_max_age             | 200000   | Age at which to autovacuum a table to prevent transaction ID wraparound.
 autovacuum_max_workers                | 8        | Sets the maximum number of simultaneously running autovacuum worker processes.
 autovacuum_multixact_freeze_max_age   | 400000   | Multixact age at which to autovacuum a table to prevent multixact wraparound.
 autovacuum_naptime                    | 1        | Time to sleep between autovacuum runs.
 autovacuum_vacuum_cost_delay          | 1        | Vacuum cost delay in milliseconds, for autovacuum.
 autovacuum_vacuum_cost_limit          | 200      | Vacuum cost amount available before napping, for autovacuum.
 autovacuum_vacuum_insert_scale_factor | 0.01     | Number of tuple inserts prior to vacuum as a fraction of reltuples.
 autovacuum_vacuum_insert_threshold    | 20       | Minimum number of tuple inserts prior to vacuum, or -1 to disable insert vacuums.
 autovacuum_vacuum_scale_factor        | 0.01     | Number of tuple updates or deletes prior to vacuum as a fraction of reltuples.
 autovacuum_vacuum_threshold           | 20       | Minimum number of tuple updates or deletes prior to vacuum.
 autovacuum_work_mem                   | -1       | Sets the maximum memory to be used by each autovacuum worker process.
 log_autovacuum_min_duration           | 0        | Sets the minimum execution time above which autovacuum actions will be logged.
(15 rows)
 ```
</details>

<details>
<summary>Выполнение pg_banch:</summary>

```console
  
```
</details>
  
 ### Пассивные настройки Autovacuum:
  
<details>
<summary>Сет параметров:</summary>

```console
  
 ```
</details>

<details>
<summary>Выполнение pg_banch:</summary>

```console
  
```
</details>  
