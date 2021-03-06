# Simple real application simulation test

This test represents what a Swoole application/microservice should aim to be - use extensive caching, and very little and fast IO operations.
The amount of loaded classes does not affects the performance.
This test does 1000 reads from cache, loads 100 classes and performs 2 fast DB queries.

The results are:
- Swoole 100 / 10 000 - Requests per second: **2288.58**
- Apache/mod_php 100 / 10 000 - Requests per second: **1250.36**
- Swoole 500 / 10 000 - Requests per second: **2011.11**
- Apache/mod_php 500 / 10 000 - Requests per second: **774.52** with **196 failed requests**
- Swoole 1 000 / 10 000 - Requests per second: **2228.23**
- Apache/mod_php 1 000 / 10 000 - Requests per second: **failed with 7702 completed requests**


#### Swoole 100 / 10 000
```
root@vesko-dev /home/local/swoole_tests/swoole-performance-tests (master) # ab -c 100 -n 10000 -k http://192.168.0.233:8082/

[...]

Server Software:        swoole-http-server
Server Hostname:        192.168.0.233
Server Port:            8082

Document Path:          /
Document Length:        792 bytes

Concurrency Level:      100
Time taken for tests:   4.370 seconds
Complete requests:      10000
Failed requests:        0
Write errors:           0
Keep-Alive requests:    10000
Total transferred:      9460000 bytes
HTML transferred:       7920000 bytes
Requests per second:    2288.58 [#/sec] (mean)
Time per request:       43.695 [ms] (mean)
Time per request:       0.437 [ms] (mean, across all concurrent requests)
Transfer rate:          2114.25 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.9      0      12
Processing:     2   43  12.8     44     172
Waiting:        2   43  12.8     43     172
Total:          2   43  13.1     44     178

Percentage of the requests served within a certain time (ms)
  50%     44
  66%     47
  75%     49
  80%     51
  90%     61
  95%     64
  98%     69
  99%     84
 100%    178 (longest request)
```
#### Apache 100 / 10 000
```
root@vesko-dev /home/local/swoole_tests/swoole-performance-tests (master) # ab -c 100 -n 10000 -k http://192.168.0.233:8083/swoole_tests/swoole-performance-tests/simple_real_app_simulation/apache.php

[...]

Server Software:        Apache/2.4.25
Server Hostname:        192.168.0.233
Server Port:            8083

Document Path:          /swoole_tests/swoole-performance-tests/simple_real_app_simulation/apache.php
Document Length:        792 bytes

Concurrency Level:      100
Time taken for tests:   7.998 seconds
Complete requests:      10000
Failed requests:        0
Write errors:           0
Keep-Alive requests:    9961
Total transferred:      10447964 bytes
HTML transferred:       7920000 bytes
Requests per second:    1250.36 [#/sec] (mean)
Time per request:       79.977 [ms] (mean)
Time per request:       0.800 [ms] (mean, across all concurrent requests)
Transfer rate:          1275.76 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   1.6      0      22
Processing:     9   79  37.9     75     405
Waiting:        9   79  37.9     75     405
Total:          9   79  38.1     75     405

Percentage of the requests served within a certain time (ms)
  50%     75
  66%     85
  75%     94
  80%    101
  90%    124
  95%    146
  98%    180
  99%    208
 100%    405 (longest request)
```
#### Swoole 500 / 10 000
```
root@vesko-dev /home/local/swoole_tests/swoole-performance-tests (master) # ab -c 500 -n 10000 -k http://192.168.0.233:8082/

[...]

Server Software:        swoole-http-server
Server Hostname:        192.168.0.233
Server Port:            8082

Document Path:          /
Document Length:        792 bytes

Concurrency Level:      500
Time taken for tests:   4.972 seconds
Complete requests:      10000
Failed requests:        0
Write errors:           0
Keep-Alive requests:    10000
Total transferred:      9460000 bytes
HTML transferred:       7920000 bytes
Requests per second:    2011.11 [#/sec] (mean)
Time per request:       248.619 [ms] (mean)
Time per request:       0.497 [ms] (mean, across all concurrent requests)
Transfer rate:          1857.92 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    2   8.5      0      48
Processing:     3  240 200.1    225    1672
Waiting:        3  240 200.1    225    1672
Total:          3  242 206.1    225    1719

Percentage of the requests served within a certain time (ms)
  50%    225
  66%    232
  75%    236
  80%    240
  90%    251
  95%    267
  98%   1287
  99%   1337
 100%   1719 (longest request)
```
#### Aapche 500 / 10 000
```
root@vesko-dev /home/local/swoole_tests/swoole-performance-tests (master) # ab -c 500 -n 10000 -k http://192.168.0.233:8083/swoole_tests/swoole-performance-tests/simple_real_app_simulation/apache.php

[...]

Server Software:        Apache/2.4.25
Server Hostname:        192.168.0.233
Server Port:            8083

Document Path:          /swoole_tests/swoole-performance-tests/simple_real_app_simulation/apache.php
Document Length:        792 bytes

Concurrency Level:      500
Time taken for tests:   12.911 seconds
Complete requests:      10000
Failed requests:        196
   (Connect: 0, Receive: 0, Length: 196, Exceptions: 0)
Write errors:           0
Keep-Alive requests:    9805
Total transferred:      10246530 bytes
HTML transferred:       7765560 bytes
Requests per second:    774.52 [#/sec] (mean)
Time per request:       645.565 [ms] (mean)
Time per request:       1.291 [ms] (mean, across all concurrent requests)
Transfer rate:          775.01 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    1  15.7      0    1001
Processing:    10  362 1364.2    100   12775
Waiting:       10  268 1196.9    100   12775
Total:         10  364 1370.0    100   12826

Percentage of the requests served within a certain time (ms)
  50%    100
  66%    123
  75%    142
  80%    158
  90%    217
  95%    333
  98%   5005
  99%   7427
 100%  12826 (longest request)
```

