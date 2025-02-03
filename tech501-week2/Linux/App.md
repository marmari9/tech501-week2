- [Creating an APP VM](#creating-an-app-vm)
  - [1. Update and Upgrade Packages](#1-update-and-upgrade-packages)
  - [2. Install Nginx and Node.js](#2-install-nginx-and-nodejs)
  - [3.Verify Installation of node js and npm:](#3verify-installation-of-node-js-and-npm)
  - [4. Check status of Nginx:](#4-check-status-of-nginx)
  - [5. SSH Access to the Azure VM](#5-ssh-access-to-the-azure-vm)
  - [6. Copy the App Folder to the Azure VM Using two methods:](#6-copy-the-app-folder-to-the-azure-vm-using-two-methods)
- [when in app folder:](#when-in-app-folder)
- [Creating an image from app VM:](#creating-an-image-from-app-vm)
- [creating a vm with userdata config:](#creating-a-vm-with-userdata-config)



## Creating an APP VM 
- Name: tech501-maram-first-deploy-app-vm
- image: Ubuntu Server 22.04LTS- x64 Gen2
- Security Type: Standard not trusted 
- SSH: already existing key and choose tech501-maram-az-key
- Networking: Allow ssh on port 22, HTTP(80), and 3000
- SSH to the VM:
    - from connect
* In new VM always run these commands:

### 1. Update and Upgrade Packages
- sudo apt-get upgrade -y
- sudo apt-get update -y 

### 2. Install Nginx and Node.js

```bash
- sudo apt install nginx -y
```

- check if it's running : 
```bash
sudo systemctl status nginx or check public IP of vm
``` 
- For Ngnix to work we need to install node js and npm as it is a dependency.

```bash
- sudo DEBIAN_FRONTEND=noninteractive bash -c "curl -fsSL https://deb.nodesource.com/setup_20.x | bash -" && \
sudo DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs
```

### 3.Verify Installation of node js and npm:
- node -v
- npm -v

### 4. Check status of Nginx:
sudo systemctl status nginx

### 5. SSH Access to the Azure VM
 - ssh username@your_azure_vm_ip

### 6. Copy the App Folder to the Azure VM Using two methods:

1- from local machine:
- cd onedrive/Documents/github
- scp -r /path/to/local/app_folder username@your_azure_vm_ip:/path/to/remote/destination
    - scp -i ~/.ssh/tech501-maram-az-key -r app adminuser@20.90.209.175:/home/adminuser/
    - rsync

2- push the code from local repo and clone it to the app vm; 
- git clone https://github.com/marmari/tech501-sparta-app.git
- cd tech501-sparta-app


* Azure allows more default within same vnet(resources within same network are able to communicate). while aws is restricted by default(you have to set a seperate rule for each resource).


## when in app folder: 
- cd app
- npm install
- to run the app two ways: 
    1- node app.js
    2- npm start 
- http://public IP:3000 (app should appear). ps; allow port 3000 in NSG on app vm.




## Creating an image from app VM:
- move the app from adminuser home directory to the root directory:
```bash
sudo mv /home/adminuser/app /
```

- this will delete the home directory: 
```bash  
sudo waagent -deprovision+user 
```
- No need to have the image in the gallery.
- on azure stop the app VM.
- Capture the image
- name the image: tech501-maram-ready-to-run-app-img
- after creating image create a VM from the image 
- ssh to the vm and cd app


<br>

## creating a vm with userdata config:
- Use the vm image.
- License: select other
- in advanced:
- userdata:

```bash
#!/bin/bash
cd /app
export DB_HOST=mongodb://10.0.3.4:27017/posts;; always check for the private IP of the database if it needs to be changed.
pm2 start app.js
```
- create vm and check public IP
- use /posts 


