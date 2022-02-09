## Uptime Kuma

### A fancy self-hosted monitoring tool

## ⭐ Features

- Monitoring uptime for HTTP(s) / TCP / HTTP(s) Keyword / Ping / DNS Record / Push / Steam Game Server.
- Fancy, Reactive, Fast UI/UX.
- Notifications via Telegram, Discord, Gotify, Slack, Pushover, Email (SMTP), and 70+ notification services, click here for the full list.
- 20 second intervals.
- Multi Languages
- Simple Status Page
- Ping Chart
- Certificate Info

## 🔧 How to Install 🐳 Docker

Run `docker volume create uptime-kuma`
and this `docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1`

⚠️ Please use a local volume only. Other types such as NFS are not supported.

Browse to http://serverip:3001 after starting.

Create the Admin account (strong password)
![](https://i.imgur.com/XvuVJg3.png)

Adding a Site for Monitor
![](https://i.imgur.com/akY62B6.gif)

Setting up Discord Notification
![](https://i.imgur.com/kQXWg5g.gif)

**How to Update**

```
docker pull louislam/uptime-kuma:1
docker stop uptime-kuma
docker rm uptime-kuma
docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
```

Please read: https://github.com/louislam/uptime-kuma/wiki/%F0%9F%86%99-How-to-Update


## Securing Uptime Kuma

### Setting up a Reverse Proxy and point to a domain

1. Install and configure Nginx proxy manager as explained "[here](https://forum.cyberalliance.in/public/d/17-install-nginx-proxy-manager)"
2. Login to Nginx proxy manager
3. Go to Hosts > Proxy Hosts
4. Click on Add proxy Host

Fill it as seen below

1. Replace "service.yourdomain.tld" with your prefered subdomain followed by your domain url
2. Type your servers ip in forward hostname box
3. Forward the port, jellyfin comes with 8096 by default
4. Choose Cache Assets, Block Common Exploits
5. Turn on Websockets support	

![](https://i.imgur.com/MIN4sAY.png)

Now go to SSL Tab

1. Under SSL certificate, choose "Request a new SSL Cert" from the dropdown menu
2. Enable Force SSL
3. Fill in your email address
4. Click on I agree to Tos
5. Click save

![Setting up SSL](https://i.imgur.com/kigFJzL.png)

After a while, you site should be live on service.yourdomain.tld no need to type
serverip:3001 from now on and plus it has **SSL** now.

![SSL active](https://i.imgur.com/eCuYKlN.png)

References :
https://en.wikipedia.org/wiki/List_of_HTTP_status_codes

## That's all Folks!

![](https://i.imgur.com/8g3bgEE.png)
![](https://i.imgur.com/cmkxcCX.png)

Learn more about Uptime Kuma at  https://github.com/louislam/uptime-kuma
