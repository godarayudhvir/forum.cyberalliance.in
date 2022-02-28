### Installing NginxProxyManager(Nproxy)
#### Routing of Domain Names

What a great topic! to discuss since I am a Networking Engineering,

There are so many ways you can route traffic from a domain, 
but in general, I usually will route a domain to a server being hosted on 
Linode/GalaxyGate using an 
"A" record in DNS on my Domains.google.com, 
or I will route a domain to my home server 
(still using an A record, but in a different way).

A bit of additional routing knowledge is needed 
for hosting a server from home, and there are multiple solutions available 
for that as well, but my preferred solution is NGinX Proxy Manager.

Let's just pretend we have a domain called 
cyberalliance.com.  We don't, but we will pretend. ( we have .in 😭 )

What I like to do is create a subdomain on my domain related to a server or web-application I'm running. 
Let's say we are running a chat server like RocketChat, 
and we want to make it easier for our users to find our chat server.  
We'll choose to call it chat.cyberalliance.com.

similarly for a meeting platform using jitsi meet.cyberalliance.in
for a self-hosted cloud storage like nextcloud cloud.cyberalliance.in
for a media-server like plex we would use media.cyberalliance.in and so on...

So, from our Domain registrar 
(Domains.google.com, Porkbun, Hostinger, GoDaddy, Ghandi.net, etc), 
we'll edit the DNS for cyberalliance.com, and add a new 
"A" record called "chat".  
And we'll point that name to the public IP address of our server at linode/galaxygate

Now if you goto chat.cyberalliance.in... it will take you to thatip but it will show chat.cyberalliance.in in addressbar

Once you have that working, you're essentially done.  
There are still steps to make sure the site is secured with SSL, but the basics are complete.

#### Actually Installing Nproxy 😃

goto dir root/ and make a new dir nproxy
inside that make a folder nproxy

>cd /
cd root/
mkdir nproxy
cd nproxy/

Now make a configuration file and a json file
nano config.json | copy content from below and change accordingly
nano docker-compose.yml | copy content from below and change accordingly
Save and exit out of the file once done.

Inside the config.json file, you'll put the following:

```
{
  "database": {
    "engine": "mysql",
    "host": "db",
    "name": "nproxy",
    "user": "<your desired username>",
    "password": "<a strong password>",
    "port": 3306
  }
}
```

And inside the docker-compose.yml file you'll put:

```
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - ./config.json:/app/config/production.json
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
  db:
    image: 'jc21/mariadb-aria:latest'
    environment:
      MYSQL_ROOT_PASSWORD: '<a strong passowrd>'
      MYSQL_DATABASE: 'nproxy'
      MYSQL_USER: '<username from config.json>'
      MYSQL_PASSWORD: '<strong password from config.json>'
    volumes:
      - ./data/mysql:/var/lib/mysql
```


Now let's pull Docker Image
>docker-compose up -d

![](https://i.imgur.com/Y4boQy4.gif)

Now let's see if the docker is running
>docker ps

![](https://i.imgur.com/j9FM36d.png)
as seen here, nginx proxy manager is up and running on serverip with port 81
now go to a browser and put in http://serverip:81
it will take you to web admin panel of nproxy

if selfhosting locally at home, you may wanna check local ip so
>ip addr

![](https://i.imgur.com/nLE63BB.png)

So in this case local nginx proxy manager web admin panel would be at
http://172.17.0.1:81

![](https://i.imgur.com/MnOHLJF.png)

Default credentials are:

username: admin@example.com
passwrod: changeme

Make sure to update the email and password, from the default values, then log out, and back in usign the new values you entered.

Now, you're ready to start proxying traffic.

#### Configuring Nginx Proxy Manager
![](https://i.imgur.com/GMSH6a2.png)
Change following as seen fit according to you.
Then Choose a Strong Password
![](https://i.imgur.com/7VpeeIl.png)

#### Point Domain to server
Goto : https://domains.google.com/registrar/yourdomain/dns
Click on Manage Custom Records
and set your domain like below
![](https://i.imgur.com/qWiW3XP.png)
Hostname : * Type : A TTL : 3600 Data : Serverip
#### Create a new Proxy Host
![](https://i.imgur.com/E7QLvyr.png)
#### Point ngingxproxy to domain
![](https://i.imgur.com/qkY7aYL.png)
#### Enable SSL
![](https://i.imgur.com/uBrAwVD.png)

After a while your site should be live at that subdomain
