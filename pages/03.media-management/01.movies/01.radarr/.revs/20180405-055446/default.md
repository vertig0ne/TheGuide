---
title: Radarr
visible: true
twittercardoptions: summary
articleenabled: false
musiceventenabled: false
orgaenabled: false
orga:
    ratingValue: 2.5
orgaratingenabled: false
eventenabled: false
personenabled: false
restaurantenabled: false
restaurant:
    acceptsReservations: 'yes'
    priceRange: $
---

[TOC]

## Installation

#### Local Installation

##### Dependancies

If you have already installed these dependancies from other areas of the guide. You can safely ignore this particular section and move onto the next.

```bash
// Install mono
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb http://download.mono-project.com/repo/ubuntu stable-xenial main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
sudo apt update
sudo apt install mono-devel
```

##### Application
```bash
// Install Radarr
wget https://github.com/Radarr/Radarr/releases/download/v0.2.0.995/Radarr.develop.0.2.0.995.linux.tar.gz
tar -zxf Radarr.develop.0.2.0.995.linux.tar.gz -C /opt/
    
// Add Radarr user
adduser --system --no-create-home --group radarr
chown -R radarr:radarr /opt/Radarr
    
// Create Radarr Service
wget https://gist.githubusercontent.com/vertig0ne/644846b495461b4462f5f610277e6d58/raw/ff5f4a64d187c3e0b004d49cd7acd3eab3e8c21c/radarr.service
sudo mv radarr.service /etc/systemd/system/
sudo systemctl daemon-reload
    
// Start Radarr and Enable startup at system boot
sudo systemctl enable radarr
sudo systemctl start radarr
```

#### Docker Installation

```bash
docker create \
	--name=radarr \
	-v ~/.config/radarr:/config \
    -v ~/Downloads:/downloads \
    -v /mnt/media/Movies:/movies \
    -v /etc/localtime:/etc/localtime:ro \
    -p 7878:7878 \
	linuxserver/radarr
```

## Configuration

#### Initial Configuration

Now that you have Radarr installed and started, you should be able to get to it at `http://127.0.0.1:7878`

#### Adding WebHooks
##### Plex

##### Discord

#### Adding Indexers

#### Adding Download Clients

#### Lists!

#### Reverse Proxy

##### Radarr

##### Nginx

##### Caddy

##### Apache