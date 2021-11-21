
<details>
<summary>Настрока</summary>

> https://github.com/Percona-Lab/sysbench-tpcc (требует установки https://github.com/akopytov/sysbench)
>
> **_NOTE:_** Команда для наполнения теста:
> 
> :warning: ./tpcc.lua --pgsql-user=postgres --pgsql-db=sbtest --time=300 --threads=36 --report-interval=1 --tables=5 --scale=5 --pgsql-host='127.0.0.1' --db-driver=pgsql prepare 
>
>**_NOTE:_** Команда для запуска теста:
>
> :warning: ./tpcc.lua --pgsql-user=postgres --pgsql-db=sbtest --time=300 --threads=36 --report-interval=1 --tables=5 --scale=5 --pgsql-host='127.0.0.1' --db-driver=pgsql run
>
> Параметры запуска были изменены для не слишком большого размера БД, т.к.:
>
> **"As a rough estimation, 100 warehouses with 1 table set produces about 10GB of data in non-compressed InnoDB tables (so 100 warehouses with 10 table sets gives about 100GB)."**
> 
> https://www.percona.com/blog/2018/06/15/tuning-postgresql-for-sysbench-tpcc/
> 
> https://www.percona.com/blog/why-linux-hugepages-are-super-important-for-database-servers-a-case-with-postgresql/
> 
> https://www.percona.com/blog/2018/03/05/tpcc-like-workload-sysbench-1-0/

</details>

ℹ️ Все тесты проводились с настройкой **threads=36**

### Тест на стандартных настройках - total number of events: 10313 (среднее - 34 tps)

<details>
<summary>log</summary>

