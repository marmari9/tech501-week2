## 1. Update and Upgrade Packages
- sudo apt-get upgrade -y
- sudo apt-get update -y 

## 2. Install Nginx and Node.js
- sudo apt install nginx -y
- check if it's running : sudo systemctl status nginx or check public IP of vm 
- sudo DEBIAN_FRONTEND=noninteractive bash -c "curl -fsSL https://deb.nodesource.com/setup_20.x | bash -" && \
sudo DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs

## 3.Verify Installation
- node -v
- npm -v

## 4 SSH Access to the Azure VM
 - ssh username@your_azure_vm_ip

## 5 Copy the App Folder to the Azure VM Using scp
- scp -r /path/to/local/app_folder username@your_azure_vm_ip:/path/to/remote/destination

- git clone https://github.com/marmari/tech501-sparta-app.git
- cd tech501-sparta-app


### Azure allows more default within same vnet(resources within same network are able to communicate). while aws is restricted by default(you have to set a seperate rule for each resource).


## when in app folder: 
- npm install
- to run the app two ways: 
    1- node app.js
    2- npm start 
- http://public IP:3000 (app should appear). ps; allow port 3000 in NSG on app vm.
- 
