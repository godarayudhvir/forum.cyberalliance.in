## Qbittorent
### A Open source Light weight Bittorent client

Today we’ll configure a containerized version of Qbittorent and have you up and going in just a few minutes. 

We’ll also add a **custom theme** to it 😍 


## Preparation

1. Browse to the root directory
2. Create a folder "**qbittorent**"
3. Browse into the folder
4. Create a docker compose file with nano docker-compose.yml
5. Paste the content provided below
6. Save the docker file
7. Run `docker-compose up -d`

**Docker Compose File**

```
---
version: "2.1"
services:
  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent
    container_name: qbittorrent
    environment:
      - PUID=0 #for root uid and gid are 0
      - PGID=0
      - TZ=Asia/Calcutta
      - WEBUI_PORT=9885 #our Web Gui will be avaialable at this port
    volumes:
      - /root/qbittorent/appdata/config:/config
      - /root/downloads:/downloads # you will find your downloads in this location
    ports:
      - 6881:6881
      - 6881:6881/udp
      - 9885:9885 #If you change this, do change aboe WEBUI_PORT also
    restart: unless-stopped #Docker will restart on its own everytime it crashes
```

### Check if Docker is up and running

`Run Docker ps` 

![](https://i.imgur.com/nXwwj3g.png)



## Spinning it up

***The webui is at <your-ip>:9885*** 
![](https://i.imgur.com/jsHaKa0.png)

**Default Login credentials**

Username : admin
Password : adminadmin

![](https://i.imgur.com/RpVMJol.png)

## Securing Qbittorent

1. Login Qbittorent
![](https://i.imgur.com/Cvoawye.png)
2. Go to tools
![](https://i.imgur.com/wao70a4.png)
3. Navigate to WebUI tab
![](https://i.imgur.com/Iv9qdM4.png)
4. Here you change login credentials
![](https://i.imgur.com/Bd8Ovoo.png)

## Setting up a Reverse Proxy and point to a domain

1. Install and configure Nginx proxy manager as explained "[here](https://forum.cyberalliance.in/public/d/17-install-nginx-proxy-manager)"
2. Login to Nginx proxy manager
3. Go to Hosts > Proxy Hosts
4. Click on Add proxy Host

Fill it as seen below

1. Replace "qbit.yourdomain.tld" with your prefered subdomain followed by your domain url
2. Type your servers ip in forward hostname box
3. Forward the port, in our config we had it set to 9885
4. Choose Cache Assets, Block Common Exploits

![Setting up Proxy](https://i.imgur.com/44BUNVo.png)

Now go to SSL Tab

1. Under SSL certificate, choose "Request a new SSL Cert" from the dropdown menu
2. Enable Force SSL
3. Fill in your email address
4. Click on I agree to Tos
5. Click save

![Setting up SSL](https://i.imgur.com/kigFJzL.png)

After a while, you site should be live on filebrowser.yourdomain.tld no need to type
serverip:9885	 from now on and plus it has **SSL** now.

![SSL active](https://i.imgur.com/OW0FwSl.png)

## Applying a custom them 💘

1. Go [here](https://github.com/WDaan/VueTorrent)
![](https://i.imgur.com/ixEMYwN.png)
2. Go to releases
![](https://i.imgur.com/jW4ELXv.png)
3. Download the Vuetorrent.zip from the latest release
4. Extract Zip
5. Upload the Vuetorrent folder which was just extracted
to the location below

`root>qbit>appdata>config>theme`
*folder theme doesn't exist there, you will have to make it

So, paste vuetorrent folder inside that.
![](https://i.imgur.com/7zPBzZD.png)

7. Under the same Web UI section scroll down to
![](https://i.imgur.com/IXhw3Dc.png)
and type in the location to the theme as seen above

8. Scroll down and Click the **Save** button and reload site
Ahhhhh Voila!!!

![](https://i.imgur.com/BOLRDj7.png)
On the bottom left click the sun icon to switch to dark theme
![](https://i.imgur.com/paE0Y3k.png)