```console
[ 1s ] thds: 36 tps: 108.54 qps: 3270.15 (r/w/o: 1460.81/1430.94/378.40) lat (ms,95%): 601.29 err/s 26.89 reconn/s: 0.00
[ 2s ] thds: 36 tps: 130.31 qps: 4067.65 (r/w/o: 1846.38/1902.51/318.76) lat (ms,95%): 530.08 err/s 29.07 reconn/s: 0.00
[ 3s ] thds: 36 tps: 132.00 qps: 4215.14 (r/w/o: 1927.06/1982.07/306.01) lat (ms,95%): 580.02 err/s 24.00 reconn/s: 0.00
[ 4s ] thds: 36 tps: 146.00 qps: 4267.95 (r/w/o: 1926.98/1978.98/362.00) lat (ms,95%): 539.71 err/s 35.00 reconn/s: 0.00
[ 5s ] thds: 36 tps: 155.00 qps: 4463.87 (r/w/o: 2040.94/2054.94/367.99) lat (ms,95%): 484.44 err/s 29.00 reconn/s: 0.00
[ 6s ] thds: 36 tps: 158.00 qps: 4318.98 (r/w/o: 1938.99/1997.99/382.00) lat (ms,95%): 530.08 err/s 33.00 reconn/s: 0.00
[ 7s ] thds: 36 tps: 145.00 qps: 4432.05 (r/w/o: 2016.02/2073.02/343.00) lat (ms,95%): 580.02 err/s 28.00 reconn/s: 0.00
[ 8s ] thds: 36 tps: 151.00 qps: 4309.00 (r/w/o: 1953.00/1987.00/369.00) lat (ms,95%): 539.71 err/s 33.00 reconn/s: 0.00
[ 9s ] thds: 36 tps: 71.01 qps: 2550.25 (r/w/o: 1177.11/1217.12/156.01) lat (ms,95%): 601.29 err/s 7.00 reconn/s: 0.00
[ 10s ] thds: 36 tps: 42.00 qps: 951.93 (r/w/o: 420.97/426.97/103.99) lat (ms,95%): 1304.21 err/s 10.00 reconn/s: 0.00
[ 11s ] thds: 36 tps: 19.00 qps: 1044.01 (r/w/o: 486.00/498.00/60.00) lat (ms,95%): 1771.29 err/s 13.00 reconn/s: 0.00
[ 12s ] thds: 36 tps: 43.00 qps: 1029.88 (r/w/o: 464.95/460.95/103.99) lat (ms,95%): 2728.81 err/s 9.00 reconn/s: 0.00
[ 13s ] thds: 36 tps: 30.00 qps: 944.09 (r/w/o: 434.04/440.04/70.01) lat (ms,95%): 1678.14 err/s 5.00 reconn/s: 0.00
[ 14s ] thds: 36 tps: 26.00 qps: 873.90 (r/w/o: 391.96/413.95/67.99) lat (ms,95%): 1708.63 err/s 8.00 reconn/s: 0.00
[ 15s ] thds: 36 tps: 35.00 qps: 777.04 (r/w/o: 341.02/360.02/76.00) lat (ms,95%): 1678.14 err/s 3.00 reconn/s: 0.00
[ 16s ] thds: 36 tps: 27.00 qps: 813.09 (r/w/o: 363.04/380.04/70.01) lat (ms,95%): 2279.14 err/s 8.00 reconn/s: 0.00
[ 17s ] thds: 36 tps: 27.00 qps: 897.90 (r/w/o: 414.95/410.95/71.99) lat (ms,95%): 3208.88 err/s 9.00 reconn/s: 0.00
[ 18s ] thds: 36 tps: 22.00 qps: 849.05 (r/w/o: 375.02/412.03/62.00) lat (ms,95%): 2045.74 err/s 9.00 reconn/s: 0.00
[ 19s ] thds: 36 tps: 42.00 qps: 916.04 (r/w/o: 396.02/420.02/100.00) lat (ms,95%): 3095.38 err/s 8.00 reconn/s: 0.00
[ 20s ] thds: 36 tps: 29.00 qps: 1110.07 (r/w/o: 509.03/527.03/74.00) lat (ms,95%): 2880.27 err/s 9.00 reconn/s: 0.00
[ 21s ] thds: 36 tps: 35.00 qps: 1057.90 (r/w/o: 480.95/486.95/89.99) lat (ms,95%): 1903.57 err/s 10.00 reconn/s: 0.00
[ 22s ] thds: 36 tps: 31.00 qps: 916.93 (r/w/o: 418.97/427.97/69.99) lat (ms,95%): 1803.47 err/s 4.00 reconn/s: 0.00
[ 23s ] thds: 36 tps: 31.00 qps: 1261.03 (r/w/o: 565.01/618.01/78.00) lat (ms,95%): 1708.63 err/s 8.00 reconn/s: 0.00
[ 24s ] thds: 36 tps: 30.00 qps: 855.06 (r/w/o: 382.03/403.03/70.01) lat (ms,95%): 3208.88 err/s 6.00 reconn/s: 0.00
[ 25s ] thds: 36 tps: 21.00 qps: 805.01 (r/w/o: 365.00/388.00/52.00) lat (ms,95%): 2493.86 err/s 5.00 reconn/s: 0.00
[ 26s ] thds: 36 tps: 38.00 qps: 1042.92 (r/w/o: 474.96/475.96/91.99) lat (ms,95%): 2680.11 err/s 8.00 reconn/s: 0.00
[ 27s ] thds: 36 tps: 24.00 qps: 1031.06 (r/w/o: 464.03/507.03/60.00) lat (ms,95%): 2238.47 err/s 6.00 reconn/s: 0.00
[ 28s ] thds: 36 tps: 31.99 qps: 1086.60 (r/w/o: 489.82/510.81/85.97) lat (ms,95%): 3040.14 err/s 11.00 reconn/s: 0.00
[ 29s ] thds: 36 tps: 41.01 qps: 1083.23 (r/w/o: 482.10/510.11/91.02) lat (ms,95%): 2320.55 err/s 8.00 reconn/s: 0.00
[ 30s ] thds: 36 tps: 43.01 qps: 1183.19 (r/w/o: 527.09/543.09/113.02) lat (ms,95%): 1258.08 err/s 10.00 reconn/s: 0.00
[ 31s ] thds: 36 tps: 39.00 qps: 1167.07 (r/w/o: 536.03/531.03/100.01) lat (ms,95%): 1803.47 err/s 11.00 reconn/s: 0.00
[ 32s ] thds: 36 tps: 35.00 qps: 980.88 (r/w/o: 445.95/448.95/85.99) lat (ms,95%): 1903.57 err/s 8.00 reconn/s: 0.00
[ 33s ] thds: 36 tps: 29.00 qps: 965.99 (r/w/o: 434.00/453.99/78.00) lat (ms,95%): 1836.24 err/s 10.00 reconn/s: 0.00
[ 34s ] thds: 36 tps: 34.00 qps: 1180.08 (r/w/o: 533.04/563.04/84.01) lat (ms,95%): 2198.52 err/s 8.00 reconn/s: 0.00
[ 35s ] thds: 36 tps: 37.00 qps: 811.99 (r/w/o: 362.00/366.00/84.00) lat (ms,95%): 2120.76 err/s 5.00 reconn/s: 0.00
[ 36s ] thds: 36 tps: 35.00 qps: 1343.93 (r/w/o: 608.97/644.97/90.00) lat (ms,95%): 1280.93 err/s 10.00 reconn/s: 0.00
[ 37s ] thds: 36 tps: 44.00 qps: 1130.88 (r/w/o: 497.95/520.95/111.99) lat (ms,95%): 1903.57 err/s 12.00 reconn/s: 0.00
[ 38s ] thds: 36 tps: 28.00 qps: 1110.13 (r/w/o: 512.06/532.06/66.01) lat (ms,95%): 1327.91 err/s 6.00 reconn/s: 0.00
[ 39s ] thds: 36 tps: 56.00 qps: 1251.01 (r/w/o: 556.00/547.00/148.00) lat (ms,95%): 2120.76 err/s 18.00 reconn/s: 0.00
[ 40s ] thds: 36 tps: 28.00 qps: 1143.15 (r/w/o: 537.07/536.07/70.01) lat (ms,95%): 2449.36 err/s 7.00 reconn/s: 0.00
[ 41s ] thds: 36 tps: 45.00 qps: 1231.92 (r/w/o: 547.96/563.96/119.99) lat (ms,95%): 1708.63 err/s 15.00 reconn/s: 0.00
[ 42s ] thds: 36 tps: 44.00 qps: 1060.00 (r/w/o: 473.00/475.00/112.00) lat (ms,95%): 1401.61 err/s 12.00 reconn/s: 0.00
[ 43s ] thds: 36 tps: 33.00 qps: 1262.07 (r/w/o: 572.03/602.03/88.00) lat (ms,95%): 1836.24 err/s 11.00 reconn/s: 0.00
[ 44s ] thds: 36 tps: 34.00 qps: 1058.91 (r/w/o: 476.96/497.96/83.99) lat (ms,95%): 1973.38 err/s 8.00 reconn/s: 0.00
[ 45s ] thds: 36 tps: 41.00 qps: 1232.01 (r/w/o: 545.01/581.01/106.00) lat (ms,95%): 1803.47 err/s 12.00 reconn/s: 0.00
[ 46s ] thds: 36 tps: 30.00 qps: 1005.98 (r/w/o: 460.99/472.99/72.00) lat (ms,95%): 1589.90 err/s 6.00 reconn/s: 0.00
[ 47s ] thds: 36 tps: 41.00 qps: 1324.96 (r/w/o: 595.98/628.98/100.00) lat (ms,95%): 1903.57 err/s 9.00 reconn/s: 0.00
[ 48s ] thds: 36 tps: 28.00 qps: 1053.05 (r/w/o: 478.02/505.02/70.00) lat (ms,95%): 1648.20 err/s 7.00 reconn/s: 0.00
[ 49s ] thds: 36 tps: 50.00 qps: 1588.99 (r/w/o: 723.99/750.99/114.00) lat (ms,95%): 1678.14 err/s 8.00 reconn/s: 0.00
[ 50s ] thds: 36 tps: 35.00 qps: 1358.10 (r/w/o: 623.05/645.05/90.01) lat (ms,95%): 1149.76 err/s 10.00 reconn/s: 0.00
[ 51s ] thds: 36 tps: 54.99 qps: 1054.87 (r/w/o: 466.94/474.94/112.99) lat (ms,95%): 1506.29 err/s 6.00 reconn/s: 0.00
[ 52s ] thds: 36 tps: 32.00 qps: 1387.21 (r/w/o: 637.10/653.10/97.01) lat (ms,95%): 1191.92 err/s 12.00 reconn/s: 0.00
[ 53s ] thds: 36 tps: 50.00 qps: 1521.95 (r/w/o: 684.98/706.98/130.00) lat (ms,95%): 1533.66 err/s 15.00 reconn/s: 0.00
[ 54s ] thds: 36 tps: 49.00 qps: 1264.94 (r/w/o: 574.97/565.97/123.99) lat (ms,95%): 1589.90 err/s 13.00 reconn/s: 0.00
[ 55s ] thds: 36 tps: 42.00 qps: 937.01 (r/w/o: 416.01/425.01/96.00) lat (ms,95%): 1973.38 err/s 6.00 reconn/s: 0.00
[ 56s ] thds: 36 tps: 29.00 qps: 1430.90 (r/w/o: 666.95/677.95/85.99) lat (ms,95%): 1191.92 err/s 15.00 reconn/s: 0.00
[ 57s ] thds: 36 tps: 54.00 qps: 1572.02 (r/w/o: 710.01/734.01/128.00) lat (ms,95%): 1561.52 err/s 11.00 reconn/s: 0.00
[ 58s ] thds: 36 tps: 52.00 qps: 1464.12 (r/w/o: 662.06/676.06/126.01) lat (ms,95%): 1327.91 err/s 11.00 reconn/s: 0.00
[ 59s ] thds: 36 tps: 36.00 qps: 1158.89 (r/w/o: 529.95/544.95/83.99) lat (ms,95%): 1352.03 err/s 6.00 reconn/s: 0.00
[ 60s ] thds: 36 tps: 48.99 qps: 1568.79 (r/w/o: 710.91/739.90/117.98) lat (ms,95%): 1479.41 err/s 10.00 reconn/s: 0.00
[ 61s ] thds: 36 tps: 59.01 qps: 1245.19 (r/w/o: 539.08/543.08/163.02) lat (ms,95%): 1213.57 err/s 23.00 reconn/s: 0.00
[ 62s ] thds: 36 tps: 33.00 qps: 1612.89 (r/w/o: 753.95/775.95/82.99) lat (ms,95%): 1258.08 err/s 9.00 reconn/s: 0.00
[ 63s ] thds: 36 tps: 46.99 qps: 1313.85 (r/w/o: 590.93/606.93/115.99) lat (ms,95%): 1708.63 err/s 11.00 reconn/s: 0.00
[ 64s ] thds: 36 tps: 45.01 qps: 1476.18 (r/w/o: 670.08/686.08/120.01) lat (ms,95%): 1352.03 err/s 15.00 reconn/s: 0.00
[ 65s ] thds: 36 tps: 63.99 qps: 1229.75 (r/w/o: 519.89/545.89/163.97) lat (ms,95%): 1401.61 err/s 18.00 reconn/s: 0.00
[ 66s ] thds: 36 tps: 44.01 qps: 1570.49 (r/w/o: 722.22/724.22/124.04) lat (ms,95%): 943.16 err/s 18.01 reconn/s: 0.00
[ 67s ] thds: 36 tps: 49.00 qps: 1479.97 (r/w/o: 666.99/692.99/120.00) lat (ms,95%): 1708.63 err/s 11.00 reconn/s: 0.00
[ 68s ] thds: 36 tps: 44.00 qps: 1474.03 (r/w/o: 662.02/680.02/132.00) lat (ms,95%): 1648.20 err/s 22.00 reconn/s: 0.00
[ 69s ] thds: 36 tps: 53.99 qps: 1446.71 (r/w/o: 646.87/667.87/131.97) lat (ms,95%): 1648.20 err/s 12.00 reconn/s: 0.00
[ 70s ] thds: 36 tps: 48.01 qps: 1455.16 (r/w/o: 666.07/667.07/122.01) lat (ms,95%): 1401.61 err/s 13.00 reconn/s: 0.00
[ 71s ] thds: 36 tps: 50.00 qps: 1566.12 (r/w/o: 705.06/723.06/138.01) lat (ms,95%): 1589.90 err/s 19.00 reconn/s: 0.00
[ 72s ] thds: 36 tps: 49.00 qps: 1327.99 (r/w/o: 601.99/605.99/120.00) lat (ms,95%): 1648.20 err/s 12.00 reconn/s: 0.00
[ 73s ] thds: 36 tps: 36.00 qps: 1710.93 (r/w/o: 786.97/833.96/90.00) lat (ms,95%): 1258.08 err/s 10.00 reconn/s: 0.00
[ 74s ] thds: 36 tps: 53.00 qps: 1465.07 (r/w/o: 666.03/677.03/122.01) lat (ms,95%): 1678.14 err/s 8.00 reconn/s: 0.00
[ 75s ] thds: 36 tps: 47.00 qps: 1324.99 (r/w/o: 617.99/599.00/108.00) lat (ms,95%): 1352.03 err/s 7.00 reconn/s: 0.00
[ 76s ] thds: 36 tps: 64.00 qps: 2004.88 (r/w/o: 906.95/929.95/167.99) lat (ms,95%): 1213.57 err/s 21.00 reconn/s: 0.00
[ 77s ] thds: 36 tps: 48.00 qps: 1578.02 (r/w/o: 717.01/733.01/128.00) lat (ms,95%): 1258.08 err/s 16.00 reconn/s: 0.00
[ 78s ] thds: 36 tps: 47.00 qps: 1284.05 (r/w/o: 562.02/596.02/126.00) lat (ms,95%): 1401.61 err/s 16.00 reconn/s: 0.00
[ 79s ] thds: 36 tps: 49.00 qps: 1625.12 (r/w/o: 745.06/752.06/128.01) lat (ms,95%): 1235.62 err/s 15.00 reconn/s: 0.00
[ 80s ] thds: 36 tps: 65.99 qps: 1782.86 (r/w/o: 793.94/822.93/165.99) lat (ms,95%): 1213.57 err/s 18.00 reconn/s: 0.00
[ 81s ] thds: 36 tps: 34.00 qps: 1566.02 (r/w/o: 727.01/759.01/80.00) lat (ms,95%): 1013.60 err/s 6.00 reconn/s: 0.00
[ 82s ] thds: 36 tps: 53.00 qps: 1818.09 (r/w/o: 827.04/855.04/136.01) lat (ms,95%): 1327.91 err/s 15.00 reconn/s: 0.00
[ 83s ] thds: 36 tps: 47.00 qps: 1386.00 (r/w/o: 624.00/650.00/112.00) lat (ms,95%): 1304.21 err/s 9.00 reconn/s: 0.00
[ 84s ] thds: 36 tps: 74.99 qps: 1942.66 (r/w/o: 859.85/880.85/201.96) lat (ms,95%): 1109.09 err/s 28.99 reconn/s: 0.00
[ 85s ] thds: 36 tps: 52.01 qps: 1460.21 (r/w/o: 665.10/651.10/144.02) lat (ms,95%): 1129.24 err/s 18.00 reconn/s: 0.00
[ 86s ] thds: 36 tps: 43.00 qps: 1764.94 (r/w/o: 806.97/841.97/116.00) lat (ms,95%): 1280.93 err/s 15.00 reconn/s: 0.00
[ 87s ] thds: 36 tps: 50.00 qps: 1711.87 (r/w/o: 781.94/793.94/135.99) lat (ms,95%): 1533.66 err/s 18.00 reconn/s: 0.00
[ 88s ] thds: 36 tps: 50.00 qps: 1603.07 (r/w/o: 727.03/756.03/120.00) lat (ms,95%): 1938.16 err/s 10.00 reconn/s: 0.00
[ 89s ] thds: 36 tps: 59.00 qps: 1596.00 (r/w/o: 723.00/733.00/140.00) lat (ms,95%): 1235.62 err/s 11.00 reconn/s: 0.00
[ 90s ] thds: 36 tps: 62.00 qps: 1767.96 (r/w/o: 793.98/817.98/156.00) lat (ms,95%): 943.16 err/s 18.00 reconn/s: 0.00
[ 91s ] thds: 36 tps: 45.00 qps: 1645.15 (r/w/o: 733.07/786.07/126.01) lat (ms,95%): 1327.91 err/s 18.00 reconn/s: 0.00
[ 92s ] thds: 36 tps: 57.01 qps: 1631.15 (r/w/o: 741.07/752.07/138.01) lat (ms,95%): 1352.03 err/s 12.00 reconn/s: 0.00
[ 93s ] thds: 36 tps: 61.00 qps: 1779.97 (r/w/o: 799.99/825.99/154.00) lat (ms,95%): 943.16 err/s 16.00 reconn/s: 0.00
[ 94s ] thds: 36 tps: 45.99 qps: 1548.75 (r/w/o: 704.89/725.88/117.98) lat (ms,95%): 1376.60 err/s 13.00 reconn/s: 0.00
[ 95s ] thds: 36 tps: 60.00 qps: 1850.10 (r/w/o: 833.05/859.05/158.01) lat (ms,95%): 1327.91 err/s 19.00 reconn/s: 0.00
[ 96s ] thds: 36 tps: 52.00 qps: 1652.04 (r/w/o: 749.02/769.02/134.00) lat (ms,95%): 1109.09 err/s 15.00 reconn/s: 0.00
[ 97s ] thds: 36 tps: 53.00 qps: 1701.11 (r/w/o: 776.05/793.05/132.01) lat (ms,95%): 1213.57 err/s 13.00 reconn/s: 0.00
[ 98s ] thds: 36 tps: 50.00 qps: 1466.00 (r/w/o: 655.00/695.00/116.00) lat (ms,95%): 1453.01 err/s 8.00 reconn/s: 0.00
[ 99s ] thds: 36 tps: 29.00 qps: 1307.78 (r/w/o: 588.90/646.89/71.99) lat (ms,95%): 1089.30 err/s 7.00 reconn/s: 0.00
[ 100s ] thds: 36 tps: 68.00 qps: 1712.09 (r/w/o: 765.04/790.04/157.01) lat (ms,95%): 1479.41 err/s 12.00 reconn/s: 0.00
[ 101s ] thds: 36 tps: 54.01 qps: 1968.25 (r/w/o: 905.12/928.12/135.02) lat (ms,95%): 995.51 err/s 14.00 reconn/s: 0.00
[ 102s ] thds: 36 tps: 48.00 qps: 1771.89 (r/w/o: 811.95/845.95/113.99) lat (ms,95%): 1533.66 err/s 9.00 reconn/s: 0.00
[ 103s ] thds: 36 tps: 52.00 qps: 1553.09 (r/w/o: 695.04/736.04/122.01) lat (ms,95%): 893.56 err/s 9.00 reconn/s: 0.00
[ 104s ] thds: 36 tps: 67.00 qps: 2230.02 (r/w/o: 1005.01/1053.01/172.00) lat (ms,95%): 1280.93 err/s 20.00 reconn/s: 0.00
[ 105s ] thds: 36 tps: 48.00 qps: 1791.83 (r/w/o: 812.92/852.92/125.99) lat (ms,95%): 943.16 err/s 15.00 reconn/s: 0.00
[ 106s ] thds: 36 tps: 47.00 qps: 1351.89 (r/w/o: 606.95/626.95/117.99) lat (ms,95%): 977.74 err/s 12.00 reconn/s: 0.00
[ 107s ] thds: 36 tps: 48.01 qps: 1356.14 (r/w/o: 598.06/636.07/122.01) lat (ms,95%): 1327.91 err/s 13.00 reconn/s: 0.00
[ 108s ] thds: 36 tps: 61.00 qps: 2025.94 (r/w/o: 908.97/948.97/167.99) lat (ms,95%): 1533.66 err/s 23.00 reconn/s: 0.00
[ 109s ] thds: 36 tps: 46.00 qps: 1554.95 (r/w/o: 704.98/737.97/112.00) lat (ms,95%): 1213.57 err/s 11.00 reconn/s: 0.00
[ 110s ] thds: 36 tps: 71.00 qps: 2336.03 (r/w/o: 1068.01/1096.01/172.00) lat (ms,95%): 1376.60 err/s 15.00 reconn/s: 0.00
[ 111s ] thds: 36 tps: 72.00 qps: 1877.00 (r/w/o: 849.00/852.00/176.00) lat (ms,95%): 1050.76 err/s 16.00 reconn/s: 0.00
[ 112s ] thds: 36 tps: 50.00 qps: 1704.14 (r/w/o: 780.07/788.07/136.01) lat (ms,95%): 995.51 err/s 18.00 reconn/s: 0.00
[ 113s ] thds: 36 tps: 59.99 qps: 1766.76 (r/w/o: 801.89/827.89/136.98) lat (ms,95%): 1304.21 err/s 14.00 reconn/s: 0.00
[ 114s ] thds: 36 tps: 53.00 qps: 1883.13 (r/w/o: 848.06/886.06/149.01) lat (ms,95%): 909.80 err/s 16.00 reconn/s: 0.00
[ 115s ] thds: 36 tps: 43.00 qps: 1728.02 (r/w/o: 794.01/824.01/110.00) lat (ms,95%): 1191.92 err/s 12.00 reconn/s: 0.00
[ 116s ] thds: 36 tps: 64.00 qps: 2038.98 (r/w/o: 930.99/949.99/158.00) lat (ms,95%): 1149.76 err/s 15.00 reconn/s: 0.00
[ 117s ] thds: 36 tps: 48.99 qps: 1341.81 (r/w/o: 600.92/608.92/131.98) lat (ms,95%): 995.51 err/s 17.00 reconn/s: 0.00
[ 118s ] thds: 36 tps: 38.01 qps: 1171.16 (r/w/o: 541.07/544.07/86.01) lat (ms,95%): 1280.93 err/s 5.00 reconn/s: 0.00
[ 119s ] thds: 36 tps: 56.01 qps: 1216.13 (r/w/o: 539.06/531.06/146.02) lat (ms,95%): 1533.66 err/s 17.00 reconn/s: 0.00
[ 120s ] thds: 36 tps: 30.00 qps: 1111.88 (r/w/o: 506.94/522.94/81.99) lat (ms,95%): 1678.14 err/s 11.00 reconn/s: 0.00
[ 121s ] thds: 36 tps: 34.00 qps: 1185.07 (r/w/o: 544.03/551.03/90.01) lat (ms,95%): 1561.52 err/s 11.00 reconn/s: 0.00
[ 122s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 123s ] thds: 36 tps: 15.00 qps: 209.00 (r/w/o: 86.00/89.00/34.00) lat (ms,95%): 3151.62 err/s 2.00 reconn/s: 0.00
[ 124s ] thds: 36 tps: 19.00 qps: 781.08 (r/w/o: 354.04/383.04/44.00) lat (ms,95%): 3574.99 err/s 3.00 reconn/s: 0.00
[ 125s ] thds: 36 tps: 29.99 qps: 1113.69 (r/w/o: 503.86/527.85/81.98) lat (ms,95%): 4055.23 err/s 12.00 reconn/s: 0.00
[ 126s ] thds: 36 tps: 15.00 qps: 403.09 (r/w/o: 179.04/192.04/32.01) lat (ms,95%): 1869.60 err/s 1.00 reconn/s: 0.00
[ 127s ] thds: 36 tps: 20.00 qps: 126.98 (r/w/o: 38.99/37.99/49.99) lat (ms,95%): 3841.98 err/s 5.00 reconn/s: 0.00
[ 128s ] thds: 36 tps: 16.00 qps: 956.23 (r/w/o: 442.11/466.11/48.01) lat (ms,95%): 2585.31 err/s 8.00 reconn/s: 0.00
[ 129s ] thds: 36 tps: 33.00 qps: 472.96 (r/w/o: 185.99/206.98/79.99) lat (ms,95%): 3448.53 err/s 7.00 reconn/s: 0.00
[ 130s ] thds: 36 tps: 28.00 qps: 1327.10 (r/w/o: 614.05/645.05/68.01) lat (ms,95%): 2362.72 err/s 6.00 reconn/s: 0.00
[ 131s ] thds: 36 tps: 21.00 qps: 917.95 (r/w/o: 420.98/442.97/54.00) lat (ms,95%): 1618.78 err/s 6.00 reconn/s: 0.00
[ 132s ] thds: 36 tps: 29.00 qps: 960.96 (r/w/o: 432.98/455.98/72.00) lat (ms,95%): 1771.29 err/s 7.00 reconn/s: 0.00
[ 133s ] thds: 36 tps: 36.00 qps: 1016.97 (r/w/o: 454.98/477.98/84.00) lat (ms,95%): 3511.19 err/s 6.00 reconn/s: 0.00
[ 134s ] thds: 36 tps: 13.00 qps: 594.03 (r/w/o: 272.02/286.02/36.00) lat (ms,95%): 1129.24 err/s 5.00 reconn/s: 0.00
[ 135s ] thds: 36 tps: 23.00 qps: 482.99 (r/w/o: 215.99/212.99/54.00) lat (ms,95%): 1771.29 err/s 4.00 reconn/s: 0.00
[ 136s ] thds: 36 tps: 33.00 qps: 1042.06 (r/w/o: 468.03/488.03/86.01) lat (ms,95%): 2728.81 err/s 10.00 reconn/s: 0.00
[ 137s ] thds: 36 tps: 17.00 qps: 508.01 (r/w/o: 236.01/236.01/36.00) lat (ms,95%): 1938.16 err/s 1.00 reconn/s: 0.00
[ 138s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 139s ] thds: 36 tps: 20.00 qps: 157.00 (r/w/o: 50.00/53.00/54.00) lat (ms,95%): 4599.99 err/s 7.00 reconn/s: 0.00
[ 140s ] thds: 36 tps: 42.00 qps: 2021.96 (r/w/o: 936.98/972.98/112.00) lat (ms,95%): 3773.42 err/s 14.00 reconn/s: 0.00
[ 141s ] thds: 36 tps: 45.00 qps: 1196.01 (r/w/o: 527.01/555.01/114.00) lat (ms,95%): 1589.90 err/s 12.00 reconn/s: 0.00
[ 142s ] thds: 36 tps: 55.01 qps: 1395.19 (r/w/o: 628.09/631.09/136.02) lat (ms,95%): 1280.93 err/s 13.00 reconn/s: 0.00
[ 143s ] thds: 36 tps: 14.00 qps: 837.94 (r/w/o: 400.97/404.97/32.00) lat (ms,95%): 1235.62 err/s 2.00 reconn/s: 0.00
[ 144s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 145s ] thds: 36 tps: 22.00 qps: 180.01 (r/w/o: 63.00/61.00/56.00) lat (ms,95%): 2828.87 err/s 6.00 reconn/s: 0.00
[ 146s ] thds: 36 tps: 28.00 qps: 1086.06 (r/w/o: 494.03/510.03/82.00) lat (ms,95%): 4055.23 err/s 13.00 reconn/s: 0.00
[ 147s ] thds: 36 tps: 28.99 qps: 1393.69 (r/w/o: 647.85/669.85/75.98) lat (ms,95%): 3773.42 err/s 9.00 reconn/s: 0.00
[ 148s ] thds: 36 tps: 46.01 qps: 1508.25 (r/w/o: 677.11/717.12/114.02) lat (ms,95%): 2362.72 err/s 11.00 reconn/s: 0.00
[ 149s ] thds: 36 tps: 24.00 qps: 280.01 (r/w/o: 109.00/109.00/62.00) lat (ms,95%): 1648.20 err/s 7.00 reconn/s: 0.00
[ 150s ] thds: 36 tps: 49.00 qps: 1668.01 (r/w/o: 769.00/777.00/122.00) lat (ms,95%): 1869.60 err/s 12.00 reconn/s: 0.00
[ 151s ] thds: 36 tps: 27.00 qps: 1309.91 (r/w/o: 591.96/641.96/75.99) lat (ms,95%): 1803.47 err/s 11.00 reconn/s: 0.00
[ 152s ] thds: 36 tps: 52.00 qps: 1451.05 (r/w/o: 645.02/676.02/130.00) lat (ms,95%): 1453.01 err/s 13.00 reconn/s: 0.00
[ 153s ] thds: 36 tps: 80.00 qps: 2523.91 (r/w/o: 1127.96/1185.96/209.99) lat (ms,95%): 1327.91 err/s 25.00 reconn/s: 0.00
[ 154s ] thds: 36 tps: 46.00 qps: 1272.12 (r/w/o: 570.05/590.06/112.01) lat (ms,95%): 943.16 err/s 10.00 reconn/s: 0.00
[ 155s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 156s ] thds: 36 tps: 12.00 qps: 306.00 (r/w/o: 134.00/142.00/30.00) lat (ms,95%): 2778.39 err/s 3.00 reconn/s: 0.00
[ 157s ] thds: 36 tps: 3.00 qps: 178.99 (r/w/o: 85.00/88.00/6.00) lat (ms,95%): 2932.60 err/s 0.00 reconn/s: 0.00
[ 158s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 159s ] thds: 36 tps: 18.00 qps: 65.00 (r/w/o: 12.00/11.00/42.00) lat (ms,95%): 6026.41 err/s 3.00 reconn/s: 0.00
[ 160s ] thds: 36 tps: 4.00 qps: 723.05 (r/w/o: 353.02/354.02/16.00) lat (ms,95%): 6135.91 err/s 4.00 reconn/s: 0.00
[ 161s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 162s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 163s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 164s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 165s ] thds: 36 tps: 13.00 qps: 461.01 (r/w/o: 210.01/221.01/30.00) lat (ms,95%): 11317.84 err/s 2.00 reconn/s: 0.00
[ 166s ] thds: 36 tps: 2.00 qps: 196.99 (r/w/o: 97.00/96.00/4.00) lat (ms,95%): 6026.41 err/s 0.00 reconn/s: 0.00
[ 167s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 168s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 169s ] thds: 36 tps: 19.00 qps: 597.94 (r/w/o: 269.97/279.97/48.00) lat (ms,95%): 14827.42 err/s 5.00 reconn/s: 0.00
[ 170s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 171s ] thds: 36 tps: 17.00 qps: 376.01 (r/w/o: 166.00/172.00/38.00) lat (ms,95%): 11946.04 err/s 2.00 reconn/s: 0.00
[ 172s ] thds: 36 tps: 17.00 qps: 930.99 (r/w/o: 435.99/456.99/38.00) lat (ms,95%): 3267.19 err/s 2.00 reconn/s: 0.00
[ 173s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 174s ] thds: 36 tps: 18.00 qps: 493.01 (r/w/o: 222.01/229.01/42.00) lat (ms,95%): 14302.94 err/s 3.00 reconn/s: 0.00
[ 175s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 176s ] thds: 36 tps: 11.00 qps: 331.98 (r/w/o: 145.99/153.99/32.00) lat (ms,95%): 4203.93 err/s 5.00 reconn/s: 0.00
[ 177s ] thds: 36 tps: 1.00 qps: 296.98 (r/w/o: 139.99/154.99/2.00) lat (ms,95%): 5409.26 err/s 0.00 reconn/s: 0.00
[ 178s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 179s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 180s ] thds: 36 tps: 19.00 qps: 553.99 (r/w/o: 248.00/256.00/50.00) lat (ms,95%): 20137.61 err/s 6.00 reconn/s: 0.00
[ 181s ] thds: 36 tps: 25.00 qps: 307.96 (r/w/o: 113.98/123.98/69.99) lat (ms,95%): 15371.13 err/s 10.00 reconn/s: 0.00
[ 182s ] thds: 36 tps: 2.00 qps: 367.05 (r/w/o: 183.03/180.02/4.00) lat (ms,95%): 16519.10 err/s 0.00 reconn/s: 0.00
[ 183s ] thds: 36 tps: 21.00 qps: 57.00 (r/w/o: 7.00/4.00/46.00) lat (ms,95%): 14562.82 err/s 2.00 reconn/s: 0.00
[ 184s ] thds: 36 tps: 7.00 qps: 731.03 (r/w/o: 348.02/357.02/26.00) lat (ms,95%): 3095.38 err/s 6.00 reconn/s: 0.00
[ 185s ] thds: 36 tps: 42.00 qps: 959.90 (r/w/o: 418.96/432.96/107.99) lat (ms,95%): 4517.90 err/s 12.00 reconn/s: 0.00
[ 186s ] thds: 36 tps: 20.00 qps: 1190.01 (r/w/o: 563.00/581.00/46.00) lat (ms,95%): 2680.11 err/s 3.00 reconn/s: 0.00
[ 187s ] thds: 36 tps: 1.00 qps: 67.01 (r/w/o: 32.00/33.00/2.00) lat (ms,95%): 1129.24 err/s 0.00 reconn/s: 0.00
[ 188s ] thds: 36 tps: 19.00 qps: 661.95 (r/w/o: 296.98/320.98/44.00) lat (ms,95%): 2932.60 err/s 3.00 reconn/s: 0.00
[ 189s ] thds: 36 tps: 26.00 qps: 329.01 (r/w/o: 130.01/135.01/64.00) lat (ms,95%): 8184.67 err/s 6.00 reconn/s: 0.00
[ 190s ] thds: 36 tps: 1.00 qps: 332.00 (r/w/o: 167.00/163.00/2.00) lat (ms,95%): 2449.36 err/s 0.00 reconn/s: 0.00
[ 191s ] thds: 36 tps: 13.00 qps: 580.02 (r/w/o: 264.01/284.01/32.00) lat (ms,95%): 1869.60 err/s 3.00 reconn/s: 0.00
[ 192s ] thds: 36 tps: 17.00 qps: 770.98 (r/w/o: 352.99/375.99/42.00) lat (ms,95%): 5507.54 err/s 4.00 reconn/s: 0.00
[ 193s ] thds: 36 tps: 1.00 qps: 5.00 (r/w/o: 3.00/0.00/2.00) lat (ms,95%): 3386.99 err/s 0.00 reconn/s: 0.00
[ 194s ] thds: 36 tps: 18.01 qps: 392.12 (r/w/o: 163.05/179.05/50.01) lat (ms,95%): 5124.81 err/s 7.00 reconn/s: 0.00
[ 195s ] thds: 36 tps: 0.00 qps: 433.00 (r/w/o: 214.00/219.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 196s ] thds: 36 tps: 18.00 qps: 118.00 (r/w/o: 44.00/38.00/36.00) lat (ms,95%): 6960.17 err/s 0.00 reconn/s: 0.00
[ 197s ] thds: 36 tps: 29.00 qps: 1292.89 (r/w/o: 591.95/626.95/73.99) lat (ms,95%): 6247.39 err/s 8.00 reconn/s: 0.00
[ 198s ] thds: 36 tps: 40.00 qps: 804.05 (r/w/o: 347.02/353.02/104.01) lat (ms,95%): 6247.39 err/s 12.00 reconn/s: 0.00
[ 199s ] thds: 36 tps: 33.00 qps: 814.05 (r/w/o: 358.02/376.02/80.00) lat (ms,95%): 1589.90 err/s 8.00 reconn/s: 0.00
[ 200s ] thds: 36 tps: 17.00 qps: 1028.96 (r/w/o: 480.98/505.98/42.00) lat (ms,95%): 2405.65 err/s 4.00 reconn/s: 0.00
[ 201s ] thds: 36 tps: 2.00 qps: 392.94 (r/w/o: 183.97/204.97/4.00) lat (ms,95%): 1739.68 err/s 0.00 reconn/s: 0.00
[ 202s ] thds: 36 tps: 20.00 qps: 780.12 (r/w/o: 353.06/379.06/48.01) lat (ms,95%): 3386.99 err/s 4.00 reconn/s: 0.00
[ 203s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 204s ] thds: 36 tps: 26.00 qps: 649.01 (r/w/o: 288.00/309.00/52.00) lat (ms,95%): 5124.81 err/s 0.00 reconn/s: 0.00
[ 205s ] thds: 36 tps: 41.00 qps: 1171.04 (r/w/o: 523.02/544.02/104.00) lat (ms,95%): 5813.24 err/s 11.00 reconn/s: 0.00
[ 206s ] thds: 36 tps: 23.00 qps: 828.02 (r/w/o: 362.01/406.01/60.00) lat (ms,95%): 2680.11 err/s 7.00 reconn/s: 0.00
[ 207s ] thds: 36 tps: 44.00 qps: 1175.92 (r/w/o: 518.96/528.96/127.99) lat (ms,95%): 1938.16 err/s 20.00 reconn/s: 0.00
[ 208s ] thds: 36 tps: 35.00 qps: 1125.05 (r/w/o: 505.02/534.03/86.00) lat (ms,95%): 1771.29 err/s 8.00 reconn/s: 0.00
[ 209s ] thds: 36 tps: 23.00 qps: 928.01 (r/w/o: 413.00/447.01/68.00) lat (ms,95%): 3267.19 err/s 11.00 reconn/s: 0.00
[ 210s ] thds: 36 tps: 52.00 qps: 1299.91 (r/w/o: 571.96/587.96/139.99) lat (ms,95%): 1803.47 err/s 18.00 reconn/s: 0.00
[ 211s ] thds: 36 tps: 27.00 qps: 1114.04 (r/w/o: 512.02/540.02/62.00) lat (ms,95%): 1427.08 err/s 4.00 reconn/s: 0.00
[ 212s ] thds: 36 tps: 31.00 qps: 985.03 (r/w/o: 440.01/471.02/74.00) lat (ms,95%): 1973.38 err/s 6.00 reconn/s: 0.00
[ 213s ] thds: 36 tps: 38.00 qps: 863.01 (r/w/o: 385.01/379.01/99.00) lat (ms,95%): 2320.55 err/s 12.00 reconn/s: 0.00
[ 214s ] thds: 36 tps: 41.00 qps: 898.91 (r/w/o: 402.96/400.96/94.99) lat (ms,95%): 1903.57 err/s 6.00 reconn/s: 0.00
[ 215s ] thds: 36 tps: 39.00 qps: 1431.13 (r/w/o: 648.06/679.06/104.01) lat (ms,95%): 2159.29 err/s 14.00 reconn/s: 0.00
[ 216s ] thds: 36 tps: 18.00 qps: 719.00 (r/w/o: 335.00/336.00/48.00) lat (ms,95%): 1401.61 err/s 6.00 reconn/s: 0.00
[ 217s ] thds: 36 tps: 20.00 qps: 1001.99 (r/w/o: 455.00/495.00/52.00) lat (ms,95%): 1561.52 err/s 6.00 reconn/s: 0.00
[ 218s ] thds: 36 tps: 32.00 qps: 899.00 (r/w/o: 400.00/411.00/88.00) lat (ms,95%): 3095.38 err/s 12.00 reconn/s: 0.00
[ 219s ] thds: 36 tps: 30.00 qps: 917.98 (r/w/o: 406.99/430.99/80.00) lat (ms,95%): 3326.55 err/s 10.00 reconn/s: 0.00
[ 220s ] thds: 36 tps: 52.00 qps: 1668.08 (r/w/o: 761.03/777.04/130.01) lat (ms,95%): 1280.93 err/s 13.00 reconn/s: 0.00
[ 221s ] thds: 36 tps: 39.00 qps: 853.95 (r/w/o: 379.98/375.98/97.99) lat (ms,95%): 2279.14 err/s 10.00 reconn/s: 0.00
[ 222s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 223s ] thds: 36 tps: 19.00 qps: 773.13 (r/w/o: 360.06/371.06/42.01) lat (ms,95%): 2449.36 err/s 4.00 reconn/s: 0.00
[ 224s ] thds: 36 tps: 28.00 qps: 1215.89 (r/w/o: 543.95/595.95/75.99) lat (ms,95%): 3448.53 err/s 9.00 reconn/s: 0.00
[ 225s ] thds: 36 tps: 32.01 qps: 956.15 (r/w/o: 434.07/440.07/82.01) lat (ms,95%): 3511.19 err/s 9.00 reconn/s: 0.00
[ 226s ] thds: 36 tps: 29.00 qps: 813.98 (r/w/o: 371.99/371.99/70.00) lat (ms,95%): 4599.99 err/s 6.00 reconn/s: 0.00
[ 227s ] thds: 36 tps: 36.00 qps: 1051.14 (r/w/o: 476.06/481.06/94.01) lat (ms,95%): 2320.55 err/s 11.00 reconn/s: 0.00
[ 228s ] thds: 36 tps: 28.00 qps: 395.96 (r/w/o: 165.99/161.99/67.99) lat (ms,95%): 2362.72 err/s 6.00 reconn/s: 0.00
[ 229s ] thds: 36 tps: 5.00 qps: 729.91 (r/w/o: 346.96/372.96/10.00) lat (ms,95%): 1235.62 err/s 0.00 reconn/s: 0.00
[ 230s ] thds: 36 tps: 27.00 qps: 907.08 (r/w/o: 413.04/426.04/68.01) lat (ms,95%): 3095.38 err/s 7.00 reconn/s: 0.00
[ 231s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 232s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 233s ] thds: 36 tps: 25.00 qps: 760.00 (r/w/o: 341.00/357.00/62.00) lat (ms,95%): 4943.53 err/s 6.00 reconn/s: 0.00
[ 234s ] thds: 36 tps: 2.00 qps: 45.00 (r/w/o: 26.00/15.00/4.00) lat (ms,95%): 960.30 err/s 0.00 reconn/s: 0.00
[ 235s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 236s ] thds: 36 tps: 26.00 qps: 1047.07 (r/w/o: 470.03/511.03/66.00) lat (ms,95%): 8484.79 err/s 8.00 reconn/s: 0.00
[ 237s ] thds: 36 tps: 42.00 qps: 1263.01 (r/w/o: 569.01/584.01/110.00) lat (ms,95%): 3841.98 err/s 13.00 reconn/s: 0.00
[ 238s ] thds: 36 tps: 20.00 qps: 870.02 (r/w/o: 404.01/416.01/50.00) lat (ms,95%): 5033.35 err/s 6.00 reconn/s: 0.00
[ 239s ] thds: 36 tps: 29.00 qps: 945.09 (r/w/o: 429.04/448.04/68.01) lat (ms,95%): 2405.65 err/s 5.00 reconn/s: 0.00
[ 240s ] thds: 36 tps: 56.99 qps: 1321.84 (r/w/o: 577.93/603.93/139.98) lat (ms,95%): 1973.38 err/s 13.00 reconn/s: 0.00
[ 241s ] thds: 36 tps: 31.00 qps: 1704.82 (r/w/o: 798.92/837.91/67.99) lat (ms,95%): 1427.08 err/s 4.00 reconn/s: 0.00
[ 242s ] thds: 36 tps: 43.01 qps: 1420.23 (r/w/o: 634.10/678.11/108.02) lat (ms,95%): 1506.29 err/s 11.00 reconn/s: 0.00
[ 243s ] thds: 36 tps: 53.00 qps: 1767.02 (r/w/o: 796.01/845.01/126.00) lat (ms,95%): 1533.66 err/s 10.00 reconn/s: 0.00
[ 244s ] thds: 36 tps: 39.00 qps: 1257.89 (r/w/o: 562.95/604.95/89.99) lat (ms,95%): 943.16 err/s 6.00 reconn/s: 0.00
[ 245s ] thds: 36 tps: 26.00 qps: 808.95 (r/w/o: 365.98/376.98/66.00) lat (ms,95%): 1453.01 err/s 7.00 reconn/s: 0.00
[ 246s ] thds: 36 tps: 54.00 qps: 1563.10 (r/w/o: 700.04/705.04/158.01) lat (ms,95%): 1771.29 err/s 25.00 reconn/s: 0.00
[ 247s ] thds: 36 tps: 57.99 qps: 1465.86 (r/w/o: 651.94/665.93/147.99) lat (ms,95%): 1235.62 err/s 23.00 reconn/s: 0.00
[ 248s ] thds: 36 tps: 47.00 qps: 1989.17 (r/w/o: 925.08/922.08/142.01) lat (ms,95%): 1352.03 err/s 19.00 reconn/s: 0.00
[ 249s ] thds: 36 tps: 47.00 qps: 1229.01 (r/w/o: 553.00/554.00/122.00) lat (ms,95%): 1533.66 err/s 14.00 reconn/s: 0.00
[ 250s ] thds: 36 tps: 24.00 qps: 1081.01 (r/w/o: 488.00/521.00/72.00) lat (ms,95%): 1903.57 err/s 12.00 reconn/s: 0.00
[ 251s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 252s ] thds: 36 tps: 26.00 qps: 1095.93 (r/w/o: 495.97/531.97/68.00) lat (ms,95%): 3040.14 err/s 8.00 reconn/s: 0.00
[ 253s ] thds: 36 tps: 36.00 qps: 1219.09 (r/w/o: 543.04/588.04/88.01) lat (ms,95%): 3511.19 err/s 8.00 reconn/s: 0.00
[ 254s ] thds: 36 tps: 62.00 qps: 1329.96 (r/w/o: 589.98/591.98/148.00) lat (ms,95%): 1453.01 err/s 12.00 reconn/s: 0.00
[ 255s ] thds: 36 tps: 39.00 qps: 1728.95 (r/w/o: 799.98/828.97/100.00) lat (ms,95%): 1089.30 err/s 13.00 reconn/s: 0.00
[ 256s ] thds: 36 tps: 53.00 qps: 1282.08 (r/w/o: 558.03/580.04/144.01) lat (ms,95%): 1479.41 err/s 19.00 reconn/s: 0.00
[ 257s ] thds: 36 tps: 41.00 qps: 1728.90 (r/w/o: 797.95/826.95/103.99) lat (ms,95%): 1771.29 err/s 11.00 reconn/s: 0.00
[ 258s ] thds: 36 tps: 19.00 qps: 149.00 (r/w/o: 55.00/48.00/46.00) lat (ms,95%): 1506.29 err/s 4.00 reconn/s: 0.00
[ 259s ] thds: 36 tps: 28.00 qps: 1030.00 (r/w/o: 470.00/486.00/74.00) lat (ms,95%): 2320.55 err/s 9.00 reconn/s: 0.00
[ 260s ] thds: 36 tps: 13.00 qps: 782.04 (r/w/o: 369.02/383.02/30.00) lat (ms,95%): 2585.31 err/s 2.00 reconn/s: 0.00
[ 261s ] thds: 36 tps: 27.00 qps: 355.98 (r/w/o: 145.99/143.99/66.00) lat (ms,95%): 3982.86 err/s 6.00 reconn/s: 0.00
[ 262s ] thds: 36 tps: 33.00 qps: 1440.08 (r/w/o: 661.04/689.04/90.01) lat (ms,95%): 2585.31 err/s 12.00 reconn/s: 0.00
[ 263s ] thds: 36 tps: 56.99 qps: 1947.80 (r/w/o: 885.91/923.90/137.99) lat (ms,95%): 1533.66 err/s 12.00 reconn/s: 0.00
[ 264s ] thds: 36 tps: 43.00 qps: 1378.01 (r/w/o: 632.00/642.00/104.00) lat (ms,95%): 1401.61 err/s 9.00 reconn/s: 0.00
[ 265s ] thds: 36 tps: 32.00 qps: 1021.01 (r/w/o: 458.00/473.00/90.00) lat (ms,95%): 1401.61 err/s 13.00 reconn/s: 0.00
[ 266s ] thds: 36 tps: 49.00 qps: 1345.11 (r/w/o: 602.05/617.05/126.01) lat (ms,95%): 1869.60 err/s 14.00 reconn/s: 0.00
[ 267s ] thds: 36 tps: 51.00 qps: 1491.08 (r/w/o: 672.04/685.04/134.01) lat (ms,95%): 1708.63 err/s 16.00 reconn/s: 0.00
[ 268s ] thds: 36 tps: 51.00 qps: 1306.89 (r/w/o: 585.95/594.95/125.99) lat (ms,95%): 1170.65 err/s 12.00 reconn/s: 0.00
[ 269s ] thds: 36 tps: 52.00 qps: 1867.06 (r/w/o: 838.03/897.03/132.00) lat (ms,95%): 1129.24 err/s 14.00 reconn/s: 0.00
[ 270s ] thds: 36 tps: 33.00 qps: 1088.03 (r/w/o: 491.01/513.01/84.00) lat (ms,95%): 1479.41 err/s 9.00 reconn/s: 0.00
[ 271s ] thds: 36 tps: 40.99 qps: 1410.81 (r/w/o: 634.91/659.91/115.98) lat (ms,95%): 2009.23 err/s 17.00 reconn/s: 0.00
[ 272s ] thds: 36 tps: 34.00 qps: 1000.07 (r/w/o: 443.03/467.03/90.01) lat (ms,95%): 1869.60 err/s 11.00 reconn/s: 0.00
[ 273s ] thds: 36 tps: 19.00 qps: 567.02 (r/w/o: 250.01/277.01/40.00) lat (ms,95%): 2045.74 err/s 1.00 reconn/s: 0.00
[ 274s ] thds: 36 tps: 28.00 qps: 934.94 (r/w/o: 414.97/439.97/79.99) lat (ms,95%): 2405.65 err/s 12.00 reconn/s: 0.00
[ 275s ] thds: 36 tps: 17.00 qps: 469.02 (r/w/o: 210.01/223.01/36.00) lat (ms,95%): 2405.65 err/s 1.00 reconn/s: 0.00
[ 276s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 277s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 278s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 279s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 280s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 281s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 282s ] thds: 36 tps: 14.00 qps: 218.00 (r/w/o: 82.00/86.00/50.00) lat (ms,95%): 9118.47 err/s 11.00 reconn/s: 0.00
[ 283s ] thds: 36 tps: 32.00 qps: 1516.09 (r/w/o: 700.04/734.05/82.01) lat (ms,95%): 8955.74 err/s 9.00 reconn/s: 0.00
[ 284s ] thds: 36 tps: 47.00 qps: 1126.97 (r/w/o: 500.99/515.99/110.00) lat (ms,95%): 2120.76 err/s 8.00 reconn/s: 0.00
[ 285s ] thds: 36 tps: 53.00 qps: 1922.00 (r/w/o: 888.00/902.00/132.00) lat (ms,95%): 1427.08 err/s 14.00 reconn/s: 0.00
[ 286s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 287s ] thds: 36 tps: 23.00 qps: 498.99 (r/w/o: 218.99/221.99/58.00) lat (ms,95%): 2539.17 err/s 6.00 reconn/s: 0.00
[ 288s ] thds: 36 tps: 10.00 qps: 436.00 (r/w/o: 196.00/214.00/26.00) lat (ms,95%): 2880.27 err/s 3.00 reconn/s: 0.00
[ 289s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 290s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 291s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 292s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 293s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 294s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 295s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 296s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 297s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 298s ] thds: 36 tps: 31.00 qps: 1196.05 (r/w/o: 537.02/573.02/86.00) lat (ms,95%): 13071.47 err/s 12.00 reconn/s: 0.00
[ 299s ] thds: 36 tps: 36.00 qps: 1021.05 (r/w/o: 455.02/476.03/90.00) lat (ms,95%): 11732.86 err/s 9.00 reconn/s: 0.00
[ 300s ] thds: 36 tps: 63.99 qps: 1745.76 (r/w/o: 775.89/791.89/177.98) lat (ms,95%): 1589.90 err/s 25.00 reconn/s: 0.00
```
</details>

