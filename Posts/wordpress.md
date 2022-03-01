## Wordpress
### A CMS for blogging and more

*WordPress* is a rich content management system which can utilize plugins, widgets, and themes. 

## Links
Docker Image : https://hub.docker.com/_/wordpress

## What we will be doing ?

1. Spin up a VPS
2. Install Docker and Docker-compose
3. Pull Docker Image for Wordpress
4. Installing and configuring Wordpress
5. Making WP Filesystem Management Easy with FileBrowser (Bonus)
6. Changing a few important php settings - Upload size and Post size
7. Setting up a Basic Site
8. Setting up a reverse proxy with SSL certificate


## Spin up a VPS

This is a basic login process of a Linux VPS

- Open terminal (CMD, Tabby, Windows Terminal etc.)
- type ssh root@x.x.x.x (x.x.x.x is your serverIP)
- fill in your password for root
- Update your system `sudo apt update && sudo apt upgrade` (recommended, but not related to login)
- Now that you are in the system you are ready to do the next part in the guide

## Install Docker and Docker-compose


### What's Docker ?
Docker let's you get prebuilt images of software and their dependancies that run LIKE a vm but not exactly
Docker pulls these images from hub.docker.com a public directory of docker images

### What's Docker-compse ?

Docker-Compose is a tool for defining and running multi-container Docker applications. 
With Compose, you use a YAML file to configure your application’s services. 
Then, with a single command, you create and start all the services from your configuration. 

### To install Docker and docker-compose

Have a look at our Docker and docker-compose guide here:

https://github.com/godarayudhvir/forum.cyberalliance.in/blob/main/Posts/docker.md

## Pull Docker Image for Wordpress

- goto root folder
- create a folder "wp"
- browse into the directory cd wp
- create and open docker-compose file `nano docker-compose.yml`
- paste in the contents from below
- Use the command `docker-compose up -d`

**Docker Compose File**

```
version: '3.1'

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80 

# you can replace 8080 with port of your choice..
# your site will be at serverip:8080

    environment:
      WORDPRESS_DB_HOST: db #leave it as is
      WORDPRESS_DB_USER: exampleuser  #change it to username of choice
      WORDPRESS_DB_PASSWORD: examplepass #choose a strong password
      WORDPRESS_DB_NAME: exampledb #name the database
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: exampledb #choose name for the database
      MYSQL_USER: exampleuser #choose a username for mysql
      MYSQL_PASSWORD: examplepass #choose a strong! password for mysql
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:

```
### What have we done so far ?

- we logged in to the server
- we installed docker and docker-compose
- We created a docker-docker compose file to pull the required images(Wordpress, Mysql)
- where MySql is a dependancy of Wordpress
- We then configured docker-compose.yml based on our liking
- We then pulled the image via docker-compose up -d

### checking if our Docker images are running

Run `Docker ps -a`

you should then be able to see something like
![wp running on docker](https://i.imgur.com/wprunningondocker.png)

## Installing and configuring Wordpress

- Goto **youserverip:8080**
- fill in the admin registration forum

![admin registration forum](https://i.imgur.com/adminregforum.png)

You should now be at the welcome page of wordpress

![wordpress welcome](https://i.imgur.com/wpwelcome.png)

## Making WP Filesystem Management Easy with FileBrowser (Bonus)

### What is Filebrowser ?
Filebrowser is a WEB Gui based Filemanager that you can use to manager files and folders on your
server via a web browser, simple as that.

### Installing Filebrowser
Have a look at our Docker and docker-compose guide here:

https://github.com/godarayudhvir/forum.cyberalliance.in/blob/main/Posts/file-browser.md

## Changing a few important php settings - Upload size and Post size

If you paused the video and went on using Wordpress and tried to upload something more than 2MB
you would have noticed that you are limited to uploading at max 2MB/file... not just that
you also have a limit of Post size. :laughing:

to fix that we need to set it to our desired limit by going to the docker volume for wp(wordpress)
and finding the .htaccess file | we will then add these two lines there

```

php_value upload_max_filesize xxxxM
php_value post_max_size yyyyM

```

here we are telling apache to tell php.ini that we are overriding the php.ini for this directory and everything underneath it.

Once you have made these changes, you will want to restart your web server and php services to read in the modifications.



## Setting up a Basic Site

Have a look at our WP basics guide here: (comingsoon)

## Setting up a reverse proxy with SSL certificate

1. Install and configure Nginx proxy manager as explained "[here](https://github.com/godarayudhvir/forum.cyberalliance.in/blob/main/Posts/Nginxproxymanager.md)"
2. Login to Nginx proxy manager
3. Go to Hosts > Proxy Hosts
4. Click on Add proxy Host

Fill it as seen below

1. Replace "filebrowser.yourdomain.tld" with your prefered subdomain followed by your domain url
2. Type your servers ip in forward hostname box
3. Forward the port, in our config(docker-compose.yml) we had it set to 8080
4. Choose Cache Assets, Block Common Exploits

![Setting up Proxy](https://i.imgur.com/6yMYmRO.png)

Now go to SSL Tab

1. Under SSL certificate, choose "Request a new SSL Cert" from the dropdown menu
2. Enable Force SSL
3. Fill in your email address
4. Click on I agree to Tos
5. Click save

![Setting up SSL](https://i.imgur.com/kigFJzL.png)

After a while, you site should be live on subdomain.yourdomain.tld no need to type
serverip:8080 from now on and plus it has **SSL** now.

![SSL active](https://i.imgur.com/wpsslactiveproof.png)

Have a look at more of our guides.
- Thanks