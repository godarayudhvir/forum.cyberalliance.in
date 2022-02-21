### Installing Docker, Docker-compose
#### Docker and Docker Compose
Docker was confusing to me at start.  
I really just didn't get it.  I knew what it was and all... but always ran into errors
So I gave up, then I found a community of Selfhosters, who would down the road teach me there ways
and, at some point, it just clicked with me!!

The best explanation I can give, 
is exactly what their logo tried to exhibit.  
Docker is like the Items in a container on a ship, comes in all shapes and sizes could be
Example : Reality(services that docker can run)
TV(plex), Servers(ubuntu system), and what not can come in a container/services 🤷‍♂️ 
Future Reference : >!and the Portainer is that Ship that carries it all!<

In reality, Docker is a virtual environment (think Virtual Box, etc) 
where you run servers in virtual machines that are very slimmed down 
to only have the most necessary pieces of software.

Docker-Compose is a tool to make it a bit easier to get Docker containers 
(especially multiple containers that need to communicate) up and running using a static configuration file.

I use the instructions at Digital Ocean, linode docks, fleet.linuxserver.io, hub.docker.com
for documentation on installing various services and docker itself ( docker-ce {community edition} )

I make a script of it, then run the script as I generally work on an LTS (Long Term Support) version of Ubuntu.

create a file docker_install.sh in root

Cd / 
Cd root
nano docker_install.sh

Now paste the content from below

> #!/bin/bash
> sudo apt update
> sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
> curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
> 
> sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
> 
> sudo apt update
> apt-cache policy docker-ce
> sudo apt install docker-ce -y
> 
> #now set user as part of docker group
> sudo usermod -aG docker ${USER}
> 
> #install docker-compose
> sudo apt install docker-compose -y

1. Press Ctrl+O to save
2. Press Enter to Confirm
3. Press Ctrl+x to Close

Give it Execute perms, so we can run it like a .bat file on windows 🤔
>chmod +x docker_install.sh

Now Run it with ( You need to be in the dir(directory where the file is located.. that why we used ./ {means current dir}
>./docker_install.sh

Let it finish...
Progress: [100%] : {###################}
Once done run the following commands to see if docker installed correctly..
![](https://i.imgur.com/JXU5n25.png)
>docker -v
docker-compose -v

You should be able to see the versions.

### Basic Docker Commands

- docker -v
- docker-compose -v
- docker ps
docker ps -a 
- docker-compose up -d
-  docker container stop CONTAINER containerid
- docker run -it -d <image name>
- docker stop <container id>
- docker kill <container id>
- docker rm <container id>
- docker rmi <image-id>
- docker image ls [OPTIONS] [REPOSITORY[:TAG]]

Get docker images at : http://hub.docker.com/
