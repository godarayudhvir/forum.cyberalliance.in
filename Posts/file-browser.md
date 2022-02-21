## File Browser
### A Small but Mighty Web File Browser

Meet **File Browser**, an open source, self-hosted alternative to services like Dropbox and other web based file browsers. Today we’ll configure a containerized version of File Browser and have you up and going in just a few minutes. 

We’ll also add a **custom theme** to it 😍 

And lastly we will walk you through **sharing files and folders** 

## Preparation

- Browse to the root directory
- Create a folder "**filebrowser**"
- Browse into the folder
- Create a docker compose file with nano docker-compose.yml
- Paste the content provided below
- Save the docker file
- Create a file "**filebrowser.db**" with "touch" not nano

**Docker Compose File**

```
version: '3'
services:
  file-browser:
    image: filebrowser/filebrowser
    container_name: file-browser
	#uid and gid is 0 for root
    user: 0:0 #uid and gid
    ports:
      - 8081:80 #Web Gui Will be available on port 8081
    volumes:
      - /root:/srv # If you want to serve out entire storage on Web-Gui do it as /:/srv
      - /root/filebrowser/filebrowser.db:/database.db
    restart: unless-stopped #Docker will restart on its own everytime it crashes
    security_opt:
      - no-new-privileges:true
```


## Spinning it up
- Goto **youserverip:8081**
- Default login credentials : 	Admin / Admin for user and password respectively.

You should now be in the Graphical Web user interface of File browser

![File browser web gui](https://i.imgur.com/PkMkK8p.png)

## Securing File browser

1. Login to File browser
2. Go to settings
3. Change Password
4. Go to user Management
5. Click on Pencil icon next to Admin
6. Edit "admin" to a "preferred username

## Setting up a Reverse Proxy and point to a domain

1. Install and configure Nginx proxy manager as explained "[here](https://forum.cyberalliance.in/public/d/17-install-nginx-proxy-manager)"
2. Login to Nginx proxy manager
3. Go to Hosts > Proxy Hosts
4. Click on Add proxy Host

Fill it as seen below

1. Replace "filebrowser.yourdomain.tld" with your prefered subdomain followed by your domain url
2. Type your servers ip in forward hostname box
3. Forward the port, in our config we had it set to 8081
4. Choose Cache Assets, Block Common Exploits

![Setting up Proxy](https://i.imgur.com/6yMYmRO.png)

Now go to SSL Tab

1. Under SSL certificate, choose "Request a new SSL Cert" from the dropdown menu
2. Enable Force SSL
3. Fill in your email address
4. Click on I agree to Tos
5. Click save

![Setting up SSL](https://i.imgur.com/kigFJzL.png)

After a while, you site should be live on filebrowser.yourdomain.tld no need to type
serverip:8081 from now on and plus it has **SSL** now.

![SSL active](https://i.imgur.com/6OA1Fu8.png)

## Applying a custom them 💘

1. Go [here](https://docs.theme-park.dev/themes/filebrowser/#screenshots)
2. Choose one of the many available themes (Steps for all of em will be same)

**I'll be choosing this one**, Looks pretty good to me 😉
![Dark Theme](https://docs.theme-park.dev/site_assets/filebrowser/dark.png)

```
proxy_set_header Accept-Encoding "";
sub_filter
'</head>'
'<link rel="stylesheet" type="text/css" href="https://theme-park.dev/css/base/filebrowser/<THEME>.css">
</head>';
sub_filter_once on;
```

#### Copy above css code ^

1. Go to Nginx Proxy Manager
2. Under proxy hosts, edit your proxy for File browser 

![edit](https://i.imgur.com/GTiu3oy.png)

3. Now go to custom location tab and fill as below

![custom css](https://i.imgur.com/Ub1iDLs.png)

1. Click on add location
2. In location type `/`
3. Click the gear icon
4. Fill the IP and port same as your proxy
5. Inside the text box below fill the code provided earlier
6. Replace <THEME> with name of the theme you want
7. For example in my case it would be dark
8. That is my style sheet tag would look like

`<link rel="stylesheet" type="text/css" href="https://theme-park.dev/css/base/filebrowser/dark.css">`

You can change yours to one of many themes available at
[Theme-park](https://docs.theme-park.dev/themes/filebrowser/#screenshots)

And then Click the **Save** button and reload site
Ahhhhh Voila!!!

![File browser theme preview](https://i.imgur.com/xki0DAm.png)

## Sharing Files and folders

Choose a file/folder, click the share button above
![Step 1](https://i.imgur.com/2KUP0PK.png)
1. Set a Integer value for time
2. Choose Duration type : Hour, Day, seconds etc
3. Set a optional Password
4. Click share

![Step 2](https://i.imgur.com/iI6jdzd.png)

Copy the Link

![Step 3](https://i.imgur.com/5UplL9w.png)

Brows it in a new tab
Fill in the password if set and click submit

![](https://i.imgur.com/Kq7Nt3s.png)

Now you can download your file or folder from here

![](https://i.imgur.com/RxyuoQ7.png)

Learn more about file browser at : https://filebrowser.org/
