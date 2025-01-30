### Create a dashboard:
* From VM overview choose monitoring and pin the desired metrics. choose create new dashboard and shared. 
* From dashboard hub edit metrics to view in one line.
* Azure provides a 1-minute interval checks
* Change Local time to last 30 minutes and save.

### Installing Apache Bench:
* on our local machine ssh to the vm and run this code: 
  ```
    sudo apt-get install apache2-utils 
    ```

* to overwork the CPU with requests:

  ```
    ab -n 1000 -c 100 http://172.187.147.115/
    ```
    - notice how CPU utilization has gone up on the dashboard 
  

![alt text](<Screenshot 2025-01-30 124829.png>)

 