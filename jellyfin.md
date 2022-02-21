## Jellyfin
### A Free open-source Media server

Jellyfin is the volunteer-built media solution that puts you in control of your media. Stream to any device from your own server, with no strings attached. Your media, your server, your way.

### What is Jellyfin?
Jellyfin enables you to collect, manage, and stream your media. Run the Jellyfin server on your system and gain access to the leading free-software entertainment system, bells and whistles included.
![](https://i.imgur.com/ZktevwI.png)

Jellyfin lets you watch your media from a web browser on your computer, apps on your Roku, Android, iOS (including AirPlay), Android TV, or Fire TV device, or via your Chromecast or existing Kodi installation. See all available [clients](https://jellyfin.org/clients/).


## Preparation
- Browse to the root directory
- Create a folder "**jellyfin**"
- Browse into the folder
- Pull Docker image : `docker pull jellyfin/jellyfin`
- Create these folders
config, cache, media and media2
- Create a docker compose file with nano
- Paste the content provided below
- Save the docker file

```
version: "3.5"
services:
  jellyfin:
    image: jellyfin/jellyfin
    container_name: jellyfin
    user: 0:0 #uid and gid are 0 for root
    network_mode: "host"
    volumes:
      - /root/jellyfin/config:/config
      - /root/jellyfin/cache:/cache
      - /root/jellyfin/media:/media
      - /root/jellyfin/media2:/media2:ro
      - /root/jellyfin/tv:/tv
      - /root/jellyfin/movies:/movies
      - /root/jellyfin/anime:/anime
      - /root/jellyfin/music:/music
        
      
    restart: "unless-stopped" #self explanatory
```


Run `docker-compose up -d`

Once done run Docker ps
Make sure jellyfin is running.

Now go to serverip:8096
you will see this setup wizard

Choose the language you prefer
![](https://i.imgur.com/bFZXBNc.png)
Choose a username and a strong password
![](https://i.imgur.com/PA6WSt2.png)
Now add a library like this:
![](https://i.imgur.com/IfVE8Lb.gif)
****We can configure all these settings later too***

Now sign in to your account
![](https://i.imgur.com/cx3C7um.png)

### Where to store Movies/shows etc. ?
/root/jellyfin/media
/root/jellyfin/movies
/root/jellyfin/tv
/root/jellyfin/anime
/root/jellyfin/music
etc...

### Explore Jellyfin
![](https://i.imgur.com/9TIHNHd.png)
Main keypoints

Dashboard : shows active users
General : Server name, language, paths to cache and metadata, branding : login disclaimer ; custom css etc
Users : Manage users : add , remove, configure
Libraries : Add a library, Scan Libraries and change library settings such as metadata providers etc
Playback : Transcoding settings

### Securing Jellyfin
![](https://i.imgur.com/sLUSyaU.gif)

## Setting up a Reverse Proxy and point to a domain

1. Install and configure Nginx proxy manager as explained "[here](https://forum.cyberalliance.in/public/d/17-install-nginx-proxy-manager)"
2. Login to Nginx proxy manager
3. Go to Hosts > Proxy Hosts
4. Click on Add proxy Host

Fill it as seen below

1. Replace "service.yourdomain.tld" with your prefered subdomain followed by your domain url
2. Type your servers ip in forward hostname box
3. Forward the port, jellyfin comes with 8096 by default
4. Choose Cache Assets, Block Common Exploits

![Setting up Proxy](https://i.imgur.com/nyeI2hq.png)

Now go to SSL Tab

1. Under SSL certificate, choose "Request a new SSL Cert" from the dropdown menu
2. Enable Force SSL
3. Fill in your email address
4. Click on I agree to Tos
5. Click save

![Setting up SSL](https://i.imgur.com/kigFJzL.png)

After a while, you site should be live on filebrowser.yourdomain.tld no need to type
serverip:8096 from now on and plus it has **SSL** now.

![SSL active](https://i.imgur.com/AdMt23g.png)

Learn more about Jellyfin at : https://jellyfin.org/docs/general/quick-start.html
