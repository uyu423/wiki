---
title: ab - Apache HTTP server benchmarking tool
description: 
published: true
date: 2023-02-09T11:54:28.380Z
tags: http, terminal, ab, benchmark, linux
editor: markdown
dateCreated: 2023-02-09T07:22:40.676Z
---

The Apache HTTP server benchmarking tool, also known as "ab", is a tool used to measure the performance of web servers. The tool simulates multiple client requests to a web server and provides information on the server's response time and its ability to handle a large number of requests. In this article, we will discuss the basics of using the ab tool, its features and a sample usage.

## Getting Started with ab

The ab tool is included in the Apache HTTP Server package, which can be installed on a variety of operating systems, including Windows, macOS, and Linux. To use the ab tool, you must first have the Apache HTTP Server or `apache2-utils` installed on your system.

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

Suppose we want to test the performance of a web server located at `http://google.com`. We can use the following command to perform 500 requests with 20 concurrent requests:

```bash
ab -n 500 -c 20 http://google.com/
```

The output of this command will provide information about the server's response time, the number of requests per second, the time taken for the test, and various other performance metrics.

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


## Conclusion

The ab tool is an essential tool for testing the performance of web servers. It provides a quick and easy way to simulate multiple client requests to a web server and measure its response time and ability to handle a large number of requests. By using the various options and parameters available with the ab tool, you can customize the behavior of the tool to fit your specific testing needs.

> **Tip: How to use the ab tool effectively?**
> 
> Using the Apache HTTP server benchmarking tool (ab) effectively requires understanding the purpose of the tool, the available options, and the factors that can affect its results. Here are some tips to help you use the ab tool effectively:
> 
> 1. Determine the Purpose of the Test: Before using the ab tool, determine the purpose of the test. This will help you to choose the right options and parameters to meet your testing goals. For example, if you want to test the maximum number of requests per second that a web server can handle, you may want to use a large number of concurrent requests and a large number of total requests.
> 
> 2. Choose the Right Options: Choose the options and parameters that best fit the purpose of your test. For example, if you want to test the maximum number of concurrent requests a web server can handle, use a large value for the `-c` option. Similarly, if you want to test the server's response time under a high load, use a large value for the `-n` option.
> 
> 3. Use Realistic Test Data: Use realistic test data that closely mimics the actual data and workload that the web server will face in production. This will provide more accurate results and help you to identify any bottlenecks or performance issues that may arise in a real-world scenario.
> 
> 4. Monitor the Server's Resource Usage: Monitor the web server's resource usage, such as CPU and memory utilization, during the test to see if it is being stressed or if there are any resource constraints that may affect the performance.
> 
> 5. Repeat the Test Multiple Times: Repeat the test multiple times and average the results to account for any variations in the results. This will provide a more accurate picture of the web server's performance.
> 
> 6. Use a Representative Test Environment: Use a test environment that closely represents the production environment in terms of hardware, network, and other relevant factors. This will ensure that the test results are representative of the web server's actual performance in production.
> 
> 7. Use the Correct URL: Use the correct URL when testing the web server. For example, if you are testing a web application, use the URL of the specific page that you want to test.

> **Warnings**
> 
> There are a few things you should be wary of when using the Apache HTTP server benchmarking tool (ab):
> 
> 1. Test Environment: The test environment, including the hardware, network, and other relevant factors, can greatly affect the results of the test. Make sure to use a test environment that closely represents the production environment to ensure accurate results.
> 
> 2. Caching Effects: Web servers often use caching mechanisms to improve performance. This can cause test results to be misleading if the cache is not cleared before each test run. Be sure to clear the cache before each test to eliminate caching effects.
> 
> 3. Load on the Test Machine: The load on the machine running the ab tool can affect the results of the test. Be sure to run the ab tool on a machine with minimal load to eliminate any potential impact on the results.
> 
> 4. Network Latency: Network latency can greatly affect the results of the test, especially when testing web servers located on remote machines. Be sure to test the web server from a location with low network latency to get accurate results.
> 
> 5. Concurrent Requests: The number of concurrent requests specified with the `-c` option can affect the results of the test. A high number of concurrent requests can stress the web server and produce inaccurate results. On the other hand, a low number of concurrent requests may not provide a realistic picture of the web server's performance. Choose the number of concurrent requests carefully to get accurate results.
> 
> 6. Realistic Test Data: Using unrealistic or artificial test data can result in inaccurate results. Make sure to use realistic test data that closely mimics the actual data and workload that the web server will face in production.
> 
> 7. Other Factors: There may be other factors, such as network congestion or firewall restrictions, that can affect the results of the test. Be aware of these factors and take them into account when interpreting the results.
> 
> .
{.is-warning}
