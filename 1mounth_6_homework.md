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
progress: 10.0 s, 893.7 tps, lat 8.923 ms stddev 7.253
progress: 20.0 s, 900.1 tps, lat 8.887 ms stddev 6.939
progress: 30.0 s, 900.7 tps, lat 8.882 ms stddev 6.925
progress: 40.0 s, 869.2 tps, lat 9.202 ms stddev 8.457
progress: 50.0 s, 871.2 tps, lat 9.183 ms stddev 7.074
progress: 60.0 s, 878.6 tps, lat 9.103 ms stddev 7.020
progress: 70.0 s, 914.9 tps, lat 8.744 ms stddev 6.751
progress: 80.0 s, 893.5 tps, lat 8.952 ms stddev 7.181
progress: 90.0 s, 893.2 tps, lat 8.956 ms stddev 6.886
progress: 100.0 s, 884.9 tps, lat 9.040 ms stddev 6.837
progress: 110.0 s, 904.6 tps, lat 8.842 ms stddev 6.622
progress: 120.0 s, 907.5 tps, lat 8.815 ms stddev 6.358
progress: 130.0 s, 907.8 tps, lat 8.811 ms stddev 6.854
progress: 140.0 s, 893.7 tps, lat 8.952 ms stddev 6.859
progress: 150.0 s, 877.8 tps, lat 9.109 ms stddev 7.035
progress: 160.0 s, 883.4 tps, lat 9.059 ms stddev 6.504
progress: 170.0 s, 910.5 tps, lat 8.785 ms stddev 6.813
progress: 180.0 s, 903.0 tps, lat 8.859 ms stddev 6.660
progress: 190.0 s, 892.4 tps, lat 8.965 ms stddev 7.108
progress: 200.0 s, 898.9 tps, lat 8.895 ms stddev 6.529
progress: 210.0 s, 898.1 tps, lat 8.912 ms stddev 6.810
progress: 220.0 s, 866.2 tps, lat 9.232 ms stddev 6.865
progress: 230.0 s, 872.2 tps, lat 9.171 ms stddev 6.820
progress: 240.0 s, 884.1 tps, lat 9.048 ms stddev 6.578
progress: 250.0 s, 863.3 tps, lat 9.266 ms stddev 7.034
progress: 260.0 s, 864.5 tps, lat 9.255 ms stddev 7.213
progress: 270.0 s, 880.3 tps, lat 9.086 ms stddev 6.769
progress: 280.0 s, 786.9 tps, lat 10.080 ms stddev 13.000
progress: 290.0 s, 535.6 tps, lat 14.941 ms stddev 26.006
progress: 300.0 s, 532.6 tps, lat 14.975 ms stddev 25.979
progress: 310.0 s, 539.9 tps, lat 14.794 ms stddev 25.763
progress: 320.0 s, 529.1 tps, lat 15.156 ms stddev 26.331
progress: 330.0 s, 522.0 tps, lat 15.314 ms stddev 26.497
progress: 340.0 s, 537.5 tps, lat 14.889 ms stddev 26.083
progress: 350.0 s, 534.4 tps, lat 14.972 ms stddev 25.333
progress: 360.0 s, 521.1 tps, lat 15.341 ms stddev 27.288
progress: 370.0 s, 524.2 tps, lat 15.266 ms stddev 26.742
progress: 380.0 s, 532.7 tps, lat 14.975 ms stddev 25.495
progress: 390.0 s, 518.1 tps, lat 15.426 ms stddev 27.011
progress: 400.0 s, 535.6 tps, lat 15.010 ms stddev 25.864
progress: 410.0 s, 531.4 tps, lat 15.049 ms stddev 26.321
progress: 420.0 s, 534.6 tps, lat 14.947 ms stddev 26.674
progress: 430.0 s, 520.4 tps, lat 15.377 ms stddev 27.144
progress: 440.0 s, 522.0 tps, lat 15.327 ms stddev 27.311
progress: 450.0 s, 533.0 tps, lat 15.004 ms stddev 26.133
progress: 460.0 s, 520.5 tps, lat 15.311 ms stddev 26.653
progress: 470.0 s, 528.4 tps, lat 15.200 ms stddev 26.921
progress: 480.0 s, 529.1 tps, lat 15.051 ms stddev 26.814
progress: 490.0 s, 535.3 tps, lat 14.996 ms stddev 26.608
progress: 500.0 s, 529.8 tps, lat 15.062 ms stddev 26.528
progress: 510.0 s, 532.5 tps, lat 14.996 ms stddev 25.809
progress: 520.0 s, 529.3 tps, lat 15.183 ms stddev 26.069
progress: 530.0 s, 514.5 tps, lat 15.519 ms stddev 27.002
progress: 540.0 s, 549.6 tps, lat 14.574 ms stddev 24.916
progress: 550.0 s, 525.4 tps, lat 15.215 ms stddev 26.669
progress: 560.0 s, 532.9 tps, lat 15.000 ms stddev 26.806
progress: 570.0 s, 520.5 tps, lat 15.351 ms stddev 25.984
progress: 580.0 s, 524.2 tps, lat 15.291 ms stddev 26.680
progress: 590.0 s, 545.9 tps, lat 14.627 ms stddev 25.052
progress: 600.0 s, 522.4 tps, lat 15.348 ms stddev 26.764
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 1
query mode: simple
number of clients: 8
number of threads: 1
duration: 600 s
number of transactions actually processed: 417408
latency average = 11.498 ms
latency stddev = 17.938 ms
tps = 695.643160 (including connections establishing)
tps = 695.646811 (excluding connections establishing)
```console
  
```
</details>
  
 ### Пассивные настройки Autovacuum:
  
