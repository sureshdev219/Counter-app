# Counter-app

Deploy flask-counter-app on Kubernetes

Steps Followed:
  1. Here I used 2 aws ec2 instances to deploy application into Kubernetes Cluster( General purpose
t2.large 2 vCPU 8 GB memory)
  
  2. Cloned docker image from https://hub.docker.com/r/tarunbhardwaj/flask-counter-app
  
  3. Deployed redis with 2 replica by running below two commands.
  Created 2 files --> redis-deployments.yml, redis-services.yml
        kubectl create -f redis-deployment.yml
        kubectl create -f redis-service.yml
  
  4. Deployed flask-counter-app with 2 replicas by running below two commands.
  Created 2 files --> deployment.yml, service.yml 
        kubectl create -f deployment.yml
        kubectl create -f service.yml
  Note: Here i am using NodePort as a service
  
  5. To check the pods status
        kubectl get pods
    
  6. To check the services status
        kubectl get svc
    
  7. Test the application by using ipaddress along with port number or open it in web browser
        curl 3.237.9.86:30001/  or 3.237.9.86:30001/
  
  8. Also tested the deployment via apache benchmark (ab):
        ab -l -c 100 -t 10 3.237.9.86:30001/
  
  Here the output look like this below
  
ubuntu@ip-172-31-89-203:~$ ab -l -c 100 -t 10 3.237.9.86:30001/

This is ApacheBench, Version 2.3 <$Revision: 1807734 $>

Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/

Licensed to The Apache Software Foundation, http://www.apache.org/

  Benchmarking 3.237.9.86 (be patient)

  Completed 5000 requests
  
  Completed 10000 requests
  
  Completed 15000 requests
  
  Finished 15404 requests


  Server Software:        gunicorn/19.9.0
  
  Server Hostname:        3.237.9.86  
  
  Server Port:            30001

  Document Path:          /
  
  Document Length:        Variable

  Concurrency Level:      100
  
  Time taken for tests:   10.001 seconds
  
  Complete requests:      15404
  
  Failed requests:        0
  
  Total transferred:      2691064 bytes
  
  HTML transferred:       225784 bytes
  
  Requests per second:    1540.24 [#/sec] (mean)
  
  Time per request:       64.925 [ms] (mean)  
  
  Time per request:       0.649 [ms] (mean, across all concurrent requests)
  
  Transfer rate:          262.77 [Kbytes/sec] received

  Connection Times (ms)
  
                min  mean[+/-sd] median   max  
  Connect:        1    2  14.2      1    1022
  
  Processing:     2   63  56.0     51     173
  
  Waiting:        2   63  55.9     51     173
  
  Total:          3   65  57.9     54    1156


  Percentage of the requests served within a certain time (ms)
  
    50%     54
    
    66%    113
    
    75%    122
    
    80%    126
    
    90%    136
    
    95%    143
    
    98%    149
    
    99%    152
    
    100%   1156 (longest request)


Note: Here i installed apache2 to check apache benchmark test.
