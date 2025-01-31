- [Create a new VM:](#create-a-new-vm)
  - [Dependencies](#dependencies)
- [install mongodb:](#install-mongodb)
- [on the app vm:](#on-the-app-vm)
- [Creating a reverse proxy:](#creating-a-reverse-proxy)
  - [on the app VM:](#on-the-app-vm-1)
- [Run the app in the background:](#run-the-app-in-the-background)
  - [using pm2:](#using-pm2)
  - [using \&:](#using-)
- [Create Database VM image:](#create-database-vm-image)

## Create a new VM:
### Dependencies
- Name: tech501-yourname-sparta-app-db-vm
- Ubuntu 22.04 LTS image
- Same size as usual
- NSG: allow SSH
- Public IP: yes
- VNet: 2-net one, subnet: private-subnet
- Login & run " sudo apt-get upgrade -y" , " sudo apt-get update -y".
  
## install mongodb:
- Mongo db version 7.0.6.
- Install gnupg and curl:
    - sudo apt-get install gnupg curl
- Import GPG key:
    - curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
   --dearmor

- Create the list file:
    - echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
- Reload the package database:
    - sudo apt-get update
- Install MongoDB Community Server.
  - sudo apt-get install -y mongodb-org=7.0.6 mongodb-org-database=7.0.6 mongodb-org-server=7.0.6 mongodb-mongosh mongodb-org-mongos=7.0.6 mongodb-org-tools=7.0.6
- Status of Mongo db:
  - sudo systemctl status mongod
- Start MongoDB:
  - sudo systemctl start mongod 
- Configure the bindip:
  - sudo nano /etc/mongod.conf
  - change the bindIP to: 0.0.0.0 (only for testing purposes which accepts connection from any IP address). 
  - ctrl + s followed by ctrl + x
- Restart the mongod db service:
  - sudo systemctl restart mongod
  - sudo systemctl status mongod
-------------------------------------------------------------------------------------------

- Enable the DB (add to the starter menu):
  - sudo systemctl enable mongod 
  - check; sudo systemctl is-enabled mongod 
- sudo systemctl start mongod

## on the app vm:

- environmanetal variable. use this command:
    - export DB_HOST=mongodb://<private IP>:27017/posts
    - export DB_HOST=mongodb://10.0.3.4:27017/posts
then printenv DB_HOST to check if its correct. 
- npm install
- node app.js
- the IP address: http://PublicIP:3000/posts
------------------------------------------------------------------------------------------

## Creating a reverse proxy:
### on the app VM:
1- Create a backup file of the configuration file
2- Edit Nginx Configuration:
    - sudo nano /etc/nginx/sites-available/default
3- change the location and add this:
    - On Location just remove the line and add this: proxy_pass http://localhost:3000;
    - this would allow access on port 80. it was only allowed on port 3000.
    - Ctrl + S; Ctrl + x
4- Test the Configuration:
    - sudo nginx -t
5- restart the nginx:
    - sudo systemctl restart nginx
6- Start the app:
    - npm start
7- Verify:
    - http://<your-public-ip>, http://172.187.176.32

------------------------------------------------------------------------------------------

## Run the app in the background:
### using pm2:

1- install pm2: 
    - sudo npm install -g pm2
2- Start the app with pm2:
    - pm2 start app.js --name "app"
3- Stop the app:
    - pm2 stop "app"
4- Restart the app:
    - pm2 restart "app"
5- Check running apps:
    - pm2 list


### using &:
1- Start the app in the background:
- node app.js &
  
2- Check if the app is running:
- ps aux 
  
3- Stop the app:
- kill (PID)
  
4- Restart the app:
- node app.js &

----------------------------------------

## Create Database VM image:
- SSH into the Database VM
- Run:
    - sudo waagent -deprovision+user
    - This will delete the adminuser (home directory)
- Stop the DB VM.
- Capture the Image
- Deploy a VM from Image:
- from Images: Find tech501-maram-db-ready-to-run-img.
- Click + Create VM.
- Name the new VM: tech501-maram-deploy-db-img-vm
