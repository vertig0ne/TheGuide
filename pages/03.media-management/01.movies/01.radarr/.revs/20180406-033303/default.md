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
docker start radarr
```

## Configuration

#### Initial Configuration

Now that you have Radarr installed and started, you should be able to get to it at `http://127.0.0.1:7878`

#### Adding WebHooks
##### Plex

Head on over to `http://127.0.0.1:7878/settings/mediamanagement#notifications`

Click the `+` button, select `Plex Media Server` and fill in with these details:

(IMAGE HERE)

Hit the `Test` button to verify it all works, then click `Save`
    
##### Discord

Head on over to `http://127.0.0.1:7878/settings/mediamanagement#notifications`

Click the `+` button, select `Slackr` and fill in with these details:

(IMAGE HERE)

! **PLEASE NOTE** The URL you get from discord will need to be slightly modified, you will need to append `/slack` to the end of the url.

Hit the `Test` button to verify it all works, then click `Save`

#### Adding Indexers

#### Adding Download Clients

#### Lists!

#### Reverse Proxy

##### Radarr

##### Nginx

! **PLEASE NOTE** If you have not completed Organizr setup, the `auth_request` will not pass and will either constantly fail authentication or make the page return a HTTP 500 Error

```nginx
location /radarr/ {
	auth_request /auth-admin;
	proxy_pass http://127.0.0.1:7878/radarr/;
	proxy_set_header X-Real-IP $remote_addr; 
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	proxy_set_header X-Forwarded-Proto $scheme;
	proxy_http_version 1.1;
	proxy_no_cache $cookie_session;
	proxy_set_header Accept-Encoding "";

	location /radarr/api {
		auth_request off;
		proxy_pass http://127.0.0.1:7878/radarr/api;
	}
}
```

##### Caddy

##### Apache