<details>
<summary>SQL statistics:</summary>

```console
    queries performed:
        read:                            145485
        write:                           150394
        other:                           26042
        total:                           321921
    transactions:                        10313  (34.27 per sec.)
    queries:                             321921 (1069.84 per sec.)
    ignored errors:                      2708   (9.00 per sec.)
    reconnects:                          0      (0.00 per sec.)
General statistics:
    total time:                          300.9040s
    total number of events:              10313
Latency (ms):
         min:                                    1.22
         avg:                                 1048.95
         max:                                27189.06
         95th percentile:                     2778.39
         sum:                             10817814.98
Threads fairness:
    events (avg/stddev):           286.4722/10.70
    execution time (avg/stddev):   300.4949/0.21
```
</details>
    
    
### "Минимальная" настройка - total number of events: 18124 (среднее - 60 tps)

<details>
<summary>settings</summary>

```console
shared_buffers = 16GB                  # min 128kB
#huge_pages = on
temp_buffers = 1GB
work_mem = 256MB
maintenance_work_mem = 2GB
max_connections = 36
```
</details>

  
<details>
<summary>log</summary>

```console
[ 1s ] thds: 36 tps: 31.92 qps: 1712.51 (r/w/o: 755.02/758.01/199.48) lat (ms,95%): 831.46 err/s 13.96 reconn/s: 0.00
[ 2s ] thds: 36 tps: 33.03 qps: 1156.89 (r/w/o: 521.40/567.44/68.05) lat (ms,95%): 1836.24 err/s 1.00 reconn/s: 0.00
[ 3s ] thds: 36 tps: 43.99 qps: 1153.83 (r/w/o: 512.93/536.92/103.98) lat (ms,95%): 1618.78 err/s 8.00 reconn/s: 0.00
[ 4s ] thds: 36 tps: 32.00 qps: 1607.19 (r/w/o: 746.09/775.09/86.01) lat (ms,95%): 893.56 err/s 11.00 reconn/s: 0.00
[ 5s ] thds: 36 tps: 12.00 qps: 72.00 (r/w/o: 23.00/23.00/26.00) lat (ms,95%): 2159.29 err/s 1.00 reconn/s: 0.00
[ 6s ] thds: 36 tps: 32.00 qps: 1138.04 (r/w/o: 506.02/552.02/80.00) lat (ms,95%): 2320.55 err/s 8.00 reconn/s: 0.00
[ 7s ] thds: 36 tps: 39.00 qps: 1399.11 (r/w/o: 637.05/662.05/100.01) lat (ms,95%): 2539.17 err/s 11.00 reconn/s: 0.00
[ 8s ] thds: 36 tps: 58.99 qps: 1684.70 (r/w/o: 748.87/791.86/143.97) lat (ms,95%): 1561.52 err/s 14.00 reconn/s: 0.00
[ 9s ] thds: 36 tps: 44.01 qps: 1697.21 (r/w/o: 785.10/810.10/102.01) lat (ms,95%): 1479.41 err/s 7.00 reconn/s: 0.00
[ 10s ] thds: 36 tps: 27.00 qps: 1131.92 (r/w/o: 519.96/541.96/69.99) lat (ms,95%): 1235.62 err/s 8.00 reconn/s: 0.00
[ 11s ] thds: 36 tps: 12.00 qps: 75.01 (r/w/o: 23.00/22.00/30.00) lat (ms,95%): 1869.60 err/s 3.00 reconn/s: 0.00
[ 12s ] thds: 36 tps: 42.00 qps: 1433.09 (r/w/o: 657.04/662.04/114.01) lat (ms,95%): 2405.65 err/s 16.00 reconn/s: 0.00
[ 13s ] thds: 36 tps: 78.98 qps: 1896.46 (r/w/o: 859.75/854.76/181.95) lat (ms,95%): 1327.91 err/s 12.00 reconn/s: 0.00
[ 14s ] thds: 36 tps: 37.01 qps: 1514.38 (r/w/o: 685.17/733.19/96.02) lat (ms,95%): 1069.86 err/s 11.00 reconn/s: 0.00
[ 15s ] thds: 36 tps: 58.00 qps: 1789.00 (r/w/o: 810.00/841.00/138.00) lat (ms,95%): 1069.86 err/s 12.00 reconn/s: 0.00
[ 16s ] thds: 36 tps: 22.00 qps: 787.98 (r/w/o: 347.99/381.99/58.00) lat (ms,95%): 1903.57 err/s 7.00 reconn/s: 0.00
[ 17s ] thds: 36 tps: 52.00 qps: 1493.07 (r/w/o: 669.03/690.03/134.01) lat (ms,95%): 1618.78 err/s 15.00 reconn/s: 0.00
[ 18s ] thds: 36 tps: 55.00 qps: 1486.91 (r/w/o: 660.96/691.96/133.99) lat (ms,95%): 1678.14 err/s 12.00 reconn/s: 0.00
[ 19s ] thds: 36 tps: 52.00 qps: 1500.96 (r/w/o: 678.98/691.98/130.00) lat (ms,95%): 1304.21 err/s 13.00 reconn/s: 0.00
[ 20s ] thds: 36 tps: 30.00 qps: 1393.11 (r/w/o: 635.05/678.05/80.01) lat (ms,95%): 1376.60 err/s 10.00 reconn/s: 0.00
[ 21s ] thds: 36 tps: 43.00 qps: 1332.99 (r/w/o: 604.99/619.99/108.00) lat (ms,95%): 1327.91 err/s 11.00 reconn/s: 0.00
[ 22s ] thds: 36 tps: 32.00 qps: 1140.91 (r/w/o: 520.96/533.96/85.99) lat (ms,95%): 1771.29 err/s 11.00 reconn/s: 0.00
[ 23s ] thds: 36 tps: 51.00 qps: 1750.00 (r/w/o: 798.00/834.00/118.00) lat (ms,95%): 1803.47 err/s 8.00 reconn/s: 0.00
[ 24s ] thds: 36 tps: 51.00 qps: 1679.96 (r/w/o: 738.98/804.98/136.00) lat (ms,95%): 1235.62 err/s 17.00 reconn/s: 0.00
[ 25s ] thds: 36 tps: 56.00 qps: 1566.11 (r/w/o: 699.05/719.05/148.01) lat (ms,95%): 960.30 err/s 18.00 reconn/s: 0.00
[ 26s ] thds: 36 tps: 51.00 qps: 1646.98 (r/w/o: 753.99/776.99/116.00) lat (ms,95%): 1304.21 err/s 8.00 reconn/s: 0.00
[ 27s ] thds: 36 tps: 39.00 qps: 1174.95 (r/w/o: 532.98/547.98/94.00) lat (ms,95%): 1129.24 err/s 9.00 reconn/s: 0.00
[ 28s ] thds: 36 tps: 63.01 qps: 1729.18 (r/w/o: 776.08/793.08/160.02) lat (ms,95%): 1479.41 err/s 17.00 reconn/s: 0.00
[ 29s ] thds: 36 tps: 50.00 qps: 1494.90 (r/w/o: 671.95/696.95/125.99) lat (ms,95%): 2539.17 err/s 13.00 reconn/s: 0.00
[ 30s ] thds: 36 tps: 40.00 qps: 1493.06 (r/w/o: 692.03/707.03/94.00) lat (ms,95%): 1235.62 err/s 7.00 reconn/s: 0.00
[ 31s ] thds: 36 tps: 73.00 qps: 1697.08 (r/w/o: 738.03/743.04/216.01) lat (ms,95%): 1069.86 err/s 35.00 reconn/s: 0.00
[ 32s ] thds: 36 tps: 36.00 qps: 1482.81 (r/w/o: 677.91/712.91/91.99) lat (ms,95%): 1304.21 err/s 10.00 reconn/s: 0.00
[ 33s ] thds: 36 tps: 65.01 qps: 1878.16 (r/w/o: 849.07/861.07/168.01) lat (ms,95%): 1258.08 err/s 19.00 reconn/s: 0.00
[ 34s ] thds: 36 tps: 44.00 qps: 1700.99 (r/w/o: 777.99/814.99/108.00) lat (ms,95%): 1235.62 err/s 10.00 reconn/s: 0.00
[ 35s ] thds: 36 tps: 59.99 qps: 1633.79 (r/w/o: 725.91/749.90/157.98) lat (ms,95%): 1170.65 err/s 19.00 reconn/s: 0.00
[ 36s ] thds: 36 tps: 63.00 qps: 1412.06 (r/w/o: 630.03/653.03/129.01) lat (ms,95%): 1258.08 err/s 7.00 reconn/s: 0.00
[ 37s ] thds: 36 tps: 46.00 qps: 1888.04 (r/w/o: 851.02/900.02/137.00) lat (ms,95%): 1427.08 err/s 17.00 reconn/s: 0.00
[ 38s ] thds: 36 tps: 44.00 qps: 1710.09 (r/w/o: 778.04/820.04/112.01) lat (ms,95%): 1213.57 err/s 12.00 reconn/s: 0.00
[ 39s ] thds: 36 tps: 44.00 qps: 1607.00 (r/w/o: 731.00/762.00/114.00) lat (ms,95%): 1327.91 err/s 14.00 reconn/s: 0.00
[ 40s ] thds: 36 tps: 78.00 qps: 1737.94 (r/w/o: 755.97/781.97/199.99) lat (ms,95%): 1258.08 err/s 22.00 reconn/s: 0.00
[ 41s ] thds: 36 tps: 46.00 qps: 1580.01 (r/w/o: 730.00/738.00/112.00) lat (ms,95%): 1170.65 err/s 10.00 reconn/s: 0.00
[ 42s ] thds: 36 tps: 52.00 qps: 1834.10 (r/w/o: 825.05/861.05/148.01) lat (ms,95%): 1304.21 err/s 23.00 reconn/s: 0.00
[ 43s ] thds: 36 tps: 18.00 qps: 771.96 (r/w/o: 361.98/371.98/38.00) lat (ms,95%): 1352.03 err/s 1.00 reconn/s: 0.00
[ 44s ] thds: 36 tps: 51.00 qps: 1427.89 (r/w/o: 633.95/659.95/133.99) lat (ms,95%): 1903.57 err/s 16.00 reconn/s: 0.00
[ 45s ] thds: 36 tps: 60.01 qps: 1893.21 (r/w/o: 864.10/889.10/140.02) lat (ms,95%): 1352.03 err/s 11.00 reconn/s: 0.00
[ 46s ] thds: 36 tps: 65.00 qps: 1943.09 (r/w/o: 886.04/905.04/152.01) lat (ms,95%): 1032.01 err/s 12.00 reconn/s: 0.00
[ 47s ] thds: 36 tps: 62.00 qps: 1674.98 (r/w/o: 766.99/759.99/148.00) lat (ms,95%): 1069.86 err/s 13.00 reconn/s: 0.00
[ 48s ] thds: 36 tps: 40.00 qps: 1407.93 (r/w/o: 636.97/664.96/105.99) lat (ms,95%): 1129.24 err/s 13.00 reconn/s: 0.00
[ 49s ] thds: 36 tps: 40.00 qps: 1081.94 (r/w/o: 485.97/495.97/99.99) lat (ms,95%): 1589.90 err/s 11.00 reconn/s: 0.00
[ 50s ] thds: 36 tps: 55.00 qps: 1831.12 (r/w/o: 836.05/855.05/140.01) lat (ms,95%): 1304.21 err/s 16.00 reconn/s: 0.00
[ 51s ] thds: 36 tps: 54.00 qps: 1665.93 (r/w/o: 741.97/795.97/127.99) lat (ms,95%): 1304.21 err/s 10.00 reconn/s: 0.00
[ 52s ] thds: 36 tps: 44.00 qps: 1545.97 (r/w/o: 697.99/731.99/116.00) lat (ms,95%): 1327.91 err/s 14.00 reconn/s: 0.00
[ 53s ] thds: 36 tps: 57.00 qps: 1659.02 (r/w/o: 752.01/755.01/152.00) lat (ms,95%): 1032.01 err/s 19.00 reconn/s: 0.00
[ 54s ] thds: 36 tps: 59.00 qps: 1690.89 (r/w/o: 756.95/769.95/163.99) lat (ms,95%): 1327.91 err/s 23.00 reconn/s: 0.00
[ 55s ] thds: 36 tps: 39.00 qps: 1194.13 (r/w/o: 544.06/560.06/90.01) lat (ms,95%): 1506.29 err/s 6.00 reconn/s: 0.00
[ 56s ] thds: 36 tps: 46.00 qps: 1803.00 (r/w/o: 834.00/859.00/110.00) lat (ms,95%): 1903.57 err/s 10.00 reconn/s: 0.00
[ 57s ] thds: 36 tps: 63.00 qps: 1627.09 (r/w/o: 721.04/726.04/180.01) lat (ms,95%): 1304.21 err/s 28.00 reconn/s: 0.00
[ 58s ] thds: 36 tps: 55.99 qps: 1650.84 (r/w/o: 742.93/780.92/126.99) lat (ms,95%): 1304.21 err/s 8.00 reconn/s: 0.00
[ 59s ] thds: 36 tps: 54.00 qps: 1940.97 (r/w/o: 884.98/904.98/151.00) lat (ms,95%): 1032.01 err/s 21.00 reconn/s: 0.00
[ 60s ] thds: 36 tps: 51.00 qps: 1852.16 (r/w/o: 847.08/869.08/136.01) lat (ms,95%): 1213.57 err/s 17.00 reconn/s: 0.00
[ 61s ] thds: 36 tps: 1.00 qps: 319.98 (r/w/o: 155.99/161.99/2.00) lat (ms,95%): 530.08 err/s 0.00 reconn/s: 0.00
[ 62s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 63s ] thds: 36 tps: 36.00 qps: 619.99 (r/w/o: 264.99/262.99/92.00) lat (ms,95%): 3639.94 err/s 10.00 reconn/s: 0.00
[ 64s ] thds: 36 tps: 41.00 qps: 1762.05 (r/w/o: 799.02/855.02/108.00) lat (ms,95%): 3326.55 err/s 13.00 reconn/s: 0.00
[ 65s ] thds: 36 tps: 64.00 qps: 1964.89 (r/w/o: 879.95/918.95/165.99) lat (ms,95%): 1327.91 err/s 19.00 reconn/s: 0.00
[ 66s ] thds: 36 tps: 54.00 qps: 1704.01 (r/w/o: 780.00/790.00/134.00) lat (ms,95%): 926.33 err/s 14.00 reconn/s: 0.00
[ 67s ] thds: 36 tps: 73.00 qps: 1991.04 (r/w/o: 882.02/927.02/182.00) lat (ms,95%): 1149.76 err/s 18.00 reconn/s: 0.00
[ 68s ] thds: 36 tps: 20.00 qps: 1382.91 (r/w/o: 636.96/687.95/58.00) lat (ms,95%): 943.16 err/s 9.00 reconn/s: 0.00
[ 69s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 70s ] thds: 36 tps: 9.00 qps: 115.01 (r/w/o: 44.00/45.00/26.00) lat (ms,95%): 3386.99 err/s 4.00 reconn/s: 0.00
[ 71s ] thds: 36 tps: 56.00 qps: 2176.97 (r/w/o: 1006.99/1027.99/142.00) lat (ms,95%): 3386.99 err/s 15.00 reconn/s: 0.00
[ 72s ] thds: 36 tps: 47.99 qps: 1487.78 (r/w/o: 668.90/714.89/103.98) lat (ms,95%): 1235.62 err/s 4.00 reconn/s: 0.00
[ 73s ] thds: 36 tps: 88.01 qps: 2089.14 (r/w/o: 929.06/930.06/230.02) lat (ms,95%): 1050.76 err/s 27.00 reconn/s: 0.00
[ 74s ] thds: 36 tps: 50.01 qps: 2078.21 (r/w/o: 969.10/993.10/116.01) lat (ms,95%): 1258.08 err/s 9.00 reconn/s: 0.00
[ 75s ] thds: 36 tps: 51.00 qps: 1708.84 (r/w/o: 776.93/813.92/117.99) lat (ms,95%): 1109.09 err/s 8.00 reconn/s: 0.00
[ 76s ] thds: 36 tps: 45.93 qps: 1568.71 (r/w/o: 711.96/742.92/113.83) lat (ms,95%): 1352.03 err/s 10.98 reconn/s: 0.00
[ 77s ] thds: 36 tps: 64.01 qps: 1910.37 (r/w/o: 870.17/888.17/152.03) lat (ms,95%): 1376.60 err/s 12.00 reconn/s: 0.00
[ 78s ] thds: 36 tps: 62.08 qps: 1938.48 (r/w/o: 876.12/912.17/150.19) lat (ms,95%): 1089.30 err/s 14.02 reconn/s: 0.00
[ 79s ] thds: 36 tps: 50.00 qps: 1813.04 (r/w/o: 821.02/870.02/122.00) lat (ms,95%): 1213.57 err/s 11.00 reconn/s: 0.00
[ 80s ] thds: 36 tps: 64.00 qps: 1715.99 (r/w/o: 775.00/785.00/156.00) lat (ms,95%): 1213.57 err/s 14.00 reconn/s: 0.00
[ 81s ] thds: 36 tps: 60.00 qps: 1883.98 (r/w/o: 828.99/896.99/158.00) lat (ms,95%): 1170.65 err/s 19.00 reconn/s: 0.00
[ 82s ] thds: 36 tps: 54.00 qps: 1701.11 (r/w/o: 752.05/815.05/134.01) lat (ms,95%): 1235.62 err/s 13.00 reconn/s: 0.00
[ 83s ] thds: 36 tps: 54.00 qps: 1827.92 (r/w/o: 825.96/879.96/121.99) lat (ms,95%): 1352.03 err/s 7.00 reconn/s: 0.00
[ 84s ] thds: 36 tps: 50.00 qps: 1661.16 (r/w/o: 750.07/793.07/118.01) lat (ms,95%): 1170.65 err/s 9.00 reconn/s: 0.00
[ 85s ] thds: 36 tps: 60.00 qps: 1731.92 (r/w/o: 789.96/799.96/141.99) lat (ms,95%): 1376.60 err/s 11.00 reconn/s: 0.00
[ 86s ] thds: 36 tps: 54.99 qps: 2020.81 (r/w/o: 921.91/966.91/131.99) lat (ms,95%): 1453.01 err/s 11.00 reconn/s: 0.00
[ 87s ] thds: 36 tps: 59.00 qps: 1686.06 (r/w/o: 747.03/781.03/158.01) lat (ms,95%): 943.16 err/s 20.00 reconn/s: 0.00
[ 88s ] thds: 36 tps: 1.00 qps: 383.99 (r/w/o: 189.00/193.00/2.00) lat (ms,95%): 363.18 err/s 0.00 reconn/s: 0.00
[ 89s ] thds: 36 tps: 6.00 qps: 28.00 (r/w/o: 8.00/8.00/12.00) lat (ms,95%): 2728.81 err/s 0.00 reconn/s: 0.00
[ 90s ] thds: 36 tps: 68.00 qps: 2012.98 (r/w/o: 907.99/920.99/184.00) lat (ms,95%): 2880.27 err/s 24.00 reconn/s: 0.00
[ 91s ] thds: 36 tps: 55.00 qps: 1951.13 (r/w/o: 892.06/915.06/144.01) lat (ms,95%): 1304.21 err/s 17.00 reconn/s: 0.00
[ 92s ] thds: 36 tps: 71.00 qps: 1826.97 (r/w/o: 813.99/842.99/170.00) lat (ms,95%): 1213.57 err/s 15.00 reconn/s: 0.00
[ 93s ] thds: 36 tps: 51.00 qps: 1779.00 (r/w/o: 820.00/837.00/122.00) lat (ms,95%): 909.80 err/s 10.00 reconn/s: 0.00
[ 94s ] thds: 36 tps: 38.99 qps: 1382.74 (r/w/o: 624.88/665.87/91.98) lat (ms,95%): 1401.61 err/s 7.00 reconn/s: 0.00
[ 95s ] thds: 36 tps: 69.02 qps: 1968.46 (r/w/o: 891.21/903.21/174.04) lat (ms,95%): 1327.91 err/s 18.00 reconn/s: 0.00
[ 96s ] thds: 36 tps: 38.00 qps: 1250.99 (r/w/o: 570.00/593.00/88.00) lat (ms,95%): 1479.41 err/s 6.00 reconn/s: 0.00
[ 97s ] thds: 36 tps: 50.00 qps: 1893.93 (r/w/o: 864.97/896.97/132.00) lat (ms,95%): 926.33 err/s 16.00 reconn/s: 0.00
[ 98s ] thds: 36 tps: 66.99 qps: 2112.82 (r/w/o: 952.92/987.91/171.99) lat (ms,95%): 977.74 err/s 19.00 reconn/s: 0.00
[ 99s ] thds: 36 tps: 58.01 qps: 1924.21 (r/w/o: 863.10/923.10/138.02) lat (ms,95%): 960.30 err/s 11.00 reconn/s: 0.00
[ 100s ] thds: 36 tps: 57.00 qps: 1824.99 (r/w/o: 812.99/865.99/146.00) lat (ms,95%): 1304.21 err/s 18.00 reconn/s: 0.00
[ 101s ] thds: 36 tps: 66.99 qps: 1885.85 (r/w/o: 855.93/873.93/155.99) lat (ms,95%): 1089.30 err/s 11.00 reconn/s: 0.00
[ 102s ] thds: 36 tps: 19.00 qps: 576.05 (r/w/o: 256.02/276.02/44.00) lat (ms,95%): 1533.66 err/s 4.00 reconn/s: 0.00
[ 103s ] thds: 36 tps: 51.00 qps: 1657.95 (r/w/o: 763.98/769.98/124.00) lat (ms,95%): 1973.38 err/s 11.00 reconn/s: 0.00
[ 104s ] thds: 36 tps: 61.00 qps: 1770.03 (r/w/o: 811.01/815.01/144.00) lat (ms,95%): 1427.08 err/s 11.00 reconn/s: 0.00
[ 105s ] thds: 36 tps: 54.00 qps: 1924.07 (r/w/o: 867.03/925.03/132.00) lat (ms,95%): 1032.01 err/s 12.00 reconn/s: 0.00
[ 106s ] thds: 36 tps: 65.00 qps: 2066.92 (r/w/o: 928.96/975.96/161.99) lat (ms,95%): 1032.01 err/s 16.00 reconn/s: 0.00
[ 107s ] thds: 36 tps: 58.99 qps: 1684.84 (r/w/o: 765.93/782.93/135.99) lat (ms,95%): 1050.76 err/s 9.00 reconn/s: 0.00
[ 108s ] thds: 36 tps: 76.01 qps: 2164.20 (r/w/o: 980.09/998.09/186.02) lat (ms,95%): 877.61 err/s 17.00 reconn/s: 0.00
[ 109s ] thds: 36 tps: 45.00 qps: 1488.05 (r/w/o: 677.03/695.03/116.00) lat (ms,95%): 1280.93 err/s 13.00 reconn/s: 0.00
[ 110s ] thds: 36 tps: 84.98 qps: 1867.63 (r/w/o: 819.84/825.84/221.96) lat (ms,95%): 802.05 err/s 25.99 reconn/s: 0.00
[ 111s ] thds: 36 tps: 53.00 qps: 1631.09 (r/w/o: 734.04/768.04/129.01) lat (ms,95%): 1129.24 err/s 15.00 reconn/s: 0.00
[ 112s ] thds: 36 tps: 50.01 qps: 2005.28 (r/w/o: 921.13/939.13/145.02) lat (ms,95%): 1213.57 err/s 20.00 reconn/s: 0.00
[ 113s ] thds: 36 tps: 62.00 qps: 1933.95 (r/w/o: 866.98/902.97/164.00) lat (ms,95%): 1170.65 err/s 20.00 reconn/s: 0.00
[ 114s ] thds: 36 tps: 68.00 qps: 2063.01 (r/w/o: 925.00/974.00/164.00) lat (ms,95%): 1149.76 err/s 14.00 reconn/s: 0.00
[ 115s ] thds: 36 tps: 63.00 qps: 1902.05 (r/w/o: 858.02/886.02/158.00) lat (ms,95%): 846.57 err/s 16.00 reconn/s: 0.00
[ 116s ] thds: 36 tps: 57.00 qps: 1489.99 (r/w/o: 671.00/683.00/136.00) lat (ms,95%): 1618.78 err/s 11.00 reconn/s: 0.00
[ 117s ] thds: 36 tps: 63.99 qps: 2135.83 (r/w/o: 968.92/1004.92/161.99) lat (ms,95%): 995.51 err/s 18.00 reconn/s: 0.00
[ 118s ] thds: 36 tps: 49.00 qps: 1991.90 (r/w/o: 915.95/947.95/127.99) lat (ms,95%): 1069.86 err/s 15.00 reconn/s: 0.00
[ 119s ] thds: 36 tps: 77.00 qps: 1742.07 (r/w/o: 765.03/789.03/188.01) lat (ms,95%): 1050.76 err/s 17.00 reconn/s: 0.00
[ 120s ] thds: 36 tps: 50.00 qps: 1692.96 (r/w/o: 768.98/801.98/122.00) lat (ms,95%): 1089.30 err/s 11.00 reconn/s: 0.00
[ 121s ] thds: 36 tps: 70.00 qps: 2242.95 (r/w/o: 1005.98/1048.98/188.00) lat (ms,95%): 1170.65 err/s 24.00 reconn/s: 0.00
[ 122s ] thds: 36 tps: 32.00 qps: 1268.14 (r/w/o: 580.07/608.07/80.01) lat (ms,95%): 657.93 err/s 8.00 reconn/s: 0.00
[ 123s ] thds: 36 tps: 83.99 qps: 2007.86 (r/w/o: 888.94/890.94/227.98) lat (ms,95%): 1235.62 err/s 30.00 reconn/s: 0.00
[ 124s ] thds: 36 tps: 50.00 qps: 2193.16 (r/w/o: 1006.07/1067.08/120.01) lat (ms,95%): 1258.08 err/s 12.00 reconn/s: 0.00
[ 125s ] thds: 36 tps: 65.00 qps: 2082.06 (r/w/o: 944.03/984.03/154.00) lat (ms,95%): 1013.60 err/s 12.00 reconn/s: 0.00
[ 126s ] thds: 36 tps: 66.00 qps: 1996.85 (r/w/o: 894.93/927.93/173.99) lat (ms,95%): 943.16 err/s 23.00 reconn/s: 0.00
[ 127s ] thds: 36 tps: 57.00 qps: 2195.12 (r/w/o: 997.05/1062.06/136.01) lat (ms,95%): 1170.65 err/s 11.00 reconn/s: 0.00
[ 128s ] thds: 36 tps: 74.00 qps: 2284.91 (r/w/o: 1030.96/1067.96/185.99) lat (ms,95%): 926.33 err/s 21.00 reconn/s: 0.00
[ 129s ] thds: 36 tps: 46.00 qps: 1501.04 (r/w/o: 682.02/705.02/114.00) lat (ms,95%): 1352.03 err/s 11.00 reconn/s: 0.00
[ 130s ] thds: 36 tps: 81.00 qps: 2010.89 (r/w/o: 908.95/897.95/203.99) lat (ms,95%): 816.63 err/s 21.00 reconn/s: 0.00
[ 131s ] thds: 36 tps: 76.00 qps: 2308.05 (r/w/o: 1054.02/1068.02/186.00) lat (ms,95%): 1069.86 err/s 20.00 reconn/s: 0.00
[ 132s ] thds: 36 tps: 65.99 qps: 2158.71 (r/w/o: 951.87/1034.86/171.98) lat (ms,95%): 1032.01 err/s 20.00 reconn/s: 0.00
[ 133s ] thds: 36 tps: 52.01 qps: 1676.21 (r/w/o: 758.09/786.10/132.02) lat (ms,95%): 1050.76 err/s 14.00 reconn/s: 0.00
[ 134s ] thds: 36 tps: 75.00 qps: 1783.95 (r/w/o: 807.98/793.98/181.99) lat (ms,95%): 1069.86 err/s 16.00 reconn/s: 0.00
[ 135s ] thds: 36 tps: 53.00 qps: 1777.10 (r/w/o: 817.05/822.05/138.01) lat (ms,95%): 943.16 err/s 16.00 reconn/s: 0.00
[ 136s ] thds: 36 tps: 62.00 qps: 1650.08 (r/w/o: 732.04/740.04/178.01) lat (ms,95%): 1401.61 err/s 27.00 reconn/s: 0.00
[ 137s ] thds: 36 tps: 59.00 qps: 1952.85 (r/w/o: 887.93/912.93/151.99) lat (ms,95%): 995.51 err/s 17.00 reconn/s: 0.00
[ 138s ] thds: 36 tps: 81.00 qps: 2242.11 (r/w/o: 1001.05/1047.05/194.01) lat (ms,95%): 1109.09 err/s 16.00 reconn/s: 0.00
[ 139s ] thds: 36 tps: 69.00 qps: 2095.04 (r/w/o: 954.02/973.02/168.00) lat (ms,95%): 926.33 err/s 16.00 reconn/s: 0.00
[ 140s ] thds: 36 tps: 72.00 qps: 2164.98 (r/w/o: 968.99/1013.99/182.00) lat (ms,95%): 1089.30 err/s 19.00 reconn/s: 0.00
[ 141s ] thds: 36 tps: 63.00 qps: 2045.91 (r/w/o: 920.96/960.96/163.99) lat (ms,95%): 977.74 err/s 20.00 reconn/s: 0.00
[ 142s ] thds: 36 tps: 14.00 qps: 583.96 (r/w/o: 267.98/277.98/38.00) lat (ms,95%): 995.51 err/s 5.00 reconn/s: 0.00
[ 143s ] thds: 36 tps: 43.00 qps: 982.09 (r/w/o: 424.04/442.04/116.01) lat (ms,95%): 2159.29 err/s 15.00 reconn/s: 0.00
[ 144s ] thds: 36 tps: 60.99 qps: 1958.65 (r/w/o: 879.84/914.83/163.97) lat (ms,95%): 2009.23 err/s 21.00 reconn/s: 0.00
[ 145s ] thds: 36 tps: 66.02 qps: 2115.49 (r/w/o: 954.22/997.23/164.04) lat (ms,95%): 1191.92 err/s 16.00 reconn/s: 0.00
[ 146s ] thds: 36 tps: 55.00 qps: 1530.96 (r/w/o: 673.98/710.98/146.00) lat (ms,95%): 1170.65 err/s 18.00 reconn/s: 0.00
[ 147s ] thds: 36 tps: 55.00 qps: 1976.93 (r/w/o: 915.97/926.97/134.00) lat (ms,95%): 1327.91 err/s 12.00 reconn/s: 0.00
[ 148s ] thds: 36 tps: 59.00 qps: 1710.06 (r/w/o: 765.03/805.03/140.01) lat (ms,95%): 1069.86 err/s 12.00 reconn/s: 0.00
[ 149s ] thds: 36 tps: 68.99 qps: 1887.74 (r/w/o: 840.89/860.88/185.97) lat (ms,95%): 1149.76 err/s 25.00 reconn/s: 0.00
[ 150s ] thds: 36 tps: 50.00 qps: 1270.97 (r/w/o: 559.99/580.99/130.00) lat (ms,95%): 773.68 err/s 15.00 reconn/s: 0.00
[ 151s ] thds: 36 tps: 38.00 qps: 1117.08 (r/w/o: 503.04/514.04/100.01) lat (ms,95%): 1836.24 err/s 12.00 reconn/s: 0.00
[ 152s ] thds: 36 tps: 74.00 qps: 1918.98 (r/w/o: 857.99/863.99/197.00) lat (ms,95%): 1708.63 err/s 25.00 reconn/s: 0.00
[ 153s ] thds: 36 tps: 54.00 qps: 1940.06 (r/w/o: 875.03/928.03/137.00) lat (ms,95%): 1170.65 err/s 14.00 reconn/s: 0.00
[ 154s ] thds: 36 tps: 60.00 qps: 2006.96 (r/w/o: 896.98/947.98/162.00) lat (ms,95%): 1213.57 err/s 23.00 reconn/s: 0.00
[ 155s ] thds: 36 tps: 76.00 qps: 2095.05 (r/w/o: 945.02/974.03/176.00) lat (ms,95%): 846.57 err/s 12.00 reconn/s: 0.00
[ 156s ] thds: 36 tps: 80.00 qps: 2167.90 (r/w/o: 954.96/1002.95/209.99) lat (ms,95%): 960.30 err/s 25.00 reconn/s: 0.00
[ 157s ] thds: 36 tps: 48.01 qps: 1953.24 (r/w/o: 876.11/959.12/118.01) lat (ms,95%): 1304.21 err/s 12.00 reconn/s: 0.00
[ 158s ] thds: 36 tps: 52.00 qps: 1426.94 (r/w/o: 640.97/657.97/127.99) lat (ms,95%): 1479.41 err/s 12.00 reconn/s: 0.00
[ 159s ] thds: 36 tps: 54.00 qps: 1929.93 (r/w/o: 888.97/910.97/130.00) lat (ms,95%): 893.56 err/s 11.00 reconn/s: 0.00
[ 160s ] thds: 36 tps: 80.00 qps: 2139.13 (r/w/o: 955.06/978.06/206.01) lat (ms,95%): 1149.76 err/s 23.00 reconn/s: 0.00
[ 161s ] thds: 36 tps: 64.00 qps: 2130.88 (r/w/o: 971.95/1004.95/153.99) lat (ms,95%): 1109.09 err/s 13.00 reconn/s: 0.00
[ 162s ] thds: 36 tps: 75.00 qps: 2126.93 (r/w/o: 959.97/982.97/183.99) lat (ms,95%): 802.05 err/s 17.00 reconn/s: 0.00
[ 163s ] thds: 36 tps: 63.00 qps: 2226.17 (r/w/o: 1014.08/1068.08/144.01) lat (ms,95%): 1129.24 err/s 9.00 reconn/s: 0.00
[ 164s ] thds: 36 tps: 86.00 qps: 2289.90 (r/w/o: 1026.96/1040.96/221.99) lat (ms,95%): 787.74 err/s 25.00 reconn/s: 0.00
[ 165s ] thds: 36 tps: 54.00 qps: 2031.05 (r/w/o: 932.02/967.03/132.00) lat (ms,95%): 1191.92 err/s 12.00 reconn/s: 0.00
[ 166s ] thds: 36 tps: 78.99 qps: 1954.72 (r/w/o: 866.88/885.87/201.97) lat (ms,95%): 943.16 err/s 22.00 reconn/s: 0.00
[ 167s ] thds: 36 tps: 80.01 qps: 2683.41 (r/w/o: 1220.19/1263.19/200.03) lat (ms,95%): 861.95 err/s 21.00 reconn/s: 0.00
[ 168s ] thds: 36 tps: 65.00 qps: 1960.09 (r/w/o: 877.04/923.04/160.01) lat (ms,95%): 893.56 err/s 16.00 reconn/s: 0.00
[ 169s ] thds: 36 tps: 45.00 qps: 2063.80 (r/w/o: 956.91/1000.90/105.99) lat (ms,95%): 1280.93 err/s 8.00 reconn/s: 0.00
[ 170s ] thds: 36 tps: 99.01 qps: 2603.16 (r/w/o: 1161.07/1182.07/260.02) lat (ms,95%): 877.61 err/s 31.00 reconn/s: 0.00
[ 171s ] thds: 36 tps: 17.00 qps: 1196.82 (r/w/o: 535.92/606.91/53.99) lat (ms,95%): 450.77 err/s 10.00 reconn/s: 0.00
[ 172s ] thds: 36 tps: 37.01 qps: 499.09 (r/w/o: 210.04/201.04/88.02) lat (ms,95%): 2045.74 err/s 7.00 reconn/s: 0.00
[ 173s ] thds: 36 tps: 44.99 qps: 1826.80 (r/w/o: 846.91/879.90/99.99) lat (ms,95%): 2585.31 err/s 5.00 reconn/s: 0.00
[ 174s ] thds: 36 tps: 84.01 qps: 2326.17 (r/w/o: 1043.07/1075.08/208.01) lat (ms,95%): 802.05 err/s 22.00 reconn/s: 0.00
[ 175s ] thds: 36 tps: 63.00 qps: 2035.89 (r/w/o: 928.95/948.95/157.99) lat (ms,95%): 893.56 err/s 16.00 reconn/s: 0.00
[ 176s ] thds: 36 tps: 68.00 qps: 2124.99 (r/w/o: 955.99/994.99/174.00) lat (ms,95%): 1191.92 err/s 19.00 reconn/s: 0.00
[ 177s ] thds: 36 tps: 74.00 qps: 2556.94 (r/w/o: 1164.97/1209.97/182.00) lat (ms,95%): 977.74 err/s 18.00 reconn/s: 0.00
[ 178s ] thds: 36 tps: 80.01 qps: 2499.31 (r/w/o: 1116.14/1165.14/218.03) lat (ms,95%): 816.63 err/s 30.00 reconn/s: 0.00
[ 179s ] thds: 36 tps: 28.00 qps: 1471.85 (r/w/o: 674.93/714.93/81.99) lat (ms,95%): 960.30 err/s 13.00 reconn/s: 0.00
[ 180s ] thds: 36 tps: 16.00 qps: 177.01 (r/w/o: 70.00/67.00/40.00) lat (ms,95%): 2009.23 err/s 4.00 reconn/s: 0.00
[ 181s ] thds: 36 tps: 66.00 qps: 2160.01 (r/w/o: 988.00/1020.00/152.00) lat (ms,95%): 2320.55 err/s 11.00 reconn/s: 0.00
[ 182s ] thds: 36 tps: 74.99 qps: 2367.57 (r/w/o: 1071.81/1107.80/187.97) lat (ms,95%): 733.00 err/s 19.00 reconn/s: 0.00
[ 183s ] thds: 36 tps: 73.02 qps: 2240.47 (r/w/o: 1001.21/1035.22/204.04) lat (ms,95%): 773.68 err/s 29.01 reconn/s: 0.00
[ 184s ] thds: 36 tps: 67.00 qps: 2286.91 (r/w/o: 1044.96/1091.95/149.99) lat (ms,95%): 977.74 err/s 8.00 reconn/s: 0.00
[ 185s ] thds: 36 tps: 84.00 qps: 2522.04 (r/w/o: 1147.02/1167.02/208.00) lat (ms,95%): 846.57 err/s 20.00 reconn/s: 0.00
[ 186s ] thds: 36 tps: 71.00 qps: 2127.05 (r/w/o: 961.02/986.02/180.00) lat (ms,95%): 943.16 err/s 19.00 reconn/s: 0.00
[ 187s ] thds: 36 tps: 53.00 qps: 1474.96 (r/w/o: 658.98/683.98/132.00) lat (ms,95%): 1280.93 err/s 13.00 reconn/s: 0.00
[ 188s ] thds: 36 tps: 75.00 qps: 2244.09 (r/w/o: 1019.04/1011.04/214.01) lat (ms,95%): 960.30 err/s 32.00 reconn/s: 0.00
[ 189s ] thds: 36 tps: 58.99 qps: 2040.79 (r/w/o: 936.90/971.90/131.99) lat (ms,95%): 1129.24 err/s 7.00 reconn/s: 0.00
[ 190s ] thds: 36 tps: 66.00 qps: 2031.01 (r/w/o: 914.00/949.00/168.00) lat (ms,95%): 960.30 err/s 18.00 reconn/s: 0.00
[ 191s ] thds: 36 tps: 87.01 qps: 2233.22 (r/w/o: 992.10/1025.10/216.02) lat (ms,95%): 995.51 err/s 23.00 reconn/s: 0.00
[ 192s ] thds: 36 tps: 71.00 qps: 2222.99 (r/w/o: 1028.99/1017.99/176.00) lat (ms,95%): 943.16 err/s 17.00 reconn/s: 0.00
[ 193s ] thds: 36 tps: 79.99 qps: 2376.77 (r/w/o: 1066.90/1105.89/203.98) lat (ms,95%): 893.56 err/s 23.00 reconn/s: 0.00
[ 194s ] thds: 36 tps: 24.00 qps: 1271.10 (r/w/o: 574.04/631.05/66.01) lat (ms,95%): 1109.09 err/s 9.00 reconn/s: 0.00
[ 195s ] thds: 36 tps: 91.99 qps: 2517.76 (r/w/o: 1137.89/1161.89/217.98) lat (ms,95%): 1561.52 err/s 17.00 reconn/s: 0.00
[ 196s ] thds: 36 tps: 68.01 qps: 2574.22 (r/w/o: 1182.10/1228.11/164.01) lat (ms,95%): 759.88 err/s 14.00 reconn/s: 0.00
[ 197s ] thds: 36 tps: 76.00 qps: 2490.05 (r/w/o: 1128.02/1170.02/192.00) lat (ms,95%): 995.51 err/s 20.00 reconn/s: 0.00
[ 198s ] thds: 36 tps: 94.00 qps: 2833.97 (r/w/o: 1276.98/1318.98/238.00) lat (ms,95%): 787.74 err/s 27.00 reconn/s: 0.00
[ 199s ] thds: 36 tps: 73.00 qps: 2339.01 (r/w/o: 1051.00/1094.00/194.00) lat (ms,95%): 846.57 err/s 25.00 reconn/s: 0.00
[ 200s ] thds: 36 tps: 76.00 qps: 2145.04 (r/w/o: 967.02/996.02/182.00) lat (ms,95%): 943.16 err/s 15.00 reconn/s: 0.00
[ 201s ] thds: 36 tps: 42.00 qps: 1296.98 (r/w/o: 583.99/610.99/102.00) lat (ms,95%): 1376.60 err/s 9.00 reconn/s: 0.00
[ 202s ] thds: 36 tps: 60.00 qps: 2477.02 (r/w/o: 1138.01/1185.01/154.00) lat (ms,95%): 943.16 err/s 18.00 reconn/s: 0.00
[ 203s ] thds: 36 tps: 64.00 qps: 2277.99 (r/w/o: 1043.00/1081.00/154.00) lat (ms,95%): 960.30 err/s 14.00 reconn/s: 0.00
[ 204s ] thds: 36 tps: 72.00 qps: 2499.06 (r/w/o: 1118.03/1197.03/184.00) lat (ms,95%): 893.56 err/s 20.00 reconn/s: 0.00
[ 205s ] thds: 36 tps: 67.00 qps: 2131.99 (r/w/o: 961.00/997.00/174.00) lat (ms,95%): 877.61 err/s 21.00 reconn/s: 0.00
[ 206s ] thds: 36 tps: 87.99 qps: 2543.70 (r/w/o: 1157.86/1173.86/211.98) lat (ms,95%): 977.74 err/s 18.00 reconn/s: 0.00
[ 207s ] thds: 36 tps: 74.00 qps: 2361.99 (r/w/o: 1072.00/1110.00/180.00) lat (ms,95%): 816.63 err/s 16.00 reconn/s: 0.00
[ 208s ] thds: 36 tps: 43.00 qps: 1339.13 (r/w/o: 606.06/633.06/100.01) lat (ms,95%): 1213.57 err/s 7.00 reconn/s: 0.00
[ 209s ] thds: 36 tps: 90.00 qps: 2599.09 (r/w/o: 1171.04/1194.04/234.01) lat (ms,95%): 846.57 err/s 29.00 reconn/s: 0.00
[ 210s ] thds: 36 tps: 71.99 qps: 2650.75 (r/w/o: 1209.88/1266.88/173.98) lat (ms,95%): 816.63 err/s 15.00 reconn/s: 0.00
[ 211s ] thds: 36 tps: 88.00 qps: 2806.12 (r/w/o: 1248.05/1328.06/230.01) lat (ms,95%): 1013.60 err/s 27.00 reconn/s: 0.00
[ 212s ] thds: 36 tps: 83.00 qps: 2751.13 (r/w/o: 1257.06/1298.06/196.01) lat (ms,95%): 960.30 err/s 16.00 reconn/s: 0.00
[ 213s ] thds: 36 tps: 85.00 qps: 2644.02 (r/w/o: 1194.01/1222.01/228.00) lat (ms,95%): 669.89 err/s 29.00 reconn/s: 0.00
[ 214s ] thds: 36 tps: 38.99 qps: 1455.79 (r/w/o: 655.91/697.90/101.99) lat (ms,95%): 1069.86 err/s 12.00 reconn/s: 0.00
[ 215s ] thds: 36 tps: 38.00 qps: 979.05 (r/w/o: 443.02/442.02/94.00) lat (ms,95%): 1561.52 err/s 10.00 reconn/s: 0.00
[ 216s ] thds: 36 tps: 73.00 qps: 2416.07 (r/w/o: 1102.03/1128.03/186.01) lat (ms,95%): 1213.57 err/s 21.00 reconn/s: 0.00
[ 217s ] thds: 36 tps: 73.00 qps: 2242.04 (r/w/o: 1010.02/1056.02/176.00) lat (ms,95%): 960.30 err/s 15.00 reconn/s: 0.00
[ 218s ] thds: 36 tps: 75.00 qps: 2358.84 (r/w/o: 1061.93/1104.93/191.99) lat (ms,95%): 816.63 err/s 21.00 reconn/s: 0.00
[ 219s ] thds: 36 tps: 75.00 qps: 2156.06 (r/w/o: 969.03/989.03/198.01) lat (ms,95%): 1032.01 err/s 25.00 reconn/s: 0.00
[ 220s ] thds: 36 tps: 76.00 qps: 2336.07 (r/w/o: 1054.03/1090.03/192.01) lat (ms,95%): 977.74 err/s 20.00 reconn/s: 0.00
[ 221s ] thds: 36 tps: 73.00 qps: 2073.90 (r/w/o: 936.95/940.95/195.99) lat (ms,95%): 926.33 err/s 25.00 reconn/s: 0.00
[ 222s ] thds: 36 tps: 42.00 qps: 1738.18 (r/w/o: 806.08/840.09/92.01) lat (ms,95%): 1352.03 err/s 5.00 reconn/s: 0.00
[ 223s ] thds: 36 tps: 49.00 qps: 1398.97 (r/w/o: 622.99/643.98/132.00) lat (ms,95%): 1258.08 err/s 17.00 reconn/s: 0.00
[ 224s ] thds: 36 tps: 74.99 qps: 2253.80 (r/w/o: 1015.91/1045.91/191.98) lat (ms,95%): 1213.57 err/s 21.00 reconn/s: 0.00
[ 225s ] thds: 36 tps: 77.00 qps: 2479.06 (r/w/o: 1130.03/1161.03/188.00) lat (ms,95%): 926.33 err/s 17.00 reconn/s: 0.00
[ 226s ] thds: 36 tps: 63.00 qps: 2204.17 (r/w/o: 986.08/1042.08/176.01) lat (ms,95%): 893.56 err/s 26.00 reconn/s: 0.00
[ 227s ] thds: 36 tps: 80.00 qps: 2375.02 (r/w/o: 1073.01/1098.01/204.00) lat (ms,95%): 861.95 err/s 22.00 reconn/s: 0.00
[ 228s ] thds: 36 tps: 73.00 qps: 2282.85 (r/w/o: 1042.93/1049.93/189.99) lat (ms,95%): 816.63 err/s 23.00 reconn/s: 0.00
[ 229s ] thds: 36 tps: 98.00 qps: 2804.02 (r/w/o: 1270.01/1302.01/232.00) lat (ms,95%): 707.07 err/s 19.00 reconn/s: 0.00
[ 230s ] thds: 36 tps: 34.00 qps: 1187.99 (r/w/o: 539.99/565.99/82.00) lat (ms,95%): 1170.65 err/s 7.00 reconn/s: 0.00
[ 231s ] thds: 36 tps: 64.00 qps: 2359.84 (r/w/o: 1076.93/1120.92/161.99) lat (ms,95%): 1506.29 err/s 17.00 reconn/s: 0.00
[ 232s ] thds: 36 tps: 78.00 qps: 2561.14 (r/w/o: 1166.06/1207.06/188.01) lat (ms,95%): 926.33 err/s 16.00 reconn/s: 0.00
[ 233s ] thds: 36 tps: 98.00 qps: 2551.94 (r/w/o: 1143.97/1157.97/249.99) lat (ms,95%): 759.88 err/s 28.00 reconn/s: 0.00
[ 234s ] thds: 36 tps: 64.00 qps: 2410.89 (r/w/o: 1083.95/1168.95/157.99) lat (ms,95%): 1050.76 err/s 15.00 reconn/s: 0.00
[ 235s ] thds: 36 tps: 96.02 qps: 2546.41 (r/w/o: 1141.18/1167.19/238.04) lat (ms,95%): 773.68 err/s 23.00 reconn/s: 0.00
[ 236s ] thds: 36 tps: 82.99 qps: 2773.72 (r/w/o: 1264.87/1311.87/196.98) lat (ms,95%): 909.80 err/s 18.00 reconn/s: 0.00
[ 237s ] thds: 36 tps: 29.00 qps: 1232.03 (r/w/o: 561.01/594.02/77.00) lat (ms,95%): 733.00 err/s 7.00 reconn/s: 0.00
[ 238s ] thds: 36 tps: 63.99 qps: 1911.82 (r/w/o: 864.92/876.92/169.98) lat (ms,95%): 1506.29 err/s 21.00 reconn/s: 0.00
[ 239s ] thds: 36 tps: 84.01 qps: 2351.29 (r/w/o: 1054.13/1093.13/204.02) lat (ms,95%): 926.33 err/s 19.00 reconn/s: 0.00
[ 240s ] thds: 36 tps: 83.00 qps: 2738.88 (r/w/o: 1231.94/1296.94/209.99) lat (ms,95%): 831.46 err/s 24.00 reconn/s: 0.00
[ 241s ] thds: 36 tps: 73.00 qps: 2354.13 (r/w/o: 1067.06/1115.06/172.01) lat (ms,95%): 746.32 err/s 13.00 reconn/s: 0.00
[ 242s ] thds: 36 tps: 73.00 qps: 2376.07 (r/w/o: 1067.03/1141.03/168.01) lat (ms,95%): 1013.60 err/s 12.00 reconn/s: 0.00
[ 243s ] thds: 36 tps: 91.00 qps: 2597.89 (r/w/o: 1159.95/1193.95/243.99) lat (ms,95%): 802.05 err/s 31.00 reconn/s: 0.00
[ 244s ] thds: 36 tps: 65.00 qps: 2341.10 (r/w/o: 1076.05/1111.05/154.01) lat (ms,95%): 802.05 err/s 13.00 reconn/s: 0.00
[ 245s ] thds: 36 tps: 75.00 qps: 2462.92 (r/w/o: 1111.96/1164.96/185.99) lat (ms,95%): 877.61 err/s 18.00 reconn/s: 0.00
[ 246s ] thds: 36 tps: 78.00 qps: 2740.98 (r/w/o: 1238.99/1325.99/176.00) lat (ms,95%): 861.95 err/s 11.00 reconn/s: 0.00
[ 247s ] thds: 36 tps: 88.99 qps: 2728.79 (r/w/o: 1226.90/1283.90/217.98) lat (ms,95%): 846.57 err/s 21.00 reconn/s: 0.00
[ 248s ] thds: 36 tps: 86.00 qps: 2802.05 (r/w/o: 1274.02/1310.02/218.00) lat (ms,95%): 787.74 err/s 23.00 reconn/s: 0.00
[ 249s ] thds: 36 tps: 77.99 qps: 2205.78 (r/w/o: 983.90/1027.90/193.98) lat (ms,95%): 926.33 err/s 19.00 reconn/s: 0.00
[ 250s ] thds: 36 tps: 81.01 qps: 2878.49 (r/w/o: 1319.22/1365.23/194.03) lat (ms,95%): 1013.60 err/s 16.00 reconn/s: 0.00
[ 251s ] thds: 36 tps: 63.99 qps: 2222.71 (r/w/o: 1000.87/1049.86/171.98) lat (ms,95%): 657.93 err/s 23.00 reconn/s: 0.00
[ 252s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 253s ] thds: 36 tps: 8.00 qps: 121.99 (r/w/o: 48.00/50.00/24.00) lat (ms,95%): 2778.39 err/s 4.00 reconn/s: 0.00
[ 254s ] thds: 36 tps: 75.00 qps: 2305.11 (r/w/o: 1055.05/1073.05/177.01) lat (ms,95%): 2880.27 err/s 14.00 reconn/s: 0.00
[ 255s ] thds: 36 tps: 73.01 qps: 2486.21 (r/w/o: 1125.10/1176.10/185.02) lat (ms,95%): 943.16 err/s 19.00 reconn/s: 0.00
[ 256s ] thds: 36 tps: 87.00 qps: 2677.93 (r/w/o: 1213.97/1255.97/207.99) lat (ms,95%): 846.57 err/s 18.00 reconn/s: 0.00
[ 257s ] thds: 36 tps: 62.00 qps: 2388.90 (r/w/o: 1077.96/1154.95/155.99) lat (ms,95%): 909.80 err/s 16.00 reconn/s: 0.00
[ 258s ] thds: 36 tps: 94.01 qps: 2939.24 (r/w/o: 1337.11/1382.11/220.02) lat (ms,95%): 816.63 err/s 16.00 reconn/s: 0.00
[ 259s ] thds: 36 tps: 85.99 qps: 2493.59 (r/w/o: 1119.82/1153.81/219.96) lat (ms,95%): 669.89 err/s 25.00 reconn/s: 0.00
[ 260s ] thds: 36 tps: 60.01 qps: 2033.20 (r/w/o: 928.09/947.09/158.02) lat (ms,95%): 802.05 err/s 19.00 reconn/s: 0.00
[ 261s ] thds: 36 tps: 29.00 qps: 1074.97 (r/w/o: 477.99/504.99/92.00) lat (ms,95%): 1427.08 err/s 17.00 reconn/s: 0.00
[ 262s ] thds: 36 tps: 87.99 qps: 2613.80 (r/w/o: 1169.91/1215.91/227.98) lat (ms,95%): 1678.14 err/s 26.00 reconn/s: 0.00
[ 263s ] thds: 36 tps: 94.01 qps: 2578.20 (r/w/o: 1161.09/1201.09/216.02) lat (ms,95%): 926.33 err/s 15.00 reconn/s: 0.00
[ 264s ] thds: 36 tps: 87.01 qps: 2929.20 (r/w/o: 1331.09/1388.09/210.01) lat (ms,95%): 759.88 err/s 18.00 reconn/s: 0.00
[ 265s ] thds: 36 tps: 83.00 qps: 2653.01 (r/w/o: 1195.01/1254.01/204.00) lat (ms,95%): 733.00 err/s 19.00 reconn/s: 0.00
[ 266s ] thds: 36 tps: 97.00 qps: 2823.02 (r/w/o: 1267.01/1306.01/250.00) lat (ms,95%): 746.32 err/s 28.00 reconn/s: 0.00
[ 267s ] thds: 36 tps: 103.99 qps: 3185.56 (r/w/o: 1435.80/1499.79/249.97) lat (ms,95%): 657.93 err/s 22.00 reconn/s: 0.00
[ 268s ] thds: 36 tps: 17.00 qps: 631.04 (r/w/o: 286.02/299.02/46.00) lat (ms,95%): 1149.76 err/s 5.00 reconn/s: 0.00
[ 269s ] thds: 36 tps: 86.01 qps: 2547.17 (r/w/o: 1153.08/1170.08/224.02) lat (ms,95%): 1453.01 err/s 26.00 reconn/s: 0.00
[ 270s ] thds: 36 tps: 94.00 qps: 2935.98 (r/w/o: 1338.99/1352.99/244.00) lat (ms,95%): 773.68 err/s 28.00 reconn/s: 0.00
[ 271s ] thds: 36 tps: 106.99 qps: 3164.72 (r/w/o: 1410.88/1469.87/283.98) lat (ms,95%): 694.45 err/s 36.00 reconn/s: 0.00
[ 272s ] thds: 36 tps: 100.01 qps: 2793.26 (r/w/o: 1259.12/1298.12/236.02) lat (ms,95%): 707.07 err/s 18.00 reconn/s: 0.00
[ 273s ] thds: 36 tps: 82.00 qps: 2753.88 (r/w/o: 1263.95/1289.94/199.99) lat (ms,95%): 926.33 err/s 18.00 reconn/s: 0.00
[ 274s ] thds: 36 tps: 101.99 qps: 3018.77 (r/w/o: 1357.89/1399.89/260.98) lat (ms,95%): 694.45 err/s 29.00 reconn/s: 0.00
[ 275s ] thds: 36 tps: 47.00 qps: 1672.17 (r/w/o: 762.08/795.08/115.01) lat (ms,95%): 612.21 err/s 10.00 reconn/s: 0.00
[ 276s ] thds: 36 tps: 31.00 qps: 701.95 (r/w/o: 308.98/314.98/77.99) lat (ms,95%): 1803.47 err/s 8.00 reconn/s: 0.00
[ 277s ] thds: 36 tps: 91.01 qps: 2897.26 (r/w/o: 1319.12/1360.12/218.02) lat (ms,95%): 1708.63 err/s 18.00 reconn/s: 0.00
[ 278s ] thds: 36 tps: 68.00 qps: 2407.03 (r/w/o: 1087.02/1130.02/190.00) lat (ms,95%): 1069.86 err/s 27.00 reconn/s: 0.00
[ 279s ] thds: 36 tps: 99.00 qps: 3215.98 (r/w/o: 1473.99/1503.99/238.00) lat (ms,95%): 816.63 err/s 20.00 reconn/s: 0.00
[ 280s ] thds: 36 tps: 80.99 qps: 2619.79 (r/w/o: 1180.90/1228.90/209.98) lat (ms,95%): 759.88 err/s 25.00 reconn/s: 0.00
[ 281s ] thds: 36 tps: 52.00 qps: 2104.99 (r/w/o: 973.99/1006.99/124.00) lat (ms,95%): 926.33 err/s 11.00 reconn/s: 0.00
[ 282s ] thds: 36 tps: 80.00 qps: 2253.99 (r/w/o: 1022.00/1030.00/202.00) lat (ms,95%): 1050.76 err/s 21.00 reconn/s: 0.00
[ 283s ] thds: 36 tps: 69.00 qps: 2336.13 (r/w/o: 1048.06/1116.06/172.01) lat (ms,95%): 893.56 err/s 17.00 reconn/s: 0.00
[ 284s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 285s ] thds: 36 tps: 7.00 qps: 89.00 (r/w/o: 36.00/35.00/18.00) lat (ms,95%): 3151.62 err/s 2.00 reconn/s: 0.00
[ 286s ] thds: 36 tps: 73.00 qps: 2166.07 (r/w/o: 983.03/985.03/198.01) lat (ms,95%): 3151.62 err/s 26.00 reconn/s: 0.00
[ 287s ] thds: 36 tps: 75.00 qps: 2402.02 (r/w/o: 1083.01/1129.01/190.00) lat (ms,95%): 977.74 err/s 20.00 reconn/s: 0.00
[ 288s ] thds: 36 tps: 70.99 qps: 2263.65 (r/w/o: 1017.84/1051.84/193.97) lat (ms,95%): 802.05 err/s 26.00 reconn/s: 0.00
[ 289s ] thds: 36 tps: 69.01 qps: 2045.31 (r/w/o: 914.14/963.15/168.03) lat (ms,95%): 995.51 err/s 16.00 reconn/s: 0.00
[ 290s ] thds: 36 tps: 108.99 qps: 3065.81 (r/w/o: 1376.92/1402.92/285.98) lat (ms,95%): 1089.30 err/s 35.00 reconn/s: 0.00
[ 291s ] thds: 36 tps: 79.01 qps: 2816.27 (r/w/o: 1274.12/1326.13/216.02) lat (ms,95%): 719.92 err/s 29.00 reconn/s: 0.00
[ 292s ] thds: 36 tps: 80.00 qps: 2475.91 (r/w/o: 1134.96/1152.96/187.99) lat (ms,95%): 1013.60 err/s 14.00 reconn/s: 0.00
[ 293s ] thds: 36 tps: 81.00 qps: 2687.91 (r/w/o: 1221.96/1263.96/201.99) lat (ms,95%): 707.07 err/s 20.00 reconn/s: 0.00
[ 294s ] thds: 36 tps: 0.00 qps: 0.00 (r/w/o: 0.00/0.00/0.00) lat (ms,95%): 0.00 err/s 0.00 reconn/s: 0.00
[ 295s ] thds: 36 tps: 35.00 qps: 389.99 (r/w/o: 155.00/155.00/80.00) lat (ms,95%): 2449.36 err/s 5.00 reconn/s: 0.00
[ 296s ] thds: 36 tps: 91.01 qps: 3323.49 (r/w/o: 1516.22/1589.23/218.03) lat (ms,95%): 682.06 err/s 19.00 reconn/s: 0.00
[ 297s ] thds: 36 tps: 108.99 qps: 3330.81 (r/w/o: 1508.91/1559.91/261.99) lat (ms,95%): 657.93 err/s 22.00 reconn/s: 0.00
[ 298s ] thds: 36 tps: 92.01 qps: 2881.17 (r/w/o: 1289.08/1372.08/220.01) lat (ms,95%): 669.89 err/s 18.00 reconn/s: 0.00
[ 299s ] thds: 36 tps: 78.00 qps: 2863.11 (r/w/o: 1288.05/1377.05/198.01) lat (ms,95%): 877.61 err/s 21.00 reconn/s: 0.00
[ 300s ] thds: 36 tps: 67.99 qps: 2828.43 (r/w/o: 1287.74/1362.72/177.96) lat (ms,95%): 733.00 err/s 21.00 reconn/s: 0.00
```
</details>