<details>
<summary>Сет параметров:</summary>

```console
               Параметр                | Значение |                                         Описание                                          
---------------------------------------+----------+-------------------------------------------------------------------------------------------
 autovacuum                            | on       | Starts the autovacuum subprocess.
 autovacuum_analyze_scale_factor       | 0.7      | Number of tuple inserts, updates, or deletes prior to analyze as a fraction of reltuples.
 autovacuum_analyze_threshold          | 90000    | Minimum number of tuple inserts, updates, or deletes prior to analyze.
 autovacuum_freeze_max_age             | 200000   | Age at which to autovacuum a table to prevent transaction ID wraparound.
 autovacuum_max_workers                | 8        | Sets the maximum number of simultaneously running autovacuum worker processes.
 autovacuum_multixact_freeze_max_age   | 400000   | Multixact age at which to autovacuum a table to prevent multixact wraparound.
 autovacuum_naptime                    | 60       | Time to sleep between autovacuum runs.
 autovacuum_vacuum_cost_delay          | 1        | Vacuum cost delay in milliseconds, for autovacuum.
 autovacuum_vacuum_cost_limit          | 2000     | Vacuum cost amount available before napping, for autovacuum.
 autovacuum_vacuum_insert_scale_factor | 0.7      | Number of tuple inserts prior to vacuum as a fraction of reltuples.
 autovacuum_vacuum_insert_threshold    | 20000    | Minimum number of tuple inserts prior to vacuum, or -1 to disable insert vacuums.
 autovacuum_vacuum_scale_factor        | 0.7      | Number of tuple updates or deletes prior to vacuum as a fraction of reltuples.
 autovacuum_vacuum_threshold           | 20000    | Minimum number of tuple updates or deletes prior to vacuum.
 autovacuum_work_mem                   | -1       | Sets the maximum memory to be used by each autovacuum worker process.
 log_autovacuum_min_duration           | 0        | Sets the minimum execution time above which autovacuum actions will be logged.
(15 rows)
 ```
</details>

<details>
<summary>Выполнение pg_banch:</summary>

