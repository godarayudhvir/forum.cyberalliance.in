## Navidrome

### Your personal music streaming service

Navidrome allows you to enjoy your music collection from anywhere, by making it available through a modern Web UI and through a wide range of third-party compatible mobile apps, for both iOS and Android devices.

Navidrome is open source software distributed free of charge under the terms of the GNU GPL v3 license.

## ⭐ Features

- Very low resource usage. Runs well even on simple Raspberry Pi Zero and old hardware setups
- Handles very large music collections
- Streams virtually any audio format available
- Reads and uses all your beautifully curated metadata
- Great support for compilations (Various Artists albums) and box sets (multi-disc albums)
- Multi-user, each user has their own play counts, playlists, favorites, etc..
- Multi-platform, runs on macOS, Linux and Windows. Docker images are also provided
- Ready to use, official, Raspberry Pi binaries and Docker images available
- Automatically monitors your library for changes, importing new files and reloading new metadata
- Themeable, modern and responsive Web interface based on Material UI
- Compatible with all Subsonic/Madsonic/Airsonic clients. See below for a list of tested clients
- Transcoding on the fly. Can be set per user/player. Opus encoding is supported
- Translated to 17 languages (and counting)
- Full support for playlists, with option to auto-import .m3u files and to keep them in sync
- Last.fm and ListenBrainz scrobbling

### 🌟Features supported by the Subsonic API

- Tag-based browsing/searching
- Playlists
- Bookmarks (for Audiobooks)
- Starred (favourites) Artists/Albums/Tracks
- 5-Star Rating
- Transcoding
- Get/Save Play Queue (to continue listening in a different device)
- Last.fm and ListenBrainz scrobbling
- Artist Bio from Last.fm
- Artist Images from Spotify (requires configuration)
- Lyrics (from embedded tags)

***Available Clients (Alternate to Navidrome Web UI)***

- Android Client : https://substreamerapp.com | https://github.com/austinried/subtracks
- iOS Client : https://apps.apple.com/us/app/isub-music-streamer/id362920532
- Linux Client : https://sublimemusic.app/
- Windows Client : https://github.com/jeffvli/sonixd
- Alexa (Skill) 🤭 https://github.com/srichter/asksonic#readme

## Check out Demo 😋

https://www.navidrome.org/demo

## Installation

Learn how to install Navidrome on your specific platform
Download

Visit the [releases page](https://github.com/navidrome/navidrome/releases) in GitHub and download the latest version for your platform. There are builds available for Linux (Intel and ARM, 32 and 64 bits), Windows (Intel 32 and 64 bits) and macOS (Intel 64 bits).

For ARM-Based systems (ex: Raspberry Pi), check which ARM build is the correct one for your platform using cat /proc/cpuinfo.

Remember to install ffmpeg in your system, a requirement for Navidrome to work properly. If your OS does not provide a package for ffmpeg, you may find the latest static build for your platform here: https://johnvansickle.com/ffmpeg/.

### Downloading Setup

- [Using the official docker images with Docker and Docker Compose](https://www.navidrome.org/docs/installation/docker/)
- [Steps to install on Ubuntu Linux (and other Debian based distros)](https://www.navidrome.org/docs/installation/linux/)
- [Steps to install on Windows](https://www.navidrome.org/docs/installation/windows/)
- [Steps to install on macOS](https://www.navidrome.org/docs/installation/macos/)
- [Steps to install on FreeBSD (using ports or package)](https://www.navidrome.org/docs/installation/freebsd/)
- [Community Maintained Packages](https://www.navidrome.org/docs/installation/packages/)
- [Navidrome packages for simpler installation on some platforms, powered by You!](https://www.navidrome.org/docs/installation/packages/)

`We'll be doing by the docker method, everything else is beyond the scope of this Tutorial atleast at the time of writting`

## Let's Do it!

- Browse to the root directory
- Create a folder "**navidrome**"
- Browse into the folder
- Create a docker-compose file using `nano docker-compose.yml`
- Paste the content below
- Save the docker file
- Exit out the docker file
- Run `docker-compose up -d`

```version:
version: "3.3" #version of your docker-compose
services:
  navidrome:
    image: deluan/navidrome:latest
    ports:
      - "4534:4533" # Map port 4533 in the container to port 4534 on the Docker host.
    environment:
      # Optional: put your config options customization here
      ND_SCANSCHEDULE: "@every 1m"
    volumes:
      - "./data:/data"
      - "./music:/music:ro"
```

### Running Navidrome for first time

- Goto serverip:4534
- You will be asked to create a admin account, do that.
- Add Music in the Music folder
- reload the site
- Your music should be there, if not click the button next to refresh button on top right, then click on full scan.

### Configuration options

Add the following under Environement in docker-compose.yml
Make Dark theme the default : `ND_DEFAULTTHEME: "Dark"`
Disable Downloads : `ND_ENABLEDOWNLOADS: "false"`

Enable autogenerated Avatar : `ND_ENABLEGRAVATAR: "true"` *requires docker restart

References:
https://www.navidrome.org/docs/usage/configuration-options/

### External Integrations



Enable External Metadata providers
https://www.navidrome.org/docs/usage/external-integrations/

### Security

- To protect against brute-force attacks, Navidrome is configured by default with a login rate limiter
- You should **NOT** run Navidrome as root. Ideally you should have it running under its own user. Navidrome only needs read-only access to the Music Folder, and read-write permissions to the Data Folder.
- Navidrome By default encrypts all user passwords.

Learn more : https://www.navidrome.org/docs/usage/security/

### Setting up a Reverse Proxy and point to a domain

1.  Install and configure Nginx proxy manager as explained "[here](https://forum.cyberalliance.in/public/d/17-install-nginx-proxy-manager)"
2.  Login to Nginx proxy manager
3.  Go to Hosts > Proxy Hosts
4.  Click on Add proxy Host

Fill it as seen below

1.  Replace "service.yourdomain.tld" with your prefered subdomain followed by your domain url
2.  Type your servers ip in forward hostname box
3.  Forward the port, Navidrome comes with 4533 by default
4.  Choose Cache Assets, Block Common Exploits

![](https://i.imgur.com/MIN4sAY.png)

Now go to SSL Tab

1.  Under SSL certificate, choose "Request a new SSL Cert" from the dropdown menu
2.  Enable Force SSL
3.  Fill in your email address
4.  Click on I agree to T.O.S
5.  Click save

![Setting up SSL](https://i.imgur.com/kigFJzL.png)

After a while, you site should be live on filebrowser.yourdomain.tld no need to type
serverip:4534 from now on and plus it has **SSL** now.

![SSL active](https://i.imgur.com/NKIi1qQ.png)

References :
[https://en.wikipedia.org/wiki/List\_of\_HTTP\_status\_codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

### Running Navidrome on Android client
*Running Navidrome on other clients is beyond the scope of this tutorial because I don't own a iphone 😩 Gimme 499$ and I'll do that 🤣

So I'll be using [substreamer](https://play.google.com/store/apps/details?id=com.ghenry22.substream2&hl=en&gl=US)
![](https://i.imgur.com/DwYo0q9.png)

- Download the app
- Type your server url choose https if enabled
- Fill in login credentials
- Click login
- And done! you are probably in

## That's all Folks!
![](https://i.imgur.com/9bjDSpm.png)

Learn more about Navidrome at https://www.navidrome.org/docs/
