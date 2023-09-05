# Steps to deploy a Node.js app to aws using PM2, NGINX as a reverse proxy and an SSL from LetsEncrypt
``1. Create Free AWS Account``
<br>Create free AWS Account at https://aws.amazon.com/

``2. Create and Lauch an EC2 instance and SSH into machine``
<br>I would be creating a t2.micro ubuntu machine for this demo.

``3. Install Node and NPM``
```https://deb.nodesource.com/
<br>sudo apt update && sudo apt install -y ca-certificates curl gnupg
<br>curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
<br>NODE_MAJOR=20
<br>echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
<br>sudo apt-get update && sudo apt-get install nodejs -y
node --version```

``4. Clone your project from Github``
<br>git clone https://github.com/piyushgargdev-01/short-url-nodejs

``5. Install dependencies and test app``

<br>sudo npm i pm2 -g
<br>pm2 start index

# Other pm2 commands
```pm2 show app
pm2 status
pm2 restart app
pm2 stop app
pm2 logs (Show log stream)
pm2 flush (Clear logs)```
# To make sure app starts when reboot
pm2 startup ubuntu
6. Setup Firewall
sudo ufw enable
sudo ufw status
sudo ufw allow ssh (Port 22)
sudo ufw allow http (Port 80)
sudo ufw allow https (Port 443)
7. Install NGINX and configure
sudo apt install nginx

sudo nano /etc/nginx/sites-available/default
Add the following to the location part of the server block

    server_name yourdomain.com www.yourdomain.com;

    location / {
        proxy_pass http://localhost:8001; #whatever port your app runs on
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
# Check NGINX config
sudo nginx -t

# Restart NGINX
sudo nginx -s reload
8. Add SSL with LetsEncrypt
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python3-certbot-nginx
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com

# Only valid for 90 days, test the renewal process with
certbot renew --dry-run


# INSTALL NODE.JS:


# INSTALL MONGODB:

https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/#std-label-install-mdb-community-ubuntu

cd short-url-nodejs/

<br>curl -fsSL https://pgp.mongodb.com/server-7.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
   --dearmor

<br>echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list


<br>sudo apt update

sudo apt install -y mongodb-org

sudo systemctl start mongod

sudo systemctl status mongod

mongosh

test> show dbs

<br>admin       40.00 KiB
<br>config      72.00 KiB
<br>local       72.00 KiB
<br>short-url  136.00 KiB


test> use short-url
switched to db short-url

short-url> show collections```