```console
starting vacuum...end.
progress: 10.0 s, 886.2 tps, lat 9.000 ms stddev 6.869
progress: 20.0 s, 900.3 tps, lat 8.887 ms stddev 6.890
progress: 30.0 s, 889.3 tps, lat 8.992 ms stddev 6.664
progress: 40.0 s, 880.7 tps, lat 9.084 ms stddev 6.768
progress: 50.0 s, 877.8 tps, lat 9.113 ms stddev 6.770
progress: 60.0 s, 896.9 tps, lat 8.917 ms stddev 6.639
progress: 70.0 s, 894.6 tps, lat 8.944 ms stddev 6.827
progress: 80.0 s, 881.6 tps, lat 9.070 ms stddev 6.738
progress: 90.0 s, 889.3 tps, lat 8.999 ms stddev 6.613
progress: 100.0 s, 871.4 tps, lat 9.180 ms stddev 7.020
progress: 110.0 s, 889.8 tps, lat 8.985 ms stddev 6.401
progress: 120.0 s, 903.3 tps, lat 8.860 ms stddev 6.468
progress: 130.0 s, 918.5 tps, lat 8.708 ms stddev 6.277
progress: 140.0 s, 858.6 tps, lat 9.316 ms stddev 6.331
progress: 150.0 s, 862.9 tps, lat 9.270 ms stddev 6.608
progress: 160.0 s, 898.5 tps, lat 8.905 ms stddev 6.034
progress: 170.0 s, 874.3 tps, lat 9.147 ms stddev 6.222
progress: 180.0 s, 905.8 tps, lat 8.834 ms stddev 5.883
progress: 190.0 s, 886.9 tps, lat 9.018 ms stddev 6.100
progress: 200.0 s, 878.6 tps, lat 9.105 ms stddev 6.092
progress: 210.0 s, 881.6 tps, lat 9.073 ms stddev 5.894
progress: 220.0 s, 885.0 tps, lat 9.039 ms stddev 6.096
progress: 230.0 s, 899.2 tps, lat 8.897 ms stddev 5.736
progress: 240.0 s, 902.0 tps, lat 8.867 ms stddev 5.836
progress: 250.0 s, 910.5 tps, lat 8.787 ms stddev 5.843
progress: 260.0 s, 898.4 tps, lat 8.903 ms stddev 5.755
progress: 270.0 s, 912.4 tps, lat 8.760 ms stddev 5.678
progress: 280.0 s, 912.8 tps, lat 8.769 ms stddev 6.522
progress: 290.0 s, 917.2 tps, lat 8.722 ms stddev 6.656
progress: 300.0 s, 922.3 tps, lat 8.673 ms stddev 6.821
progress: 310.0 s, 910.0 tps, lat 8.788 ms stddev 6.869
progress: 320.0 s, 917.9 tps, lat 8.714 ms stddev 6.921
progress: 330.0 s, 915.9 tps, lat 8.735 ms stddev 6.717
progress: 340.1 s, 831.6 tps, lat 9.528 ms stddev 10.776
progress: 350.1 s, 553.0 tps, lat 14.472 ms stddev 24.544
progress: 360.1 s, 557.1 tps, lat 14.372 ms stddev 24.496
progress: 370.1 s, 556.6 tps, lat 14.358 ms stddev 24.541
progress: 380.1 s, 558.1 tps, lat 14.335 ms stddev 24.273
progress: 390.1 s, 563.2 tps, lat 14.207 ms stddev 24.142
progress: 400.1 s, 547.4 tps, lat 14.616 ms stddev 24.644
progress: 410.1 s, 549.0 tps, lat 14.568 ms stddev 24.890
progress: 420.1 s, 568.7 tps, lat 14.061 ms stddev 24.076
progress: 430.1 s, 567.5 tps, lat 14.102 ms stddev 24.229
progress: 440.1 s, 553.7 tps, lat 14.446 ms stddev 23.958
progress: 450.1 s, 545.6 tps, lat 14.654 ms stddev 24.323
progress: 460.1 s, 547.0 tps, lat 14.627 ms stddev 24.131
progress: 470.1 s, 564.7 tps, lat 14.157 ms stddev 23.923
progress: 480.1 s, 568.0 tps, lat 14.091 ms stddev 23.677
progress: 490.1 s, 562.4 tps, lat 14.211 ms stddev 23.860
progress: 500.1 s, 561.4 tps, lat 14.281 ms stddev 24.164
progress: 510.1 s, 562.6 tps, lat 14.196 ms stddev 24.142
progress: 520.1 s, 558.1 tps, lat 14.339 ms stddev 24.220
progress: 530.1 s, 559.7 tps, lat 14.295 ms stddev 23.545
progress: 540.1 s, 551.2 tps, lat 14.509 ms stddev 24.324
progress: 550.0 s, 565.1 tps, lat 14.286 ms stddev 24.065
progress: 560.0 s, 557.2 tps, lat 14.359 ms stddev 23.623
progress: 570.1 s, 545.8 tps, lat 14.517 ms stddev 24.164
progress: 580.1 s, 550.0 tps, lat 14.554 ms stddev 24.257
progress: 590.1 s, 562.7 tps, lat 14.213 ms stddev 23.991
progress: 600.1 s, 559.0 tps, lat 14.303 ms stddev 23.875
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 1
query mode: simple
number of clients: 8
number of threads: 1
duration: 600 s
number of transactions actually processed: 448645
latency average = 10.699 ms
latency stddev = 14.982 ms
tps = 747.604731 (including connections establishing)
tps = 747.608314 (excluding connections establishing)
```
</details>  