#### Swoole 1 000 / 10 000
```
root@vesko-dev /home/local/swoole_tests/swoole-performance-tests (master) # ab -c 1000 -n 10000 -k http://192.168.0.233:8082/

[...]

Server Software:        swoole-http-server
Server Hostname:        192.168.0.233
Server Port:            8082

Document Path:          /
Document Length:        792 bytes

Concurrency Level:      1000
Time taken for tests:   4.488 seconds
Complete requests:      10000
Failed requests:        0
Write errors:           0
Keep-Alive requests:    10000
Total transferred:      9460000 bytes
HTML transferred:       7920000 bytes
Requests per second:    2228.23 [#/sec] (mean)
Time per request:       448.786 [ms] (mean)
Time per request:       0.449 [ms] (mean, across all concurrent requests)
Transfer rate:          2058.51 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    7  21.3      0     102
Processing:    74  418  62.9    418     638
Waiting:        3  418  62.9    418     638
Total:        105  425  56.2    420     678

Percentage of the requests served within a certain time (ms)
  50%    420
  66%    431
  75%    439
  80%    449
  90%    472
  95%    530
  98%    601
  99%    616
 100%    678 (longest request)
```
#### Apache 1 000 / 10 000
```
root@vesko-dev /home/local/swoole_tests/swoole-performance-tests (master) # ab -c 1000 -n 10000 -k http://192.168.0.233:8083/swoole_tests/swoole-performance-tests/simple_real_app_simulation/apache.php
This is ApacheBench, Version 2.3 <$Revision: 1430300 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 192.168.0.233 (be patient)
Completed 1000 requests
Completed 2000 requests
Completed 3000 requests
Completed 4000 requests
Completed 5000 requests
Completed 6000 requests
Completed 7000 requests
apr_socket_recv: Connection reset by peer (104)
Total of 7702 requests completed
```

