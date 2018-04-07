---
title: Radarr
media_order: 'radarrAddWebbookPlex.png,radarrReverseProxy.png,radarrAddIndexer.png,discordGetWebhooks.png,discordAddWebhook.png,radarrAddWebhookDiscord.png,radarrListsAdd.png,radarrListsAddImdb.png'
visible: true
googletitle: Radarr
googledesc: 'In this guide about Radarr for movie management. We teach you how to install and configure it for use in your environment.'
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
// Install Radarr
wget https://github.com/Radarr/Radarr/releases/download/v0.2.0.995/Radarr.develop.0.2.0.995.linux.tar.gz
sudo tar -zxf Radarr.develop.0.2.0.995.linux.tar.gz -C /opt/
    
// Add Radarr user
sudo adduser --system --no-create-home --group radarr
sudo chown -R radarr:radarr /opt/Radarr
    
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

Head on over to `http://127.0.0.1:7878/settings/connect`

Click the `+` button, select `Plex Media Server` and fill in with these details:

![Add Plex Webhook](radarrAddWebbookPlex.png?lightbox=2048&cropResize=300,300)

Hit the `Test` button to verify it all works, then click `Save`
    
##### Discord

Open your Discord client and Right click your server, from there select `Server Settings` then `Webhooks`
![Get Webhooks](discordGetWebhooks.png?lightbox=2048&cropResize=300,300)

Click on `Create Webhook` and fill int he details, these details can be whatever you feel like, this will also be the place to put a logo for the hook.
![Add Webhook](discordAddWebhook.png?lightbox=2048&cropResize=300,300)

Head on over to `http://127.0.0.1:7878/settings/connect`

Click the `+` button, select `Slack` and fill in with the details you set earlier for us it will look something like this:

![Add Webhook](radarrAddWebhookDiscord.png?lightbox=2048&cropResize=300,300)

! **PLEASE NOTE** The URL you get from Discord will need to be slightly modified, you will need to append `/slack` to the end of the url.

Hit the `Test` button to verify it all works, then click `Save`

#### Adding Indexers

Adding an Indexer can vary depending on type and backend. Things like [Jackett](/jackett) will have their own guide here. However as Radarr does support a lot of Indexers out of the box, we will provide a generic guide here. Turn your browser to `http://127.0.0.1:7878/settings/indexers` and hit the `+` button.

![Add Indexer](radarrAddIndexer.png?lightbox=2048&cropResize=300,300)

Clicking on any of the options will bring up a box like this:

(IMAGE HERE)

Fill in the details for the Indexer you would like to use and push the `Test` button. If this validates you can go ahead and press `Save`. If it fails, double check the details entered and/or try manually logging into the site in an Incognito Window to verify the details are in fact correct.

#### Adding Download Clients

Adding download clients is relatively simple, however it is best explained in the client section labeled `Management Integration` located in each of the [Torrent](/media-ingestion/torrents) and [Usenet](/media-ingestion/usenet) clients.

#### Lists!

Oh yeah! Lists, where everything adds by itself. Simply find an IMDb List somewhere and Radarr will monitor it for movies you don't have, then it'll add them.

Start off by going to `http://127.0.0.1:7878/settings/netimport` then hitting the `+` button

![Add List](radarrListsAdd.png?lightbox=2048&cropResize=300,300)

For this guide we are going to use this list `http://www.imdb.com/list/ls058813655/` which was found on Google using the search string `imdb movies 2018 hollywood` From the URL we are going to need this bit between the last set of /'s. For us this will be `ls058813655`. So click on `Radarr Lists > Presets > IMDb List`

You will get a window that looks like this:

![Add IMDb List](radarrListsAddImdb.png?lightbox=2048&cropResize=300,300)

Fill it out with the List ID, Minimum availability and Profile. For this guide we would recommend ticking `Add Films Monitored` and `Automatic Movie Sync`. The `Path to list` field should be set to `/imdb/list?listId=ls058813655` like the image above.

Click `Test` and verify everything is all good. Then click on `Save`



#### Reverse Proxy

##### Radarr

To configure the Radarr side, we may need to change what is known as the 'URL Base' or 'Base URL'. We can achieve this by opening up `http://127.0.0.1:7878/settings/general` and filling in the box as follows:

![Configure Base URL](radarrReverseProxy.png?lightbox=2048&cropResize=700,200)

! Something to note, while setting this up, a lot of people will advise with prefixing or trailing slashes, we have found that this isn't necesary for Radarr itself. Also while you can name your directory name in Radarr, it will need to match on the [Reverse Proxy](#reverse-proxy).

##### Nginx

```nginx
location /radarr/ {
	proxy_pass http://127.0.0.1:7878/radarr/;
	proxy_set_header X-Real-IP $remote_addr; 
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	proxy_set_header X-Forwarded-Proto $scheme;
	proxy_http_version 1.1;
	proxy_no_cache $cookie_session;
	proxy_set_header Accept-Encoding "";
}
```

##### Caddy

```
proxy /radarr 127.0.0.1:7878 {
	transparent
}
```

##### Apache

```apache
<Location /radarr>
	ProxyPass http://127.0.0.1:7878
	ProxyPassReverse http://127.0.0.1:7878
</Location>
```