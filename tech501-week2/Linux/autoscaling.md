### autoscaling and load balancers:

- Autoscaling is important for high availability and scalability.
- There are two types of scaling; horizontal and vertical. check the diagram.
- in a scale set you have to plan ahead what are the default, max, min instances and the architecture. 

![
](<Screenshot 2025-01-30 162607.png>)

![alt text](<Screenshot 2025-01-30 162651.png>)


![alt text](<Screenshot 2025-01-30 162737.png>)

- From scale set
    name:tech501-maram-sparta-app-vmss
    - Availability zones: tick all 3 zones
    - Orchestration mode: Uniform
    - scaling mode: Autoscaling and change config max:3, min:2, default:2
    - from images choose your own image
    - username:adminuser
    - SSH: use existing key and choose tech501-maram-az-key
    - from discs: standard
    - Networking:
      - choose maram-vnet; public subnet
      - azure load balancer
      - Create a new load balancer (tech501-maram-sparta-app-lb)
    - Health; 
      - enable application health monitoring
      - enable automatic repairs

* To ssh to our instances choose a healthy instance and ssh; 
    - ssh -i ~/.ssh/tech501-maram-az-key -p 50000 adminuser@20.26.248.231
    - use the load balancer public IP
    - add -p 50000 for the first instance and to connect to the second add -p 50001 and so on.


* After stopping the vm scale set. you have to reimage one of the instances so the app would work, this allows for the app disc to copy everything again into a new disc with the userdata. 
* When deleting scale set we should delete the load balncer seperately. 
* In a production setting when don't ssh to instances to make changes/updates. Updates are done from the scale set by changing the image or replacing it systematically. 