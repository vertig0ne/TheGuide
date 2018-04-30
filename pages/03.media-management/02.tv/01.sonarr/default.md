---
title: Sonarr
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

! If you have already installed these dependancies from other areas of the guide. You can safely ignore this particular section and move onto the next.

```bash
// Install mono
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb http://download.mono-project.com/repo/ubuntu stable-xenial main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
sudo apt update
sudo apt install mono-devel
```

##### Application
```bash
// Install Sonarr
wget https://github.com/Sonarr/Sonarr/archive/v2.0.0.5163.tar.gz
sudo tar -zxf v2.0.0.5163.tar.gz -C /opt/Sonarr
    
// Add Sonarr user
sudo adduser --system --no-create-home --group sonarr
sudo chown -R sonarr:sonarr /opt/Sonarr
    
// Create Sonarr Service
https://gist.githubusercontent.com/vertig0ne/644846b495461b4462f5f610277e6d58/raw/72cf218aa160c08b7c6e5c34258eb568cdfb7f53/sonarr.service
sudo mv sonarr.service /etc/systemd/system/
sudo systemctl daemon-reload
    
// Start Sonarr and Enable startup at system boot
sudo systemctl enable sonarr
sudo systemctl start sonarr
```


#### Docker Installation

```bash
docker create \
	--name=sonarr \
	-v ~/.config/sonarr:/config \
    -v ~/Downloads:/downloads \
    -v /mnt/media/Series:/series \
    -v /etc/localtime:/etc/localtime:ro \
    -p 8686:8686 \
	linuxserver/sonarr
docker start sonarr
```

## Configuration

#### Initial Configuration

#### Adding WebHooks
##### Plex

##### Discord

#### Adding Indexers

#### Adding Download Clients

#### Reverse Proxy

##### Sonarr

##### Nginx

##### Caddy

##### Apache