<details>
<summary>SQL statistics</summary>

```console
SQL statistics:
    queries performed:
        read:                            257586
        write:                           266905
        other:                           45560
        total:                           570051
    transactions:                        18124  (60.33 per sec.)
    queries:                             570051 (1897.54 per sec.)
    ignored errors:                      4703   (15.65 per sec.)
    reconnects:                          0      (0.00 per sec.)
General statistics:
    total time:                          300.4136s
    total number of events:              18124
Latency (ms):
         min:                                    0.76
         avg:                                  596.11
         max:                                 4777.94
         95th percentile:                     1352.03
         sum:                             10803847.82
Threads fairness:
    events (avg/stddev):           503.4444/10.11
    execution time (avg/stddev):   300.1069/0.12
```
</details>

    
    
### "Агрессивный" режим - total number of events: 46120 (среднее - 153 tps)

<details>
<summary>settings</summary>

```console
# Блок из "минимальных" настроек 

shared_buffers = 16GB                 
temp_buffers = 1GB
work_mem = 256MB
maintenance_work_mem = 2GB
max_connections = 36

# Уменьшаем стоимость 
random_page_cost = 1

# Оптимизацию данных параметров необходимо проводить на основе статистики, нагрузки и планов запросов (в тесте явно указал 36 тредов, исследовать запросы теста не стал)
 
effective_io_concurrency = 36           # выставляем равным кол-ву тредов
maintenance_io_concurrency = 36         # выставляем равным кол-ву тредов
max_worker_processes = 36               # выставляем равным кол-ву тредов
max_parallel_maintenance_workers = 36   # выставляем равным кол-ву тредов
max_parallel_workers_per_gather = 36    # выставляем равным кол-ву тредов
max_parallel_workers = 36               # выставляем равным кол-ву тредов

# Блок небезопасных настроек

full_page_writes = off                  # отключаем запись целой страницы при первом изменении после контрольной точки
fsync = off                             # не следим за записью на диск
synchronous_commit = off                # асинхронный коммит, не ждем подтверждения
checkpoint_timeout = 1d                 # контрольная точка раз в сутки
checkpoint_completion_target = 1        # размазываем запись на весь период до следующей контрольной точки
checkpoint_flush_after = 0              # Отключаем управление отложенной записью
checkpoint_warning = 0                  # Отключаем логирование 
track_activities = off                  # Отключаем сбор статистики
autovacuum = off                        # Отключаем автовакуум
```
</details>

