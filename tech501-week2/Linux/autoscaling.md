- [Creating a scale set:](#creating-a-scale-set)
  - [Connecting to instances:](#connecting-to-instances)
  - [Deleting a scale set:](#deleting-a-scale-set)

### Autoscaling and load balancers:

- Autoscaling is important for high availability and scalability.
- There are two types of scaling; horizontal and vertical. check the diagram.
- In a scale set you have to plan ahead what are the default, max, min instances and the architecture.
- Load balancers distribute the incoming traffic to healthy instances and ensures high availability.

## Creating a scale set:

- Basics Tab:

    name:tech501-maram-sparta-app-vmss
    - Availability zones: tick all 3 zones
    
    - Orchestration mode: Uniform
    
    - scaling mode: Autoscaling and change config max:3, min:2, default:2
    
    - from images choose your own image
    
    - username:adminuser
    
    - SSH: use existing key and choose tech501-maram-az-key

- Discs Tab: standard SSD

- Networking Tab:
      - choose maram-vnet; public subnet
      - azure load balancer
      - Create a new load balancer and keep the default settings
        - Load Balancer name: (tech501-maram-sparta-app-lb)

- Health Tab: 
      - enable application health monitoring
      - enable automatic repairs

- Advanced Tab: enable userdata and enter;
      - #!/bin/bash
        cd /app
        pm2 start app.js

- Tags: Owner: Maram
    - Create
    - Check the public IP address of the scale set

![alt text](<Screenshot 2025-01-30 170237.png>)


### Connecting to instances:
* To ssh to our instances choose a healthy instance and ssh; 
    - ssh -i ~/.ssh/tech501-maram-az-key -p 50000 adminuser@20.26.248.231
    - use the load balancer public IP
    - add -p 50000 for the first instance and to connect to the second add -p 50001 and so on.

* After stopping the vm scale set. you have to reimage one of the instances so the app would work, this allows for the app disc to copy everything again into a new disc with the userdata.

![alt text](<Screenshot 2025-01-30 170734-1.png>)

### Deleting a scale set: 
* Delete the scale set which will delete the instances by default.
* We should delete the load balncer seperately. 
* In a production setting we don't ssh to instances to make changes/updates. These are done from the scale set by changing the image or replacing it systematically.

