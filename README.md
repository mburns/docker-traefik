# Description

This is the updated docker-compose repo of all the media, home, and web server apps described in the following guides on our website:

- [Docker Media Server Ubuntu: Compose for 23 Awesome Apps](https://www.smarthomebeginner.com/docker-media-server-2022/)
- [Ultimate Traefik Docker Compose Guide [2022] with LetsEncrypt](https://www.smarthomebeginner.com/traefik-docker-compose-guide-2022/)
- [WordPress on Docker with Nginx, Traefik, LE SSL, Security, and Speed](https://www.smarthomebeginner.com/wordpress-on-docker-traefik/)
- [Ultimate Synology NAS Docker Compose Media Server 2022](https://www.smarthomebeginner.com/synology-nas-docker-media-server-2022/)

### Obsolete Posts (for educational purposes):

The following posts have been updated/replaced by the posts linked above:

- [Docker Media Server with Traefik 2 Reverse Proxy](https://www.smarthomebeginner.com/traefik-2-docker-tutorial/)
- [Docker Media Server without Reverse Proxy ](https://www.smarthomebeginner.com/docker-home-media-server-2018-basic/)
- [Docker Media Server with Traefik 1 Reverse Proxy](https://www.smarthomebeginner.com/traefik-reverse-proxy-tutorial-for-docker/)
- [Synology Docker Media Server with Traefik, Docker Compose, and Cloudflare](https://www.smarthomebeginner.com/synology-docker-media-server/)

### Description of Compose Files in this Repo

- docker-compose-t2.yml - this is my main stack with most apps/services (home aserver), including Traefik
- docker-compose-npm.yml - this is the basic media server stack with Nginx Proxy Manager instead of Traefik
- docker-compose-t2-web.yml - web server specific stack for WordPress and non-WordPress sites with Nginx and Traefik
- docker-compose-t2-synology.yml - apps/services that I run on Synology NAS using Docker Compose for Homelab use

<div style="padding:20px;border: 3px solid red;">
Please note that docker-compose files in the <strong>archives</strong> folder is not actively maintained. They may need updates/rework.
</div>

Almost any app/service from the docker-compose files listed above can be copy-pasted to any other compose file in this repo.

## MY SETUP

- Home Server (docker-compose-t2.yml) - Ubuntu 22.04 Proxmox LXC Container on AMD Ryzen 7 4800u ASROCK 4x4 Box 
- Media Server (docker-compose-t2-media-db.yml) - Ubuntu 22.04 Proxmox LXC Container on AMD Ryzen 7 4800u ASROCK 4x4 Box 
- Web Server (docker-compose-t2-web.yml) - Digital Ocean VPS (2 cores and 2 GB RAM)
- Synology (docker-compose-t2-synology.yml) - Synology DS918+ NAS.

I use Syncthing to keep certain key files synched between various systems.

## What apps are included in this stack?

The apps I use are scattered around in several different docker-compose files. Click the links below for specific installation guides.

 Some apps are used in more than one host and some on only one. 

### FRONTENDS

- Traefik - Reverse Proxy
- Nginx Proxy Manager - Reverse Proxy 
- Docker Socket Proxy - Secure Proxy for Docker API
- Traefik Custom Error Pages
- OAuth - Google OAuth 2 Forward Authentication
- Authelia - Private Forward Authentication
- [Portainer](https://www.smarthomebeginner.com/portainer-docker-compose-guide/) - Container Management
- Organizr - Dashboard for Apps
- Heimdall - Dashboard for Apps
- Homepage - Dashboard for Apps
- Dashy - Dashboard for Apps
- Autoindex - Plain text Index to All Files

### SMART HOME

- Home Assistant Core - Home Automation
- HA-Dockermon - Manage Docker containers in Home Assistant
- Mosquitto - MQTT Broker
- MotionEye - Video Surveillance
- ZoneMinder - Video Surveillance
- MiFlora - MiFlora MQTT Daemon (MiFlora Plant Sensors)

### DATABASE

- MariaDB - MySQL Database
- phpMyAdmin - Database management
- [InfluxDB](https://www.smarthomebeginner.com/influxdb-docker-compose-guide/) - Database for sensor data
- Postgres - Database
- [Grafana](https://www.smarthomebeginner.com/grafana-docker-compose-guide/) - Graphical data visualization for InfluxDB data
- Varken - Monitor Plex, Sonarr, Radarr, and Other Data
- Redis - Key value store
- Redis Commander - Redis management

### DOWNLOADERS

- jDownloader - Download management
- TransmissionBT with VPN - Torrent Downloader.
- SABnzbd - Binary newsgrabber, NZB downloader
- Nzbget - Binary newsgrabber, NZB downloader
- qBittorrent with Wireguard VPN from [Surfshark](https://bit.ly/shb-surfshark) - Torrent downloader

### INDEXERS

- NZBHydra2 - NZB meta search 
- Jackett - Torrent proxy
- Prowlarr - Torrent proxy

### PVRS

- Lidarr - Music Management
- Radarr - Movie management
- Sonarr - TV Shows management
- LazyLibrarian - Books Management
- Readarr - Books Management

### MEDIA SERVER

- AirSonic - Music Server
- NaviDrome - Music Server
- FunkWhale - Music Server
- Calibre - Ebook/Audiobook Server
- Calibre-Web - Ebook/Audiobook Reader
- [Plex](https://www.smarthomebeginner.com/plex-docker-compose/) - Media Server
- Emby - Media Server
- [Jellyfin](https://www.smarthomebeginner.com/jellyfin-docker-compose/) - Media Server
- Ombi - Media Requests
- Tautulli - Previously PlexPy. Plex statistics and monitoring
- Plex-Sync - For Syncing watched status between plex servers
- PhotoShow - Personal Photo Gallery and viewer
- TellyTv- IPTV proxy for Plex
- xTeve- IPTV proxy for Plex

### MEDIA FILE MANAGEMENT

- Bazarr - Subtitle Management
- Picard - Music Library Tagging and Management
- Handbrake - Video Conversion, Transcoding, and Compression
- MKVToolNix - Video Editing, Remuxing (changing media container while keeping original source quality)
- MakeMKV - Video Editing (Ripping from Disks)
- FileBot - File renamer
- Tiny Media Manager - Media Files Management

### UTILITIES

- Firefox - Web Broswer
- Glances - System Information
- APCUPSD - APC UPS Management
- Guacamole - Remote desktop, SSH, on Telnet on any HTML5 Browser
- Guacamole Daemon - Needed for Guacamole
- [Dozzle](https://www.smarthomebeginner.com/dozzle-docker-compose-guide/) - Docker logs viewer
- qDirStat - Directory Statistics
- StatPing - Status Page & Monitoring Server
- SmokePing - Network Latency Monitoring
- VS Code Server - Code Editor
- Logarr - Log Management
- Monitorr - Webfront to display the status of any webapp or service
- Cloud Commander - Web File Manager
- Cloud9 - Cloud IDE
- SMTP To Telegram - Sends all incoming Email messages to Telegram
- UniFi Controller - Controller for Ubiquiti UniFi Network Gear
- Rclone - Mount Cloud/Google Drive
- MergerFS - Merge local and remote file systems
- Gluetun - VPN client for docker containers and more
- DeUnhealth - Auto restart containers on VPN restart
- [AdGuard Home](https://www.smarthomebeginner.com/adguard-home-docker-compose-guide/) - DNS Sinkhole / Ad-blocker

### WEB

- Nginx - Web Server
- php7 - PHP-FPM

### MAINTENANCE

- Watchtower - Automatic Docker Container Updates
- Docker-GC - Automatic Docker Garbage Collection
- Traefik Certificate Dumper - Extract Traefik SSL Certs
- Cloudflare DDNS - Dynamic IP Updater
- Cloudflare Companion - Automatic CNAME creation for services
- WhoAmI - For testing.

## Starting and Stopping

I use bash_aliases to simplify starting and stopping containers/stack. Included in the repo is an example of bash_aliases I use (replace USER with your Linux username). Here are some example alias commands:

- <strong>dcup2</strong> - Start Docker Traefik 2 stack
- <strong>dcdown2</strong> - Stop Docker Traefik 2 stack
- <strong>dcrec2</strong> - Start or recreate a specific service
- <strong>dcstop2</strong> - Stop a specific service
- <strong>dcrestart2</strong> - Restart a specific service
- <strong>dclogs2</strong> - See real-time logs for the corresponding stack or service
- <strong>dcpull2</strong> - Pull new images for the corresponding stack or service