<details>
<summary>log</summary>

```console
[ 1s ] thds: 36 tps: 121.65 qps: 4136.01 (r/w/o: 1831.69/1882.54/421.78) lat (ms,95%): 511.33 err/s 35.90 reconn/s: 0.00
[ 2s ] thds: 36 tps: 171.11 qps: 5070.16 (r/w/o: 2306.44/2366.48/397.25) lat (ms,95%): 467.30 err/s 29.02 reconn/s: 0.00
[ 3s ] thds: 36 tps: 190.00 qps: 5563.96 (r/w/o: 2548.98/2575.98/439.00) lat (ms,95%): 419.45 err/s 30.00 reconn/s: 0.00
[ 4s ] thds: 36 tps: 197.00 qps: 5578.00 (r/w/o: 2518.00/2597.00/463.00) lat (ms,95%): 427.07 err/s 34.00 reconn/s: 0.00
[ 5s ] thds: 36 tps: 202.00 qps: 5585.94 (r/w/o: 2546.97/2571.97/466.99) lat (ms,95%): 390.30 err/s 33.00 reconn/s: 0.00
[ 6s ] thds: 36 tps: 116.00 qps: 3575.04 (r/w/o: 1623.02/1682.02/270.00) lat (ms,95%): 646.19 err/s 19.00 reconn/s: 0.00
[ 7s ] thds: 36 tps: 168.99 qps: 4926.70 (r/w/o: 2232.87/2282.86/410.98) lat (ms,95%): 646.19 err/s 39.00 reconn/s: 0.00
[ 8s ] thds: 36 tps: 204.01 qps: 5694.34 (r/w/o: 2546.15/2656.16/492.03) lat (ms,95%): 442.73 err/s 42.00 reconn/s: 0.00
[ 9s ] thds: 36 tps: 186.99 qps: 5782.61 (r/w/o: 2622.82/2707.82/451.97) lat (ms,95%): 427.07 err/s 39.00 reconn/s: 0.00
[ 10s ] thds: 36 tps: 198.01 qps: 5824.24 (r/w/o: 2643.11/2717.11/464.02) lat (ms,95%): 442.73 err/s 37.00 reconn/s: 0.00
[ 11s ] thds: 36 tps: 200.01 qps: 5817.27 (r/w/o: 2622.12/2711.12/484.02) lat (ms,95%): 427.07 err/s 40.00 reconn/s: 0.00
[ 12s ] thds: 36 tps: 198.00 qps: 5977.96 (r/w/o: 2704.98/2786.98/486.00) lat (ms,95%): 404.61 err/s 49.00 reconn/s: 0.00
[ 13s ] thds: 36 tps: 227.97 qps: 6117.14 (r/w/o: 2753.61/2831.60/531.93) lat (ms,95%): 390.30 err/s 38.99 reconn/s: 0.00
[ 14s ] thds: 36 tps: 187.01 qps: 6095.38 (r/w/o: 2786.17/2874.18/435.03) lat (ms,95%): 427.07 err/s 31.00 reconn/s: 0.00
[ 15s ] thds: 36 tps: 189.00 qps: 6017.07 (r/w/o: 2748.03/2828.03/441.00) lat (ms,95%): 404.61 err/s 31.00 reconn/s: 0.00
[ 16s ] thds: 36 tps: 214.01 qps: 5997.35 (r/w/o: 2705.16/2776.16/516.03) lat (ms,95%): 411.96 err/s 45.00 reconn/s: 0.00
[ 17s ] thds: 36 tps: 199.99 qps: 6076.76 (r/w/o: 2753.89/2844.89/477.98) lat (ms,95%): 404.61 err/s 40.00 reconn/s: 0.00
[ 18s ] thds: 36 tps: 202.00 qps: 5752.14 (r/w/o: 2577.06/2706.07/469.01) lat (ms,95%): 450.77 err/s 34.00 reconn/s: 0.00
[ 19s ] thds: 36 tps: 222.00 qps: 5963.95 (r/w/o: 2686.98/2749.98/527.00) lat (ms,95%): 419.45 err/s 41.00 reconn/s: 0.00
[ 20s ] thds: 36 tps: 203.00 qps: 6066.97 (r/w/o: 2746.99/2841.99/478.00) lat (ms,95%): 427.07 err/s 36.00 reconn/s: 0.00
[ 21s ] thds: 36 tps: 223.00 qps: 6028.99 (r/w/o: 2725.99/2768.99/534.00) lat (ms,95%): 411.96 err/s 47.00 reconn/s: 0.00
[ 22s ] thds: 36 tps: 188.01 qps: 6029.26 (r/w/o: 2749.12/2811.12/469.02) lat (ms,95%): 404.61 err/s 48.00 reconn/s: 0.00
[ 23s ] thds: 36 tps: 212.00 qps: 6298.95 (r/w/o: 2852.98/2954.98/491.00) lat (ms,95%): 383.33 err/s 34.00 reconn/s: 0.00
[ 24s ] thds: 36 tps: 196.00 qps: 6069.98 (r/w/o: 2743.99/2854.99/471.00) lat (ms,95%): 404.61 err/s 40.00 reconn/s: 0.00
[ 25s ] thds: 36 tps: 188.98 qps: 6056.47 (r/w/o: 2747.76/2864.75/443.96) lat (ms,95%): 411.96 err/s 34.00 reconn/s: 0.00
[ 26s ] thds: 36 tps: 195.01 qps: 6216.37 (r/w/o: 2810.17/2977.18/429.03) lat (ms,95%): 427.07 err/s 20.00 reconn/s: 0.00
[ 27s ] thds: 36 tps: 212.00 qps: 6179.94 (r/w/o: 2806.97/2884.97/488.00) lat (ms,95%): 383.33 err/s 34.00 reconn/s: 0.00
[ 28s ] thds: 36 tps: 203.01 qps: 6106.19 (r/w/o: 2757.09/2867.09/482.02) lat (ms,95%): 427.07 err/s 39.00 reconn/s: 0.00
[ 29s ] thds: 36 tps: 219.00 qps: 6183.10 (r/w/o: 2795.05/2883.05/505.01) lat (ms,95%): 376.49 err/s 36.00 reconn/s: 0.00
[ 30s ] thds: 36 tps: 210.00 qps: 6106.98 (r/w/o: 2756.99/2854.99/495.00) lat (ms,95%): 397.39 err/s 38.00 reconn/s: 0.00
[ 31s ] thds: 36 tps: 220.00 qps: 6148.02 (r/w/o: 2779.01/2845.01/524.00) lat (ms,95%): 397.39 err/s 44.00 reconn/s: 0.00
[ 32s ] thds: 36 tps: 225.99 qps: 6096.85 (r/w/o: 2759.93/2804.93/531.99) lat (ms,95%): 356.70 err/s 42.00 reconn/s: 0.00
[ 33s ] thds: 36 tps: 195.00 qps: 6227.98 (r/w/o: 2815.99/2953.99/458.00) lat (ms,95%): 450.77 err/s 35.00 reconn/s: 0.00
[ 34s ] thds: 36 tps: 129.00 qps: 3902.09 (r/w/o: 1766.04/1830.04/306.01) lat (ms,95%): 694.45 err/s 24.00 reconn/s: 0.00
[ 35s ] thds: 36 tps: 109.00 qps: 3287.02 (r/w/o: 1476.01/1543.01/268.00) lat (ms,95%): 977.74 err/s 26.00 reconn/s: 0.00
[ 36s ] thds: 36 tps: 133.00 qps: 4347.91 (r/w/o: 1974.96/2028.96/343.99) lat (ms,95%): 943.16 err/s 40.00 reconn/s: 0.00
[ 37s ] thds: 36 tps: 107.00 qps: 3155.86 (r/w/o: 1412.94/1474.93/267.99) lat (ms,95%): 1013.60 err/s 27.00 reconn/s: 0.00
[ 38s ] thds: 36 tps: 122.02 qps: 3769.51 (r/w/o: 1704.23/1751.24/314.04) lat (ms,95%): 733.00 err/s 35.00 reconn/s: 0.00
[ 39s ] thds: 36 tps: 114.99 qps: 3762.61 (r/w/o: 1701.82/1766.82/293.97) lat (ms,95%): 995.51 err/s 34.00 reconn/s: 0.00
[ 40s ] thds: 36 tps: 126.00 qps: 4329.15 (r/w/o: 1942.07/2061.07/326.01) lat (ms,95%): 943.16 err/s 39.00 reconn/s: 0.00
[ 41s ] thds: 36 tps: 110.00 qps: 3990.17 (r/w/o: 1821.08/1917.08/252.01) lat (ms,95%): 926.33 err/s 17.00 reconn/s: 0.00
[ 42s ] thds: 36 tps: 135.00 qps: 3698.98 (r/w/o: 1657.99/1688.99/352.00) lat (ms,95%): 995.51 err/s 42.00 reconn/s: 0.00
[ 43s ] thds: 36 tps: 112.99 qps: 3875.57 (r/w/o: 1764.80/1814.80/295.97) lat (ms,95%): 960.30 err/s 37.00 reconn/s: 0.00
[ 44s ] thds: 36 tps: 110.00 qps: 3438.14 (r/w/o: 1542.06/1614.07/282.01) lat (ms,95%): 1032.01 err/s 33.00 reconn/s: 0.00
[ 45s ] thds: 36 tps: 153.02 qps: 4554.51 (r/w/o: 2064.23/2112.24/378.04) lat (ms,95%): 694.45 err/s 37.00 reconn/s: 0.00
[ 46s ] thds: 36 tps: 135.98 qps: 4586.38 (r/w/o: 2078.72/2129.71/377.95) lat (ms,95%): 733.00 err/s 52.99 reconn/s: 0.00
[ 47s ] thds: 36 tps: 157.01 qps: 5159.20 (r/w/o: 2344.09/2427.09/388.02) lat (ms,95%): 846.57 err/s 37.00 reconn/s: 0.00
[ 48s ] thds: 36 tps: 141.01 qps: 4484.25 (r/w/o: 2025.11/2111.12/348.02) lat (ms,95%): 846.57 err/s 33.00 reconn/s: 0.00
[ 49s ] thds: 36 tps: 158.99 qps: 5157.65 (r/w/o: 2316.84/2412.84/427.97) lat (ms,95%): 634.66 err/s 56.00 reconn/s: 0.00
[ 50s ] thds: 36 tps: 145.00 qps: 4576.13 (r/w/o: 2077.06/2147.06/352.01) lat (ms,95%): 694.45 err/s 30.00 reconn/s: 0.00
[ 51s ] thds: 36 tps: 138.00 qps: 3957.01 (r/w/o: 1777.00/1816.00/364.00) lat (ms,95%): 802.05 err/s 45.00 reconn/s: 0.00
[ 52s ] thds: 36 tps: 120.99 qps: 3934.65 (r/w/o: 1764.84/1851.84/317.97) lat (ms,95%): 943.16 err/s 38.00 reconn/s: 0.00
[ 53s ] thds: 36 tps: 132.99 qps: 4163.79 (r/w/o: 1898.90/1935.90/328.98) lat (ms,95%): 861.95 err/s 33.00 reconn/s: 0.00
[ 54s ] thds: 36 tps: 162.02 qps: 5370.61 (r/w/o: 2439.28/2524.29/407.05) lat (ms,95%): 719.92 err/s 41.00 reconn/s: 0.00
[ 55s ] thds: 36 tps: 136.00 qps: 4595.85 (r/w/o: 2085.93/2167.93/341.99) lat (ms,95%): 682.06 err/s 36.00 reconn/s: 0.00
[ 56s ] thds: 36 tps: 158.02 qps: 4432.55 (r/w/o: 2002.25/2018.25/412.05) lat (ms,95%): 682.06 err/s 50.01 reconn/s: 0.00
[ 57s ] thds: 36 tps: 156.98 qps: 5053.29 (r/w/o: 2276.68/2370.67/405.94) lat (ms,95%): 733.00 err/s 46.99 reconn/s: 0.00
[ 58s ] thds: 36 tps: 142.74 qps: 4306.03 (r/w/o: 1929.43/2013.28/363.33) lat (ms,95%): 694.45 err/s 38.93 reconn/s: 0.00
[ 59s ] thds: 36 tps: 79.02 qps: 2058.45 (r/w/o: 919.20/934.20/205.04) lat (ms,95%): 893.56 err/s 24.01 reconn/s: 0.00
[ 60s ] thds: 36 tps: 84.14 qps: 2221.72 (r/w/o: 997.67/1020.71/203.34) lat (ms,95%): 1032.01 err/s 17.03 reconn/s: 0.00
[ 61s ] thds: 36 tps: 99.00 qps: 2961.09 (r/w/o: 1338.04/1389.04/234.01) lat (ms,95%): 1129.24 err/s 18.00 reconn/s: 0.00
[ 62s ] thds: 36 tps: 130.00 qps: 3872.92 (r/w/o: 1733.96/1824.96/313.99) lat (ms,95%): 861.95 err/s 28.00 reconn/s: 0.00
[ 63s ] thds: 36 tps: 125.00 qps: 3849.85 (r/w/o: 1753.93/1807.93/287.99) lat (ms,95%): 926.33 err/s 19.00 reconn/s: 0.00
[ 64s ] thds: 36 tps: 135.00 qps: 3999.01 (r/w/o: 1813.01/1844.01/342.00) lat (ms,95%): 816.63 err/s 36.00 reconn/s: 0.00
[ 65s ] thds: 36 tps: 121.01 qps: 3084.27 (r/w/o: 1374.12/1398.12/312.03) lat (ms,95%): 773.68 err/s 35.00 reconn/s: 0.00
[ 66s ] thds: 36 tps: 124.00 qps: 4007.92 (r/w/o: 1821.96/1891.96/293.99) lat (ms,95%): 759.88 err/s 24.00 reconn/s: 0.00
[ 67s ] thds: 36 tps: 101.00 qps: 3089.10 (r/w/o: 1396.04/1423.04/270.01) lat (ms,95%): 877.61 err/s 36.00 reconn/s: 0.00
[ 68s ] thds: 36 tps: 122.00 qps: 3479.99 (r/w/o: 1585.99/1605.99/288.00) lat (ms,95%): 846.57 err/s 23.00 reconn/s: 0.00
[ 69s ] thds: 36 tps: 142.99 qps: 4103.75 (r/w/o: 1847.89/1895.88/359.98) lat (ms,95%): 682.06 err/s 37.00 reconn/s: 0.00
[ 70s ] thds: 36 tps: 129.00 qps: 3886.98 (r/w/o: 1743.99/1819.99/323.00) lat (ms,95%): 926.33 err/s 35.00 reconn/s: 0.00
[ 71s ] thds: 36 tps: 110.00 qps: 3513.11 (r/w/o: 1602.05/1650.05/261.01) lat (ms,95%): 909.80 err/s 21.00 reconn/s: 0.00
[ 72s ] thds: 36 tps: 109.99 qps: 3611.73 (r/w/o: 1628.88/1714.87/267.98) lat (ms,95%): 926.33 err/s 24.00 reconn/s: 0.00
[ 73s ] thds: 36 tps: 125.01 qps: 3926.27 (r/w/o: 1776.12/1860.13/290.02) lat (ms,95%): 877.61 err/s 20.00 reconn/s: 0.00
[ 74s ] thds: 36 tps: 125.00 qps: 4239.89 (r/w/o: 1931.95/2011.95/295.99) lat (ms,95%): 773.68 err/s 25.00 reconn/s: 0.00
[ 75s ] thds: 36 tps: 104.01 qps: 3629.34 (r/w/o: 1660.16/1731.16/238.02) lat (ms,95%): 861.95 err/s 15.00 reconn/s: 0.00
[ 76s ] thds: 36 tps: 133.99 qps: 4069.63 (r/w/o: 1827.83/1913.83/327.97) lat (ms,95%): 861.95 err/s 30.00 reconn/s: 0.00
[ 77s ] thds: 36 tps: 119.00 qps: 3533.09 (r/w/o: 1584.04/1645.04/304.01) lat (ms,95%): 831.46 err/s 33.00 reconn/s: 0.00
[ 78s ] thds: 36 tps: 135.99 qps: 4284.73 (r/w/o: 1945.88/1998.88/339.98) lat (ms,95%): 816.63 err/s 35.00 reconn/s: 0.00
[ 79s ] thds: 36 tps: 118.00 qps: 3701.14 (r/w/o: 1677.06/1726.06/298.01) lat (ms,95%): 634.66 err/s 31.00 reconn/s: 0.00
[ 80s ] thds: 36 tps: 125.00 qps: 3826.99 (r/w/o: 1734.00/1795.00/298.00) lat (ms,95%): 877.61 err/s 24.00 reconn/s: 0.00
[ 81s ] thds: 36 tps: 122.00 qps: 3594.03 (r/w/o: 1624.01/1660.01/310.00) lat (ms,95%): 861.95 err/s 34.00 reconn/s: 0.00
[ 82s ] thds: 36 tps: 115.99 qps: 3194.71 (r/w/o: 1427.87/1484.87/281.97) lat (ms,95%): 861.95 err/s 25.00 reconn/s: 0.00
[ 83s ] thds: 36 tps: 146.01 qps: 4123.23 (r/w/o: 1840.10/1919.11/364.02) lat (ms,95%): 816.63 err/s 36.00 reconn/s: 0.00
[ 84s ] thds: 36 tps: 137.01 qps: 4455.30 (r/w/o: 2027.13/2098.14/330.02) lat (ms,95%): 682.06 err/s 29.00 reconn/s: 0.00
[ 85s ] thds: 36 tps: 135.99 qps: 4273.66 (r/w/o: 1931.85/2013.84/327.97) lat (ms,95%): 893.56 err/s 29.00 reconn/s: 0.00
[ 86s ] thds: 36 tps: 128.01 qps: 4041.17 (r/w/o: 1815.08/1902.08/324.01) lat (ms,95%): 909.80 err/s 34.00 reconn/s: 0.00
[ 87s ] thds: 36 tps: 104.00 qps: 3369.98 (r/w/o: 1538.99/1562.99/268.00) lat (ms,95%): 861.95 err/s 30.00 reconn/s: 0.00
[ 88s ] thds: 36 tps: 119.00 qps: 3779.11 (r/w/o: 1716.05/1755.05/308.01) lat (ms,95%): 977.74 err/s 36.00 reconn/s: 0.00
[ 89s ] thds: 36 tps: 127.98 qps: 4062.49 (r/w/o: 1835.77/1924.76/301.96) lat (ms,95%): 831.46 err/s 23.00 reconn/s: 0.00
[ 90s ] thds: 36 tps: 130.01 qps: 3821.42 (r/w/o: 1735.19/1766.20/320.04) lat (ms,95%): 960.30 err/s 30.00 reconn/s: 0.00
[ 91s ] thds: 36 tps: 125.00 qps: 3840.94 (r/w/o: 1746.97/1807.97/286.00) lat (ms,95%): 960.30 err/s 20.00 reconn/s: 0.00
[ 92s ] thds: 36 tps: 113.99 qps: 3491.73 (r/w/o: 1569.88/1639.88/281.98) lat (ms,95%): 861.95 err/s 27.00 reconn/s: 0.00
[ 93s ] thds: 36 tps: 108.00 qps: 3383.10 (r/w/o: 1546.05/1561.05/276.01) lat (ms,95%): 960.30 err/s 30.00 reconn/s: 0.00
[ 94s ] thds: 36 tps: 135.01 qps: 3945.42 (r/w/o: 1795.19/1828.19/322.03) lat (ms,95%): 773.68 err/s 29.00 reconn/s: 0.00
[ 95s ] thds: 36 tps: 96.99 qps: 3008.69 (r/w/o: 1368.86/1403.86/235.98) lat (ms,95%): 787.74 err/s 21.00 reconn/s: 0.00
[ 96s ] thds: 36 tps: 134.01 qps: 4191.16 (r/w/o: 1907.07/1951.07/333.01) lat (ms,95%): 909.80 err/s 34.00 reconn/s: 0.00
[ 97s ] thds: 36 tps: 125.00 qps: 4207.99 (r/w/o: 1904.00/1989.00/315.00) lat (ms,95%): 926.33 err/s 33.00 reconn/s: 0.00
[ 98s ] thds: 36 tps: 131.00 qps: 3964.07 (r/w/o: 1745.03/1879.04/340.01) lat (ms,95%): 960.30 err/s 41.00 reconn/s: 0.00
[ 99s ] thds: 36 tps: 119.00 qps: 3804.09 (r/w/o: 1734.04/1774.04/296.01) lat (ms,95%): 746.32 err/s 29.00 reconn/s: 0.00
[ 100s ] thds: 36 tps: 122.99 qps: 3497.66 (r/w/o: 1588.85/1622.84/285.97) lat (ms,95%): 926.33 err/s 20.00 reconn/s: 0.00
[ 101s ] thds: 36 tps: 103.01 qps: 3236.19 (r/w/o: 1452.08/1532.09/252.01) lat (ms,95%): 1191.92 err/s 23.00 reconn/s: 0.00
[ 102s ] thds: 36 tps: 136.00 qps: 4101.90 (r/w/o: 1844.95/1930.95/325.99) lat (ms,95%): 977.74 err/s 29.00 reconn/s: 0.00
[ 103s ] thds: 36 tps: 138.00 qps: 4655.86 (r/w/o: 2107.94/2224.93/322.99) lat (ms,95%): 787.74 err/s 24.00 reconn/s: 0.00
[ 104s ] thds: 36 tps: 149.01 qps: 4602.21 (r/w/o: 2107.10/2126.10/369.02) lat (ms,95%): 612.21 err/s 35.00 reconn/s: 0.00
[ 105s ] thds: 36 tps: 135.00 qps: 4409.99 (r/w/o: 2007.00/2087.00/316.00) lat (ms,95%): 682.06 err/s 23.00 reconn/s: 0.00
[ 106s ] thds: 36 tps: 139.00 qps: 4129.07 (r/w/o: 1860.03/1925.03/344.01) lat (ms,95%): 802.05 err/s 33.00 reconn/s: 0.00
[ 107s ] thds: 36 tps: 139.00 qps: 4267.00 (r/w/o: 1934.00/1997.00/336.00) lat (ms,95%): 759.88 err/s 30.00 reconn/s: 0.00
[ 108s ] thds: 36 tps: 125.00 qps: 3841.92 (r/w/o: 1735.96/1791.96/313.99) lat (ms,95%): 719.92 err/s 32.00 reconn/s: 0.00
[ 109s ] thds: 36 tps: 135.00 qps: 4382.00 (r/w/o: 1986.00/2075.00/321.00) lat (ms,95%): 773.68 err/s 27.00 reconn/s: 0.00
[ 110s ] thds: 36 tps: 127.01 qps: 3984.27 (r/w/o: 1814.12/1885.13/285.02) lat (ms,95%): 802.05 err/s 17.00 reconn/s: 0.00
[ 111s ] thds: 36 tps: 143.01 qps: 4501.20 (r/w/o: 2012.09/2105.09/384.02) lat (ms,95%): 773.68 err/s 50.00 reconn/s: 0.00
[ 112s ] thds: 36 tps: 133.99 qps: 4558.61 (r/w/o: 2076.82/2165.81/315.97) lat (ms,95%): 746.32 err/s 24.00 reconn/s: 0.00
[ 113s ] thds: 36 tps: 160.02 qps: 4319.41 (r/w/o: 1947.19/1972.19/400.04) lat (ms,95%): 623.33 err/s 41.00 reconn/s: 0.00
[ 114s ] thds: 36 tps: 131.99 qps: 3949.77 (r/w/o: 1775.90/1831.89/341.98) lat (ms,95%): 773.68 err/s 40.00 reconn/s: 0.00
[ 115s ] thds: 36 tps: 140.00 qps: 4396.92 (r/w/o: 1985.96/2084.96/325.99) lat (ms,95%): 802.05 err/s 24.00 reconn/s: 0.00
[ 116s ] thds: 36 tps: 128.01 qps: 3560.16 (r/w/o: 1607.07/1639.08/314.01) lat (ms,95%): 787.74 err/s 30.00 reconn/s: 0.00
[ 117s ] thds: 36 tps: 152.00 qps: 4427.92 (r/w/o: 2001.96/2079.96/345.99) lat (ms,95%): 877.61 err/s 21.00 reconn/s: 0.00
[ 118s ] thds: 36 tps: 130.00 qps: 4153.90 (r/w/o: 1897.95/1941.95/313.99) lat (ms,95%): 773.68 err/s 27.00 reconn/s: 0.00
[ 119s ] thds: 36 tps: 137.01 qps: 4223.16 (r/w/o: 1913.07/1970.07/340.01) lat (ms,95%): 816.63 err/s 35.00 reconn/s: 0.00
[ 120s ] thds: 36 tps: 138.01 qps: 4023.15 (r/w/o: 1846.07/1851.07/326.01) lat (ms,95%): 746.32 err/s 27.00 reconn/s: 0.00
[ 121s ] thds: 36 tps: 157.99 qps: 4471.72 (r/w/o: 1994.88/2070.87/405.97) lat (ms,95%): 707.07 err/s 45.00 reconn/s: 0.00
[ 122s ] thds: 36 tps: 140.00 qps: 4234.06 (r/w/o: 1932.03/1980.03/322.00) lat (ms,95%): 759.88 err/s 22.00 reconn/s: 0.00
[ 123s ] thds: 36 tps: 117.00 qps: 3697.00 (r/w/o: 1674.00/1733.00/290.00) lat (ms,95%): 909.80 err/s 28.00 reconn/s: 0.00
[ 124s ] thds: 36 tps: 143.98 qps: 4261.55 (r/w/o: 1941.79/1979.79/339.96) lat (ms,95%): 759.88 err/s 27.00 reconn/s: 0.00
[ 125s ] thds: 36 tps: 129.01 qps: 4165.42 (r/w/o: 1878.19/1985.20/302.03) lat (ms,95%): 816.63 err/s 22.00 reconn/s: 0.00
[ 126s ] thds: 36 tps: 152.01 qps: 4384.21 (r/w/o: 1957.10/2039.10/388.02) lat (ms,95%): 773.68 err/s 42.00 reconn/s: 0.00
[ 127s ] thds: 36 tps: 138.00 qps: 4142.91 (r/w/o: 1864.96/1943.96/333.99) lat (ms,95%): 846.57 err/s 29.00 reconn/s: 0.00
[ 128s ] thds: 36 tps: 130.99 qps: 4102.73 (r/w/o: 1874.88/1927.87/299.98) lat (ms,95%): 816.63 err/s 21.00 reconn/s: 0.00
[ 129s ] thds: 36 tps: 135.00 qps: 4168.98 (r/w/o: 1891.99/1962.99/314.00) lat (ms,95%): 759.88 err/s 22.00 reconn/s: 0.00
[ 130s ] thds: 36 tps: 149.00 qps: 4409.05 (r/w/o: 1997.02/2056.02/356.00) lat (ms,95%): 787.74 err/s 31.00 reconn/s: 0.00
[ 131s ] thds: 36 tps: 146.99 qps: 4086.76 (r/w/o: 1838.89/1869.89/377.98) lat (ms,95%): 590.56 err/s 42.00 reconn/s: 0.00
[ 132s ] thds: 36 tps: 164.00 qps: 5097.07 (r/w/o: 2313.03/2386.03/398.01) lat (ms,95%): 773.68 err/s 35.00 reconn/s: 0.00
[ 133s ] thds: 36 tps: 147.01 qps: 3907.33 (r/w/o: 1766.15/1787.15/354.03) lat (ms,95%): 746.32 err/s 30.00 reconn/s: 0.00
[ 134s ] thds: 36 tps: 147.99 qps: 4839.79 (r/w/o: 2190.90/2294.90/353.98) lat (ms,95%): 802.05 err/s 29.00 reconn/s: 0.00
[ 135s ] thds: 36 tps: 183.01 qps: 5613.34 (r/w/o: 2537.15/2616.16/460.03) lat (ms,95%): 634.66 err/s 47.00 reconn/s: 0.00
[ 136s ] thds: 36 tps: 139.98 qps: 4657.23 (r/w/o: 2114.65/2206.64/335.94) lat (ms,95%): 669.89 err/s 28.00 reconn/s: 0.00
[ 137s ] thds: 36 tps: 181.02 qps: 5314.59 (r/w/o: 2384.27/2488.28/442.05) lat (ms,95%): 657.93 err/s 42.00 reconn/s: 0.00
[ 138s ] thds: 36 tps: 151.00 qps: 4350.97 (r/w/o: 1944.99/2025.99/380.00) lat (ms,95%): 787.74 err/s 39.00 reconn/s: 0.00
[ 139s ] thds: 36 tps: 155.99 qps: 4662.79 (r/w/o: 2102.90/2185.90/373.98) lat (ms,95%): 669.89 err/s 32.00 reconn/s: 0.00
[ 140s ] thds: 36 tps: 145.01 qps: 4197.38 (r/w/o: 1884.17/1953.18/360.03) lat (ms,95%): 831.46 err/s 35.00 reconn/s: 0.00
[ 141s ] thds: 36 tps: 131.99 qps: 4220.77 (r/w/o: 1919.90/1980.89/319.98) lat (ms,95%): 657.93 err/s 28.00 reconn/s: 0.00
[ 142s ] thds: 36 tps: 135.00 qps: 3873.96 (r/w/o: 1728.98/1815.98/329.00) lat (ms,95%): 759.88 err/s 30.00 reconn/s: 0.00
[ 143s ] thds: 36 tps: 195.99 qps: 5888.80 (r/w/o: 2675.91/2741.91/470.98) lat (ms,95%): 634.66 err/s 40.00 reconn/s: 0.00
[ 144s ] thds: 36 tps: 185.01 qps: 5442.30 (r/w/o: 2435.13/2559.14/448.02) lat (ms,95%): 569.67 err/s 40.00 reconn/s: 0.00
[ 145s ] thds: 36 tps: 150.99 qps: 4631.59 (r/w/o: 2089.82/2187.81/353.97) lat (ms,95%): 707.07 err/s 26.00 reconn/s: 0.00
[ 146s ] thds: 36 tps: 138.00 qps: 4546.09 (r/w/o: 2067.04/2141.04/338.01) lat (ms,95%): 694.45 err/s 32.00 reconn/s: 0.00
[ 147s ] thds: 36 tps: 161.02 qps: 4871.55 (r/w/o: 2210.25/2269.25/392.04) lat (ms,95%): 707.07 err/s 37.00 reconn/s: 0.00
[ 148s ] thds: 36 tps: 162.98 qps: 5131.36 (r/w/o: 2334.71/2422.70/373.95) lat (ms,95%): 733.00 err/s 24.00 reconn/s: 0.00
[ 149s ] thds: 36 tps: 166.02 qps: 5511.60 (r/w/o: 2511.27/2590.28/410.04) lat (ms,95%): 657.93 err/s 39.00 reconn/s: 0.00
[ 150s ] thds: 36 tps: 178.01 qps: 5489.23 (r/w/o: 2478.10/2582.11/429.02) lat (ms,95%): 682.06 err/s 39.00 reconn/s: 0.00
[ 151s ] thds: 36 tps: 172.99 qps: 5393.65 (r/w/o: 2409.85/2534.84/448.97) lat (ms,95%): 601.29 err/s 52.00 reconn/s: 0.00
[ 152s ] thds: 36 tps: 200.00 qps: 5611.94 (r/w/o: 2534.97/2576.97/499.99) lat (ms,95%): 493.24 err/s 51.00 reconn/s: 0.00
[ 153s ] thds: 36 tps: 160.01 qps: 4722.34 (r/w/o: 2125.15/2207.16/390.03) lat (ms,95%): 657.93 err/s 37.00 reconn/s: 0.00
[ 154s ] thds: 36 tps: 157.00 qps: 5289.05 (r/w/o: 2417.02/2506.02/366.00) lat (ms,95%): 707.07 err/s 29.00 reconn/s: 0.00
[ 155s ] thds: 36 tps: 143.98 qps: 4589.39 (r/w/o: 2087.72/2165.71/335.96) lat (ms,95%): 759.88 err/s 25.00 reconn/s: 0.00
[ 156s ] thds: 36 tps: 166.01 qps: 4794.23 (r/w/o: 2167.10/2208.11/419.02) lat (ms,95%): 816.63 err/s 46.00 reconn/s: 0.00
[ 157s ] thds: 36 tps: 178.99 qps: 5375.85 (r/w/o: 2430.93/2489.93/454.99) lat (ms,95%): 539.71 err/s 49.00 reconn/s: 0.00
[ 158s ] thds: 36 tps: 174.01 qps: 5234.22 (r/w/o: 2373.10/2405.10/456.02) lat (ms,95%): 646.19 err/s 55.00 reconn/s: 0.00
[ 159s ] thds: 36 tps: 147.01 qps: 4827.24 (r/w/o: 2193.11/2290.11/344.02) lat (ms,95%): 634.66 err/s 28.00 reconn/s: 0.00
[ 160s ] thds: 36 tps: 139.98 qps: 4607.42 (r/w/o: 2091.73/2168.72/346.96) lat (ms,95%): 707.07 err/s 35.00 reconn/s: 0.00
[ 161s ] thds: 36 tps: 146.02 qps: 4457.46 (r/w/o: 2021.21/2085.22/351.04) lat (ms,95%): 831.46 err/s 32.00 reconn/s: 0.00
[ 162s ] thds: 36 tps: 171.00 qps: 4882.95 (r/w/o: 2209.98/2262.98/410.00) lat (ms,95%): 733.00 err/s 35.00 reconn/s: 0.00
[ 163s ] thds: 36 tps: 172.99 qps: 5375.71 (r/w/o: 2427.87/2525.87/421.98) lat (ms,95%): 646.19 err/s 38.00 reconn/s: 0.00
[ 164s ] thds: 36 tps: 155.99 qps: 4905.76 (r/w/o: 2208.89/2304.89/391.98) lat (ms,95%): 612.21 err/s 40.00 reconn/s: 0.00
[ 165s ] thds: 36 tps: 158.02 qps: 4456.65 (r/w/o: 2010.29/2084.30/362.05) lat (ms,95%): 646.19 err/s 23.00 reconn/s: 0.00
[ 166s ] thds: 36 tps: 155.00 qps: 4614.00 (r/w/o: 2096.00/2148.00/370.00) lat (ms,95%): 719.92 err/s 30.00 reconn/s: 0.00
[ 167s ] thds: 36 tps: 160.98 qps: 5122.39 (r/w/o: 2344.72/2393.71/383.95) lat (ms,95%): 746.32 err/s 31.00 reconn/s: 0.00
[ 168s ] thds: 36 tps: 183.02 qps: 6046.63 (r/w/o: 2742.29/2850.30/454.05) lat (ms,95%): 733.00 err/s 45.00 reconn/s: 0.00
[ 169s ] thds: 36 tps: 192.98 qps: 5977.43 (r/w/o: 2710.74/2826.73/439.96) lat (ms,95%): 569.67 err/s 28.00 reconn/s: 0.00
[ 170s ] thds: 36 tps: 209.01 qps: 6027.27 (r/w/o: 2730.12/2799.12/498.02) lat (ms,95%): 569.67 err/s 41.00 reconn/s: 0.00
[ 171s ] thds: 36 tps: 187.00 qps: 5559.92 (r/w/o: 2522.96/2576.96/459.99) lat (ms,95%): 590.56 err/s 44.00 reconn/s: 0.00
[ 172s ] thds: 36 tps: 202.02 qps: 6158.46 (r/w/o: 2769.21/2891.22/498.04) lat (ms,95%): 530.08 err/s 48.00 reconn/s: 0.00
[ 173s ] thds: 36 tps: 191.00 qps: 5890.01 (r/w/o: 2661.00/2765.00/464.00) lat (ms,95%): 569.67 err/s 42.00 reconn/s: 0.00
[ 174s ] thds: 36 tps: 169.98 qps: 5335.25 (r/w/o: 2424.66/2534.64/375.95) lat (ms,95%): 623.33 err/s 18.00 reconn/s: 0.00
[ 175s ] thds: 36 tps: 198.02 qps: 6000.65 (r/w/o: 2700.29/2814.31/486.05) lat (ms,95%): 669.89 err/s 46.01 reconn/s: 0.00
[ 176s ] thds: 36 tps: 212.00 qps: 6373.06 (r/w/o: 2893.02/2992.03/488.00) lat (ms,95%): 434.83 err/s 32.00 reconn/s: 0.00
[ 177s ] thds: 36 tps: 197.00 qps: 6033.93 (r/w/o: 2745.97/2829.97/457.99) lat (ms,95%): 549.52 err/s 32.00 reconn/s: 0.00
[ 178s ] thds: 36 tps: 206.00 qps: 6413.93 (r/w/o: 2912.97/2990.97/509.99) lat (ms,95%): 520.62 err/s 49.00 reconn/s: 0.00
[ 179s ] thds: 36 tps: 168.00 qps: 5367.87 (r/w/o: 2430.94/2508.94/427.99) lat (ms,95%): 590.56 err/s 46.00 reconn/s: 0.00
[ 180s ] thds: 36 tps: 195.01 qps: 5678.34 (r/w/o: 2567.16/2629.16/482.03) lat (ms,95%): 467.30 err/s 46.00 reconn/s: 0.00
[ 181s ] thds: 36 tps: 212.99 qps: 6644.62 (r/w/o: 3039.83/3098.82/505.97) lat (ms,95%): 442.73 err/s 41.00 reconn/s: 0.00
[ 182s ] thds: 36 tps: 166.99 qps: 5481.79 (r/w/o: 2481.91/2597.90/401.98) lat (ms,95%): 657.93 err/s 36.00 reconn/s: 0.00
[ 183s ] thds: 36 tps: 213.00 qps: 6173.88 (r/w/o: 2795.94/2881.94/495.99) lat (ms,95%): 539.71 err/s 37.00 reconn/s: 0.00
[ 184s ] thds: 36 tps: 215.01 qps: 6541.45 (r/w/o: 2970.20/3059.21/512.04) lat (ms,95%): 549.52 err/s 42.00 reconn/s: 0.00
[ 185s ] thds: 36 tps: 227.00 qps: 6743.04 (r/w/o: 3057.02/3138.02/548.00) lat (ms,95%): 434.83 err/s 48.00 reconn/s: 0.00
[ 186s ] thds: 36 tps: 242.99 qps: 6968.74 (r/w/o: 3144.88/3203.88/619.98) lat (ms,95%): 475.79 err/s 67.00 reconn/s: 0.00
[ 187s ] thds: 36 tps: 193.02 qps: 5346.45 (r/w/o: 2406.20/2470.21/470.04) lat (ms,95%): 484.44 err/s 42.00 reconn/s: 0.00
[ 188s ] thds: 36 tps: 167.98 qps: 5027.53 (r/w/o: 2262.79/2364.78/399.96) lat (ms,95%): 719.92 err/s 32.00 reconn/s: 0.00
[ 189s ] thds: 36 tps: 174.00 qps: 5546.11 (r/w/o: 2504.05/2622.05/420.01) lat (ms,95%): 580.02 err/s 36.00 reconn/s: 0.00
[ 190s ] thds: 36 tps: 175.00 qps: 5598.98 (r/w/o: 2520.99/2665.99/412.00) lat (ms,95%): 549.52 err/s 31.00 reconn/s: 0.00
[ 191s ] thds: 36 tps: 186.00 qps: 5206.00 (r/w/o: 2343.00/2393.00/470.00) lat (ms,95%): 601.29 err/s 51.00 reconn/s: 0.00
[ 192s ] thds: 36 tps: 185.01 qps: 5669.16 (r/w/o: 2554.07/2655.07/460.01) lat (ms,95%): 657.93 err/s 47.00 reconn/s: 0.00
[ 193s ] thds: 36 tps: 207.00 qps: 6328.03 (r/w/o: 2862.01/2960.02/506.00) lat (ms,95%): 601.29 err/s 46.00 reconn/s: 0.00
[ 194s ] thds: 36 tps: 200.00 qps: 5996.90 (r/w/o: 2742.95/2757.95/495.99) lat (ms,95%): 623.33 err/s 49.00 reconn/s: 0.00
[ 195s ] thds: 36 tps: 212.01 qps: 6605.23 (r/w/o: 2986.10/3111.11/508.02) lat (ms,95%): 493.24 err/s 42.00 reconn/s: 0.00
[ 196s ] thds: 36 tps: 215.99 qps: 6428.71 (r/w/o: 2921.87/2988.87/517.98) lat (ms,95%): 511.33 err/s 43.00 reconn/s: 0.00
[ 197s ] thds: 36 tps: 211.00 qps: 5988.88 (r/w/o: 2698.94/2803.94/485.99) lat (ms,95%): 484.44 err/s 33.00 reconn/s: 0.00
[ 198s ] thds: 36 tps: 197.00 qps: 5938.97 (r/w/o: 2686.99/2767.98/484.00) lat (ms,95%): 559.50 err/s 45.00 reconn/s: 0.00
[ 199s ] thds: 36 tps: 234.01 qps: 7084.36 (r/w/o: 3231.16/3317.17/536.03) lat (ms,95%): 502.20 err/s 34.00 reconn/s: 0.00
[ 200s ] thds: 36 tps: 253.99 qps: 7169.72 (r/w/o: 3228.87/3324.87/615.98) lat (ms,95%): 397.39 err/s 55.00 reconn/s: 0.00
[ 201s ] thds: 36 tps: 210.98 qps: 6886.50 (r/w/o: 3143.77/3254.76/487.96) lat (ms,95%): 475.79 err/s 34.00 reconn/s: 0.00
[ 202s ] thds: 36 tps: 249.02 qps: 7169.59 (r/w/o: 3232.27/3321.28/616.05) lat (ms,95%): 404.61 err/s 59.00 reconn/s: 0.00
[ 203s ] thds: 36 tps: 242.96 qps: 7206.74 (r/w/o: 3264.43/3358.41/583.90) lat (ms,95%): 419.45 err/s 49.99 reconn/s: 0.00
[ 204s ] thds: 36 tps: 206.04 qps: 6322.22 (r/w/o: 2870.55/2941.57/510.10) lat (ms,95%): 530.08 err/s 50.01 reconn/s: 0.00
[ 205s ] thds: 36 tps: 259.01 qps: 7061.14 (r/w/o: 3184.06/3241.07/636.01) lat (ms,95%): 411.96 err/s 59.00 reconn/s: 0.00
[ 206s ] thds: 36 tps: 214.99 qps: 6565.80 (r/w/o: 2988.91/3066.91/509.98) lat (ms,95%): 404.61 err/s 41.00 reconn/s: 0.00
[ 207s ] thds: 36 tps: 229.00 qps: 7226.88 (r/w/o: 3286.95/3397.95/541.99) lat (ms,95%): 427.07 err/s 43.00 reconn/s: 0.00
[ 208s ] thds: 36 tps: 233.01 qps: 6833.38 (r/w/o: 3105.17/3188.18/540.03) lat (ms,95%): 390.30 err/s 39.00 reconn/s: 0.00
[ 209s ] thds: 36 tps: 231.01 qps: 6238.22 (r/w/o: 2824.10/2870.10/544.02) lat (ms,95%): 363.18 err/s 42.00 reconn/s: 0.00
[ 210s ] thds: 36 tps: 213.98 qps: 6495.53 (r/w/o: 2937.79/3065.78/491.96) lat (ms,95%): 467.30 err/s 33.00 reconn/s: 0.00
[ 211s ] thds: 36 tps: 167.00 qps: 5191.02 (r/w/o: 2346.01/2447.01/398.00) lat (ms,95%): 612.21 err/s 34.00 reconn/s: 0.00
[ 212s ] thds: 36 tps: 189.00 qps: 5474.94 (r/w/o: 2471.97/2558.97/444.00) lat (ms,95%): 682.06 err/s 34.00 reconn/s: 0.00
[ 213s ] thds: 36 tps: 208.00 qps: 6574.14 (r/w/o: 2998.06/3098.07/478.01) lat (ms,95%): 590.56 err/s 32.00 reconn/s: 0.00
[ 214s ] thds: 36 tps: 204.00 qps: 6327.04 (r/w/o: 2879.02/2968.02/480.00) lat (ms,95%): 450.77 err/s 39.00 reconn/s: 0.00
[ 215s ] thds: 36 tps: 224.00 qps: 6270.12 (r/w/o: 2822.06/2897.06/551.01) lat (ms,95%): 404.61 err/s 53.00 reconn/s: 0.00
[ 216s ] thds: 36 tps: 227.00 qps: 6479.00 (r/w/o: 2933.00/3003.00/543.00) lat (ms,95%): 404.61 err/s 45.00 reconn/s: 0.00
[ 217s ] thds: 36 tps: 219.00 qps: 6354.91 (r/w/o: 2856.96/2977.96/519.99) lat (ms,95%): 419.45 err/s 42.00 reconn/s: 0.00
[ 218s ] thds: 36 tps: 227.00 qps: 6533.10 (r/w/o: 2947.04/3056.05/530.01) lat (ms,95%): 419.45 err/s 41.00 reconn/s: 0.00
[ 219s ] thds: 36 tps: 220.98 qps: 6291.53 (r/w/o: 2837.79/2927.78/525.96) lat (ms,95%): 383.33 err/s 42.00 reconn/s: 0.00
[ 220s ] thds: 36 tps: 213.01 qps: 6263.24 (r/w/o: 2831.11/2945.11/487.02) lat (ms,95%): 427.07 err/s 31.00 reconn/s: 0.00
[ 221s ] thds: 36 tps: 205.00 qps: 6211.08 (r/w/o: 2816.04/2906.04/489.01) lat (ms,95%): 397.39 err/s 39.00 reconn/s: 0.00
[ 222s ] thds: 36 tps: 219.00 qps: 6420.96 (r/w/o: 2913.98/3006.98/500.00) lat (ms,95%): 390.30 err/s 32.00 reconn/s: 0.00
[ 223s ] thds: 36 tps: 211.00 qps: 6355.13 (r/w/o: 2874.06/2963.06/518.01) lat (ms,95%): 376.49 err/s 48.00 reconn/s: 0.00
[ 224s ] thds: 36 tps: 224.00 qps: 6325.86 (r/w/o: 2859.94/2929.94/535.99) lat (ms,95%): 419.45 err/s 45.00 reconn/s: 0.00
[ 225s ] thds: 36 tps: 216.00 qps: 6461.93 (r/w/o: 2928.97/3024.97/507.99) lat (ms,95%): 419.45 err/s 41.00 reconn/s: 0.00
[ 226s ] thds: 36 tps: 235.00 qps: 6501.96 (r/w/o: 2934.98/3006.98/560.00) lat (ms,95%): 390.30 err/s 46.00 reconn/s: 0.00
[ 227s ] thds: 36 tps: 222.00 qps: 6317.11 (r/w/o: 2857.05/2938.05/522.01) lat (ms,95%): 376.49 err/s 40.00 reconn/s: 0.00
[ 228s ] thds: 36 tps: 158.48 qps: 4464.80 (r/w/o: 2014.96/2083.83/366.01) lat (ms,95%): 442.73 err/s 24.53 reconn/s: 0.00
[ 229s ] thds: 36 tps: 115.00 qps: 3323.08 (r/w/o: 1515.04/1539.04/269.01) lat (ms,95%): 539.71 err/s 20.00 reconn/s: 0.00
[ 230s ] thds: 36 tps: 96.00 qps: 3380.06 (r/w/o: 1560.03/1603.03/217.00) lat (ms,95%): 1678.14 err/s 13.00 reconn/s: 0.00
[ 231s ] thds: 36 tps: 129.99 qps: 3500.83 (r/w/o: 1581.92/1637.92/280.99) lat (ms,95%): 646.19 err/s 15.00 reconn/s: 0.00
[ 232s ] thds: 36 tps: 122.00 qps: 3695.86 (r/w/o: 1659.94/1740.93/294.99) lat (ms,95%): 1506.29 err/s 26.00 reconn/s: 0.00
[ 233s ] thds: 36 tps: 124.99 qps: 3598.82 (r/w/o: 1613.92/1718.92/265.99) lat (ms,95%): 1280.93 err/s 9.00 reconn/s: 0.00
[ 234s ] thds: 36 tps: 127.01 qps: 3625.42 (r/w/o: 1626.19/1705.20/294.03) lat (ms,95%): 1903.57 err/s 20.00 reconn/s: 0.00
[ 235s ] thds: 36 tps: 109.99 qps: 3553.67 (r/w/o: 1614.85/1672.85/265.98) lat (ms,95%): 1453.01 err/s 23.00 reconn/s: 0.00
[ 236s ] thds: 36 tps: 113.01 qps: 3368.33 (r/w/o: 1522.15/1578.16/268.03) lat (ms,95%): 977.74 err/s 21.00 reconn/s: 0.00
[ 237s ] thds: 36 tps: 125.75 qps: 3533.88 (r/w/o: 1592.18/1657.53/284.18) lat (ms,95%): 669.89 err/s 18.81 reconn/s: 0.00
[ 238s ] thds: 36 tps: 110.09 qps: 3330.97 (r/w/o: 1511.97/1563.48/255.53) lat (ms,95%): 1304.21 err/s 16.16 reconn/s: 0.00
[ 239s ] thds: 36 tps: 114.00 qps: 3440.01 (r/w/o: 1561.01/1611.01/268.00) lat (ms,95%): 511.33 err/s 21.00 reconn/s: 0.00
[ 240s ] thds: 36 tps: 128.00 qps: 3608.08 (r/w/o: 1639.04/1690.04/279.01) lat (ms,95%): 1938.16 err/s 13.00 reconn/s: 0.00
[ 241s ] thds: 36 tps: 112.00 qps: 3484.87 (r/w/o: 1585.94/1649.94/248.99) lat (ms,95%): 530.08 err/s 13.00 reconn/s: 0.00
[ 242s ] thds: 36 tps: 130.01 qps: 3831.32 (r/w/o: 1727.14/1805.15/299.02) lat (ms,95%): 2009.23 err/s 20.00 reconn/s: 0.00
[ 243s ] thds: 36 tps: 124.00 qps: 3601.93 (r/w/o: 1626.97/1687.97/286.99) lat (ms,95%): 1973.38 err/s 19.00 reconn/s: 0.00
[ 244s ] thds: 36 tps: 114.00 qps: 3523.95 (r/w/o: 1600.98/1644.98/278.00) lat (ms,95%): 1561.52 err/s 28.00 reconn/s: 0.00
[ 245s ] thds: 36 tps: 105.00 qps: 3435.12 (r/w/o: 1569.05/1636.06/230.01) lat (ms,95%): 502.20 err/s 10.00 reconn/s: 0.00
[ 246s ] thds: 36 tps: 113.00 qps: 3325.96 (r/w/o: 1527.98/1525.98/272.00) lat (ms,95%): 2198.52 err/s 23.00 reconn/s: 0.00
[ 247s ] thds: 36 tps: 118.99 qps: 3331.84 (r/w/o: 1510.93/1563.92/256.99) lat (ms,95%): 590.56 err/s 10.00 reconn/s: 0.00
[ 248s ] thds: 36 tps: 117.00 qps: 3386.10 (r/w/o: 1519.04/1582.04/285.01) lat (ms,95%): 1708.63 err/s 25.00 reconn/s: 0.00
[ 249s ] thds: 36 tps: 99.99 qps: 3310.63 (r/w/o: 1511.83/1565.82/232.97) lat (ms,95%): 1533.66 err/s 18.00 reconn/s: 0.00
[ 250s ] thds: 36 tps: 109.01 qps: 3298.28 (r/w/o: 1512.13/1548.13/238.02) lat (ms,95%): 773.68 err/s 11.00 reconn/s: 0.00
[ 251s ] thds: 36 tps: 133.99 qps: 3722.85 (r/w/o: 1658.93/1754.93/308.99) lat (ms,95%): 1013.60 err/s 20.00 reconn/s: 0.00
[ 252s ] thds: 36 tps: 109.00 qps: 3520.03 (r/w/o: 1609.02/1660.02/251.00) lat (ms,95%): 1618.78 err/s 19.00 reconn/s: 0.00
[ 253s ] thds: 36 tps: 112.00 qps: 3372.95 (r/w/o: 1523.98/1592.98/256.00) lat (ms,95%): 1050.76 err/s 16.00 reconn/s: 0.00
[ 254s ] thds: 36 tps: 126.01 qps: 3748.17 (r/w/o: 1713.08/1760.08/275.01) lat (ms,95%): 1561.52 err/s 13.00 reconn/s: 0.00
[ 255s ] thds: 36 tps: 122.00 qps: 3523.00 (r/w/o: 1603.00/1623.00/297.00) lat (ms,95%): 1708.63 err/s 26.00 reconn/s: 0.00
[ 256s ] thds: 36 tps: 121.01 qps: 3527.19 (r/w/o: 1602.09/1640.09/285.02) lat (ms,95%): 1506.29 err/s 21.00 reconn/s: 0.00
[ 257s ] thds: 36 tps: 129.91 qps: 3658.19 (r/w/o: 1653.42/1703.61/301.16) lat (ms,95%): 1506.29 err/s 22.64 reconn/s: 0.00
[ 258s ] thds: 36 tps: 106.72 qps: 3176.10 (r/w/o: 1442.21/1461.52/272.38) lat (ms,95%): 1280.93 err/s 28.46 reconn/s: 0.00
[ 259s ] thds: 36 tps: 116.99 qps: 3482.67 (r/w/o: 1585.85/1646.84/249.98) lat (ms,95%): 669.89 err/s 9.00 reconn/s: 0.00
[ 260s ] thds: 36 tps: 123.00 qps: 3574.99 (r/w/o: 1617.99/1672.99/284.00) lat (ms,95%): 1533.66 err/s 20.00 reconn/s: 0.00
[ 261s ] thds: 36 tps: 125.00 qps: 3569.14 (r/w/o: 1618.06/1660.07/291.01) lat (ms,95%): 1191.92 err/s 24.00 reconn/s: 0.00
[ 262s ] thds: 36 tps: 106.84 qps: 3428.83 (r/w/o: 1547.23/1618.46/263.15) lat (ms,95%): 1678.14 err/s 23.74 reconn/s: 0.00
[ 263s ] thds: 36 tps: 103.12 qps: 3353.57 (r/w/o: 1549.90/1564.06/239.61) lat (ms,95%): 1708.63 err/s 16.18 reconn/s: 0.00
[ 264s ] thds: 36 tps: 107.00 qps: 3398.00 (r/w/o: 1550.00/1603.00/245.00) lat (ms,95%): 1191.92 err/s 16.00 reconn/s: 0.00
[ 265s ] thds: 36 tps: 111.99 qps: 3401.84 (r/w/o: 1544.93/1589.93/266.99) lat (ms,95%): 746.32 err/s 21.00 reconn/s: 0.00
[ 266s ] thds: 36 tps: 129.00 qps: 3545.06 (r/w/o: 1623.03/1644.03/278.00) lat (ms,95%): 682.06 err/s 10.00 reconn/s: 0.00
[ 267s ] thds: 36 tps: 116.99 qps: 3603.75 (r/w/o: 1619.89/1681.88/301.98) lat (ms,95%): 1479.41 err/s 36.00 reconn/s: 0.00
[ 268s ] thds: 36 tps: 126.00 qps: 3512.12 (r/w/o: 1587.05/1655.06/270.01) lat (ms,95%): 1589.90 err/s 10.00 reconn/s: 0.00
[ 269s ] thds: 36 tps: 123.01 qps: 3567.16 (r/w/o: 1628.07/1655.08/284.01) lat (ms,95%): 1453.01 err/s 19.00 reconn/s: 0.00
[ 270s ] thds: 36 tps: 120.00 qps: 3458.03 (r/w/o: 1588.01/1619.01/251.00) lat (ms,95%): 520.62 err/s 6.00 reconn/s: 0.00
[ 271s ] thds: 36 tps: 122.99 qps: 3686.67 (r/w/o: 1678.85/1740.84/266.98) lat (ms,95%): 1427.08 err/s 11.00 reconn/s: 0.00
[ 272s ] thds: 36 tps: 110.01 qps: 3590.39 (r/w/o: 1623.17/1703.18/264.03) lat (ms,95%): 2009.23 err/s 22.00 reconn/s: 0.00
[ 273s ] thds: 36 tps: 142.00 qps: 3828.09 (r/w/o: 1734.04/1777.04/317.01) lat (ms,95%): 1506.29 err/s 18.00 reconn/s: 0.00
[ 274s ] thds: 36 tps: 125.98 qps: 3672.53 (r/w/o: 1676.78/1702.78/292.96) lat (ms,95%): 1533.66 err/s 20.00 reconn/s: 0.00
[ 275s ] thds: 36 tps: 102.99 qps: 3538.74 (r/w/o: 1615.88/1667.88/254.98) lat (ms,95%): 1533.66 err/s 25.00 reconn/s: 0.00
[ 276s ] thds: 36 tps: 113.01 qps: 3444.37 (r/w/o: 1574.17/1596.17/274.03) lat (ms,95%): 1401.61 err/s 25.00 reconn/s: 0.00
[ 277s ] thds: 36 tps: 121.00 qps: 3603.13 (r/w/o: 1642.06/1698.06/263.01) lat (ms,95%): 733.00 err/s 11.00 reconn/s: 0.00
[ 278s ] thds: 36 tps: 118.01 qps: 3370.16 (r/w/o: 1517.07/1561.07/292.01) lat (ms,95%): 2009.23 err/s 30.00 reconn/s: 0.00
[ 279s ] thds: 36 tps: 113.00 qps: 3488.91 (r/w/o: 1576.96/1655.96/255.99) lat (ms,95%): 694.45 err/s 14.00 reconn/s: 0.00
[ 280s ] thds: 36 tps: 120.98 qps: 3481.54 (r/w/o: 1572.79/1622.78/285.96) lat (ms,95%): 1213.57 err/s 23.00 reconn/s: 0.00
[ 281s ] thds: 36 tps: 112.01 qps: 3454.20 (r/w/o: 1554.09/1634.09/266.02) lat (ms,95%): 1533.66 err/s 20.00 reconn/s: 0.00
[ 282s ] thds: 36 tps: 112.84 qps: 3361.33 (r/w/o: 1540.11/1561.89/259.32) lat (ms,95%): 995.51 err/s 18.81 reconn/s: 0.00
[ 283s ] thds: 36 tps: 111.15 qps: 3384.04 (r/w/o: 1540.96/1583.40/259.69) lat (ms,95%): 1013.60 err/s 19.20 reconn/s: 0.00
[ 284s ] thds: 36 tps: 115.99 qps: 3482.66 (r/w/o: 1567.85/1659.84/254.98) lat (ms,95%): 569.67 err/s 11.00 reconn/s: 0.00
[ 285s ] thds: 36 tps: 142.01 qps: 3708.33 (r/w/o: 1679.15/1709.15/320.03) lat (ms,95%): 1506.29 err/s 18.00 reconn/s: 0.00
[ 286s ] thds: 36 tps: 127.98 qps: 3628.51 (r/w/o: 1639.78/1671.77/316.96) lat (ms,95%): 2009.23 err/s 32.00 reconn/s: 0.00
[ 287s ] thds: 36 tps: 98.02 qps: 3376.58 (r/w/o: 1536.26/1608.28/232.04) lat (ms,95%): 1069.86 err/s 19.00 reconn/s: 0.00
[ 288s ] thds: 36 tps: 104.99 qps: 3399.76 (r/w/o: 1545.89/1618.89/234.98) lat (ms,95%): 682.06 err/s 13.00 reconn/s: 0.00
[ 289s ] thds: 36 tps: 126.00 qps: 3777.13 (r/w/o: 1716.06/1775.06/286.01) lat (ms,95%): 1050.76 err/s 17.00 reconn/s: 0.00
[ 290s ] thds: 36 tps: 136.97 qps: 3528.33 (r/w/o: 1593.70/1603.70/330.94) lat (ms,95%): 1561.52 err/s 28.99 reconn/s: 0.00
[ 291s ] thds: 36 tps: 122.03 qps: 3337.74 (r/w/o: 1491.33/1543.34/303.07) lat (ms,95%): 1191.92 err/s 29.01 reconn/s: 0.00
[ 292s ] thds: 36 tps: 113.99 qps: 3266.85 (r/w/o: 1468.93/1525.93/271.99) lat (ms,95%): 1032.01 err/s 22.00 reconn/s: 0.00
[ 293s ] thds: 36 tps: 120.98 qps: 3475.32 (r/w/o: 1588.69/1610.69/275.95) lat (ms,95%): 657.93 err/s 19.00 reconn/s: 0.00
[ 294s ] thds: 36 tps: 125.03 qps: 3763.78 (r/w/o: 1704.35/1785.37/274.06) lat (ms,95%): 502.20 err/s 13.00 reconn/s: 0.00
[ 295s ] thds: 36 tps: 118.99 qps: 3704.76 (r/w/o: 1670.89/1746.89/286.98) lat (ms,95%): 1648.20 err/s 25.00 reconn/s: 0.00
[ 296s ] thds: 36 tps: 123.02 qps: 3680.46 (r/w/o: 1660.21/1717.21/303.04) lat (ms,95%): 1427.08 err/s 28.00 reconn/s: 0.00
[ 297s ] thds: 36 tps: 105.99 qps: 3644.59 (r/w/o: 1645.82/1742.81/255.97) lat (ms,95%): 1453.01 err/s 24.00 reconn/s: 0.00
[ 298s ] thds: 36 tps: 114.92 qps: 3346.56 (r/w/o: 1494.91/1575.85/275.80) lat (ms,95%): 1401.61 err/s 23.98 reconn/s: 0.00
[ 299s ] thds: 36 tps: 57.04 qps: 1903.24 (r/w/o: 852.55/912.59/138.09) lat (ms,95%): 1803.47 err/s 12.01 reconn/s: 0.00
[ 300s ] thds: 36 tps: 135.02 qps: 3515.65 (r/w/o: 1575.29/1617.30/323.06) lat (ms,95%): 1771.29 err/s 27.00 reconn/s: 0.00
[ 301s ] thds: 33 tps: 23.99 qps: 483.90 (r/w/o: 210.96/244.95/27.99) lat (ms,95%): 2362.72 err/s 3.00 reconn/s: 0.00
[ 302s ] thds: 33 tps: 11.00 qps: 224.01 (r/w/o: 99.01/105.01/20.00) lat (ms,95%): 1973.38 err/s 4.00 reconn/s: 0.00
 ```
</details>

<details>
<summary>SQL statistics:</summary>

```console
SQL statistics:
    queries performed:
        read:                            628628
        write:                           649440
        other:                           110800
        total:                           1388868
    transactions:                        46120  (152.66 per sec.)
    queries:                             1388868 (4597.37 per sec.)
    ignored errors:                      9465   (31.33 per sec.)
    reconnects:                          0      (0.00 per sec.)
General statistics:
    total time:                          302.0985s
    total number of events:              46120
Latency (ms):
         min:                                    0.71
         avg:                                  234.66
         max:                                 5309.59
         95th percentile:                      719.92
         sum:                             10822515.55
Threads fairness:
    events (avg/stddev):           1281.1111/31.07
    execution time (avg/stddev):   300.6254/0.62
```
</details>

### График

![изображение](https://user-images.githubusercontent.com/93687317/142770100-d2b1e8f0-3d65-4361-8c3e-2a76fecf061f.png)
