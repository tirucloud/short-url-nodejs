# Nodejs App
### Install node.js from https://deb.nodesource.com/
```bash
sudo systemctl start mongod
```
2. check node version --> node -v
3. check node package manager version --> npm -v
4. Install mongodb from --> https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/
5. sudo systemctl start mongod
6. sudo systemctl enable mongod
7. mongosh
8. test> show dbs
9. test> exit
10. npm list
11. Clone your project from Github --> git clone https://github.com/tirucloud/short-url-nodejs.git
12. go to short-url-nodejs directory
13. cd short-url-nodejs
14. npm install
15. sudo npm i pm2 -g\
    npm list -g\
    pm2 list
16. pm2 start index.js
17. pm2 startup
sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu<br>
18. copy and execute the output and make auto start of an node.js app even on reboot<br>
pm2 save\
mongosh\
test> show dbs<br>
test> use short-url<br>
short-url> show collections<br>
exit<br>
sudo apt install nginx -y<br>
sudo systemctl enable nginx<br>

sudo vi /etc/nginx/conf.d/site.conf
```
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

Check NGINX config

sudo nginx -t

Restart NGINX

sudo nginx -s reload

Add SSL with LetsEncrypt
sudo add-apt-repository ppa:certbot/certbot 

sudo apt update 

sudo apt install python3-certbot-nginx 

sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com

Only valid for 90 days, test the renewal process with

certbot renew --dry-run

sudo systemctl status certbot.timer

Wriet a cron job to perform auto renewal for every 30 days

sudo vi /etc/cron.d/certbot

# /etc/cron.d/certbot: crontab entries for the certbot package
#
# Upstream recommends attempting renewal twice a day
#
# Eventually, this will be an opportunity to validate certificates
# haven't been revoked, etc.  Renewal will only occur if expiration
# is within 30 days.
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

0 */12 * * * root test -x /usr/bin/certbot -a \! -d /run/systemd/system && perl -e 'sleep int(rand(3600))' && certbot -q renew

crontab -l
crontab -t


mongosh

test> show dbs

admin       40.00 KiB
config      72.00 KiB
local       72.00 KiB
short-url  136.00 KiB


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

Signup Page: http://yourdomain.com:8001/signup

http://yourdomain.com:8001/login

# mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.1.1

# Download mongodb compass client tool: https://www.mongodb.com/try/download/compass

Go to Linux terminal, edit mongo conf file to access mongodb from anaywhere
sudo vi /etc/mongod.conf

Goto network section 

Replace 127.0.0.1 with 0.0.0.0

