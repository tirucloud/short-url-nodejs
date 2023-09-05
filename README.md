# INSTALL NODE.JS:

https://deb.nodesource.com/


sudo apt update && sudo apt install -y ca-certificates curl gnupg

<br>curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg

<br>NODE_MAJOR=20

<br>echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list

<br>sudo apt-get update && sudo apt-get install nodejs -y


node --version

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

short-url> show collections
