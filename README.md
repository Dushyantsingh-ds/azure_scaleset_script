# Azure PowerShell Script
We will create a VM using PowerShell then Configure the server
### Create Virtual Machine Using PowerShell
`set-variable -name "USERNAME" -value "Your_UserName" 

Set-Variable -name "PASSWORD" -value "Password"  

New-AzResourceGroup -Name Your_ResourceGroup_Name -Location EastUS2
az vm create --name VM_Name --resource-group Your_ResourceGroup_Name --image 'Win2016Datacenter' --size Standard_B1s --location EastUS2 --admin-username $USERNAME --admin-password $PASSWORD --zone 2`
### WebServerConfiguration
`packages:
  /- nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: User_Name:User_Name
  - path: /home/User_Name/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Welcome to My World !! Let's learn together!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/hauser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js `
