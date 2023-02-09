---
title: ab - Apache HTTP server benchmarking tool
description: 
published: true
date: 2023-02-09T07:22:51.889Z
tags: ab, benchmark, http, linux, terminal
editor: markdown
dateCreated: 2023-02-09T07:22:40.676Z
---

The Apache HTTP server benchmarking tool, also known as "ab", is a tool used to measure the performance of web servers. The tool simulates multiple client requests to a web server and provides information on the server's response time and its ability to handle a large number of requests. In this article, we will discuss the basics of using the ab tool, its features and a sample usage.

## Getting Started with ab

The ab tool is included in the Apache HTTP Server package, which can be installed on a variety of operating systems, including Windows, macOS, and Linux. To use the ab tool, you must first have the Apache HTTP Server installed on your system.

## Usage

The basic syntax of the ab tool is as follows:

```bash
ab [options] [URL]
```

Where `options` are the various flags and parameters that can be used to customize the behavior of the tool, and `URL` is the URL of the web server that you want to test.

## Options

The following are some of the most commonly used options with the ab tool:

* `-n`: The number of requests to perform.

* `-c`: The number of concurrent requests to perform.

* `-k`: Enables the HTTP KeepAlive feature, allowing multiple requests to be sent over a single HTTP connection.

* `-t`: The maximum time, in seconds, that the ab tool will run.

* `-p`: The file containing post data to include in the request.

* `-T`: The content type of the data included in the request.

## Sample Usage

Suppose we want to test the performance of a web server located at `http://www.example.com`. We can use the following command to perform 1000 requests with 100 concurrent requests:

```bash
ab -n 500 -c 20 http://google.com/
```
```
This is ApacheBench, Version 2.3 <$Revision: 1901567 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking google.com (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Finished 500 requests


Server Software:        gws
Server Hostname:        google.com
Server Port:            80

Document Path:          /
Document Length:        219 bytes

Concurrency Level:      20
Time taken for tests:   6.834 seconds
Complete requests:      500
Failed requests:        0
Non-2xx responses:      500
Total transferred:      264000 bytes
HTML transferred:       109500 bytes
Requests per second:    73.17 [#/sec] (mean)
Time per request:       273.344 [ms] (mean)
Time per request:       13.667 [ms] (mean, across all concurrent requests)
Transfer rate:          37.73 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       32   73  25.5     70     120
Processing:   129  173  33.4    166     428
Waiting:      126  171  33.3    165     428
Total:        163  246  55.5    239     471

Percentage of the requests served within a certain time (ms)
  50%    239
  66%    285
  75%    297
  80%    301
  90%    311
  95%    320
  98%    356
  99%    381
 100%    471 (longest request)
```

The output of this command will provide information about the server's response time, the number of requests per second, the time taken for the test, and various other performance metrics.

## Conclusion

The ab tool is an essential tool for testing the performance of web servers. It provides a quick and easy way to simulate multiple client requests to a web server and measure its response time and ability to handle a large number of requests. By using the various options and parameters available with the ab tool, you can customize the behavior of the tool to fit your specific testing needs.