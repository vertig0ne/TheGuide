---
title: Plex
media_order: 'serverSetupName.png,addLibraryTypeSeries.png,serverDashboard.png,addLibraryAdvancedMusic.png,addLibraryFolderMusic.png,addLibraryMusicOptions.png,serverSetupLibraryFull.png,addLibraryFolderRoot.png,serverSetupLibraryEmpty.png,serverSetupDone.png,addLibraryFolderMovie.png,addLibraryAdvancedMovie.png,addLibraryTypeMovie.png,addLibraryTypeMusic.png,addLibraryFolderSeries.png,addLibraryAdvancedSeries.png,addLibraryTypes.png,plex.png'
process:
    markdown: true
    twig: true
visible: true
googletitle: 'Plex Installation & Configuration'
googledesc: 'Guide to install Plex Media Server and configure Music, Movies and TV Show libraries'
twitterenable: true
twittercardoptions: summary
twittershareimg: /media-servers/plex/serverSetupName.png
twittertitle: 'Plex Installation & Configuration'
twitterdescription: 'Guide to install Plex Media Server and configure Music, Movies and TV Show libraries'
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
facebookenable: false
facebooktitle: 'Plex Installation & Configuration'
facebookdesc: 'Guide to install Plex Media Server and configure Music, Movies and TV Show libraries'
page-toc:
    active: true
---

![](plex.png?lightbox=600,400&resize=200,200){.center}

[TOC]

### What is Plex?

Plex in itself is a Media Server, it can serve your media to you anywhere in the world. It currently supports Video and Audio based media. As an added benefit you are also able to share access to your server to your friends and family.

### Installation 

##### Local Installation 

First of all, we need to get the latest download links to which we will pop over to Plex website to get the links.

[https://www.plex.tv/downloads/](https://www.plex.tv/downloads/)

Select Linux in the drop down list, then click select distribution, right click on the distribution and click on "Copy link address" for the guide we will be using the url `https://downloads.plex.tv/plex-media-server/1.12.1.4885-1046ba85f/plexmediaserver_1.12.1.4885-1046ba85f_amd64.deb` however if there is a newer version (which there likely will be) then just paste the url from your clipboard wherever you see this link.

```bash
wget https://downloads.plex.tv/plex-media-server/1.12.1.4885-1046ba85f/plexmediaserver_1.12.1.4885-1046ba85f_amd64.deb
sudo dpkg -i plexmediaserver_1.12.1.4885-1046ba85f_amd64.deb
systemctl plexmediaserver enable
systemctl plexmediaserver start
```

##### Docker Installation 

Docker has a few caveats due to the way it works, however, there are workarounds.
First of all, head over to [Here](https://www.plex.tv/claim/) and get a claim id. Use this claim id in the PLEX_CLAIM variable below.

Second of all, by running `ip addr` in the terminal, will get the machines IP address, use this to replace `hostIPAddress` in the ADVERTISE_IP variable below.

```bash
docker run \
	-d \
	--name plex \
	-p 32400:32400/tcp \
	-p 3005:3005/tcp \
	-p 8324:8324/tcp \
	-p 32469:32469/tcp \
	-p 1900:1900/udp \
	-p 32410:32410/udp \
	-p 32412:32412/udp \
	-p 32413:32413/udp \
	-p 32414:32414/udp \
	-e TZ="Europe/London" \
	-e PLEX_CLAIM="claimToken" \
	-e ADVERTISE_IP="http://hostIPAddress:32400/" \
	-h plex \
	-v ~/.docker/plex:/config \
	-v /dev/shm:/transcode \
	-v /mnt/media:/data \
plexinc/pms-docker
```

### Configuration 


##### Initial Configuration

After connecting to `http://127.0.0.1:32400/` (or if using docker the `ADVERTISE_IP`) 

You should end up with a screen that looks something like this:

![Plex Server Setup Page](serverSetupName.png?lightbox=1024&cropResize=300,300)

As you go through each step to setup your Movies, Music and TV Show libraries and point them to the paths we setup in the [Basics](/home/basics) page but please feel free to use the below images as guides to some advanced options.

! Please bear in mind that Premium Music Library is **ONLY** available with a Plex Pass

{% set array = [] %}
{% for item in page.media.images %}
{% if item.html matches "/.addLibrary*/" %}
{% set array = array|merge([item]) %}
{% endif %}
{% endfor %}

{{ unite_gallery(array, '{"gallery_theme":"tiles", "tiles_type":"justified"}') }}

Once you have completed the initial configuration you will be presented with a screen that looks like this:

![Plex Dashboard](serverDashboard.png?lightbox=1024&cropResize=300,300)