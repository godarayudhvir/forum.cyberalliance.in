## Vaultwarden

### The Most Trusted Open Source Password Manager for Business

Unofficial Bitwarden compatible server written in Rust, formerly known as bitwarden_rs

Alternative implementation of the Bitwarden server API written in Rust and compatible with [upstream Bitwarden clients](https://bitwarden.com/download/)*, perfect for self-hosted deployment where running the official resource-heavy service might not be ideal..

Github: https://github.com/dani-garcia/vaultwarden/

## ⭐ Features

Basically full implementation of Bitwarden API is provided including:

-     Organizations support
-     Attachments
-     Vault API support
-     Serving the static files for Vault interface
-     Website icons API
-     Authenticator and U2F support
-     YubiKey and Duo support

## Check out Demo 😋

Try out (With limited functionalities)
https://bitwarden.com/

## Installation

- Browse to the root directory
- Create a folder "**vaultwarden**"
- Browse into the folder
- Create a docker-compose file using `nano docker-compose.yml`
- Paste the content below
- Save the docker file
- Exit out the docker file
- Run `docker-compose up -d`

![Vaultwarden-installation.preview](https://i.imgur.com/rj8FLuH.png)

```
version: '3'
services:
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden
    restart: always
    environment:
      - WEBSOCKET_ENABLED=true  # Enable WebSocket notifications.
    volumes:
      - ./vw-data:/data
    ports:
      - 9884:80
      - 9885:443
```

Make sure docker container is running
![vaultwarden-docker.ps](https://i.imgur.com/Zzs22wz.png)

### Before running Vaultwarden

In order for Vaultwarden to work, first you need to enable HTTPS on the vaultwarden service

#### Setting up a Reverse Proxy and point to a domain

1.  Install and configure Nginx proxy manager as explained "[here](https://forum.cyberalliance.in/public/d/17-install-nginx-proxy-manager)"
2.  Login to Nginx proxy manager
3.  Go to Hosts > Proxy Hosts
4.  Click on Add proxy Host

Fill it as seen below

1.  Replace "service.yourdomain.tld" with your prefered subdomain followed by your domain url
2.  Type your servers ip in forward hostname box
3.  Forward the port,  9884 (as in the docker config)
4.  Choose Cache Assets, Block Common Exploits and Websockets support

![](https://i.imgur.com/MIN4sAY.png)

Now go to SSL Tab

1.  Under SSL certificate, choose "Request a new SSL Cert" from the dropdown menu
2.  Enable Force SSL
3.  Fill in your email address
4.  Click on I agree to T.O.S
5.  Click save

![Setting up SSL](https://i.imgur.com/kigFJzL.png)

After a while, you site should be live on filebrowser.yourdomain.tld no need to type
serverip:9884 from now on and plus it has **SSL** now.

![Bitwarden SSL active](https://i.imgur.com/r0IwQ0S.png.png)

### Setting up Bitwarden
![vaultwarden-welcome.scr](https://i.imgur.com/L3Ol2vx.png)
Now the installation has been finished,
so let's proceed witht the setup.
1. Click on "Create Account"
2. Create a account like you normally would
![vault-warden.signup](https://i.imgur.com/cyBRE5Z.png)
3. Login and you shall then see...
![vaultwarde-welcome.scr](https://i.imgur.com/o4ucyFF.png)
4. Creating first Login credential
![vaultwarden-add.scr](https://i.imgur.com/g6IktVI.gif)
5. Add the browser extension
![vaultwarden-ext.inst](https://i.imgur.com/LaHt5TZ.gif)
6. Login to the extension
![vaultwarden-ext.login](https://i.imgur.com/TOr6UG2.gif)
7. Using the extension
![vaultwarden-ext.use](https://i.imgur.com/Iof7Y6v.gif)

### Using the Android/iOS Client

## That's all Folks!
![Bitwarden preview](https://i.imgur.com/VDKzdbQ.png.png)

**Using Bitwarden complete guide : Coming soon**
