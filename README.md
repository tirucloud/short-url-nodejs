#### Install node.js from https://deb.nodesource.com
#### check node version
```bash node -v
```
#### check node package manager version
```bash
npm -v 
```
#### Install mongodb from https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/
```bash 
sudo systemctl start mongod
```
```bash
sudo systemctl enable mongod 
```
```bash
mongosh 
```
```bash
test> show dbs 
```
```bash
test> exit 
```
```bash
npm list 
```
#### Clone your project from Github --> git clone https://github.com/tirucloud/short-url-nodejs.git
#### go to short-url-nodejs directory
```bash
cd short-url-nodejs
npm install
sudo npm i pm2 -g
npm list -g
pm2 list
pm2 start index.js
pm2 startup
```
```bash
sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu
```
#### copy and execute the output and make auto start of an node.js app even on reboot
```bash
pm2 save
```
```bash
mongosh
test> show dbs
test> use short-url
short-url> show collections
exit
sudo apt install nginx -y
sudo systemctl enable nginx
```
```bash
sudo vi /etc/nginx/sites-available/default
````
```bash
server {
       listen 80;
       listen [::]:80;

       server_name 3.110.28.55;

location / {
    proxy_pass http://localhost:8001;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}

}
```
#### Check NGINX config

```bash
sudo nginx -t
```
#### Restart NGINX
```bash
sudo nginx -s reload
````
#### Add SSL with LetsEncrypt
```bash
sudo add-apt-repository ppa:certbot/certbot 
```
```bash
sudo apt update 
sudo apt install python3-certbot-nginx 
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```
#### Only valid for 90 days, test the renewal process with
```bash
certbot renew --dry-run
```
```bash
sudo systemctl status certbot.timer
```
#### Wriet a cron job to perform auto renewal for every 30 days
```bash
sudo vi /etc/cron.d/certbot
```
```bash
# /etc/cron.d/certbot: crontab entries for the certbot package
#
# Upstream recommends attempting renewal twice a day
#
# entually, this will be an opportunity to validate certificates
# haven't been revoked, etc.  Renewal will only occur if expiration
# is within 30 days.
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

0 */12 * * * root test -x /usr/bin/certbot -a \! -d /run/systemd/system && perl -e 'sleep int(rand(3600))' && certbot -q renew
```
```bash
crontab -l
crontab -t
```
```bash
mongosh
```
```bash
test> show dbs
```
```bash
admin       40.00 KiB
config      72.00 KiB
local       72.00 KiB
short-url  136.00 KiB
```
```bash
test> use short-url
switched to db short-url
short-url> show collections
short-url> show collections
urls
users
short-url> db.users.find()
[
  {
	_id: ObjectId('659fe20f73142bd743583f1f'),
	name: 'abc',
	email: 'abc@xyz.com',
	password: '123456',
	createdAt: ISODate('2024-01-11T12:41:51.429Z'),
	updatedAt: ISODate('2024-01-11T12:41:51.429Z'),
	__v: 0
  }
]
short-url> db.urls.find()
[
  {
	.........
  }
]
```
#### Signup Page: http://yourdomain.com:8001/signup

#### http://yourdomain.com:8001/login

#### mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.1.1

#### Download mongodb compass client tool: https://www.mongodb.com/try/download/compass

#### Go to Linux terminal, edit mongo conf file to access mongodb from anaywhere
```bash
sudo vi /etc/mongod.conf
```
#### Goto network section 
#### Replace 127.0.0.1 with 0.0.0.0

