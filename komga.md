## Komga
### A cool selfhosted library for Manga, Books, Comics, Magazines on the go

Komga is a media server for your comics, mangas, BDs and magazines.

### How it works:

1. Install and run Komga on a computer or NAS.
2. Add libraries by type of content and let Komga do the rest.
3. Use the web interface or any compatible client.
4. Enjoy your books!

### What media and devices work?
Komga supports these media file types:

1. Comic book archives: CBZ and CBR (except RAR5 and solid archives)
2. Books in EPUB format
3. PDF files

### Feature

1. Browse libraries, series and books via a responsive web UI that works on desktop, tablets and phones
2. Organize your library with collections and read lists
3. Edit metadata for your series and books
4. Import embedded metadata automatically
5. Webreader with multiple reading modes
5. Manage multiple users, with per-library access control
6. Offers a REST API, many community tools and scripts can interact with Komga
7. Download book files, whole series, or read lists
8. Duplicate files detection
9. Duplicate pages detection and removal
10. Import books from outside your libraries directly into your series folder
11. Import ComicRack cbl read lists

### Preparation

- Browse to the root directory
- Create a folder "**Komga**"
- Browse into the folder
- Create a docker compose file with nano docker-compose.yml
- Paste the content provided below
- Save the docker file
	
```
---
version: '3.3'
services:
  komga:
    image: gotson/komga
    container_name: komga
    volumes:
      - type: bind
        source: /root/komga/config #create this folder before docker compose
        target: /config
      - type: bind
        source: /root/komga/data #create this folder before docker compose
        target: /data
      - type: bind
        source: /etc/timezone #create this folder before docker compose
        target: /etc/timezone
        read_only: true
    ports:
      - 9886:8080
    user: "0:0" #uid and gid are 0 for root
```

This should be the final layout of the folder

![](https://i.imgur.com/Jrry0Fr.png)

Run `Docker-compose up -d` (You should see no errors)
Run `Docker ps` (You should see port assigned)

### Run the WebGUI
The webui is at <your-ip>:9886 and then,
You will be asked to create a user account 
Choose an email and password, then click on Create User Account.
![](https://i.imgur.com/NzPkGkW.png)

### Adding Books/comics
Navigate into root/komga/data
Create folders Manga, Books, Magazines etc
and upload files into them accordingly.
![](https://i.imgur.com/4lSlCBv.png)

Click on Add library
![](https://i.imgur.com/GeKRFeA.png)
Add the libraries and you should have it all up and running 😉
![](https://i.imgur.com/z9PqEpS.gif)

### End goal!
![](https://i.imgur.com/cir4JCx.png)

> **_Disclaimer_**
> If you have a library with a root path of /books/mangas, 
> you can't create a library with a root path of /books, 
> because the two root paths would overlap. 
> You can however create a library with a root path of /books/comics

## Setting up a Reverse Proxy and point to a domain

1. Install and configure Nginx proxy manager as explained "[here](https://forum.cyberalliance.in/public/d/17-install-nginx-proxy-manager)"
2. Login to Nginx proxy manager
3. Go to Hosts > Proxy Hosts
4. Click on Add proxy Host

Fill it as seen below

1. Replace "service.yourdomain.tld" with your prefered subdomain followed by your domain url
2. Type your servers ip in forward hostname box
3. Forward the port, in our config we had it set to 9886
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
serverip:9886 from now on and plus it has **SSL** now.

![SSL active](https://i.imgur.com/4UEVFxZ.png)

Learn more about Komga at : https://komga.org/guides/
