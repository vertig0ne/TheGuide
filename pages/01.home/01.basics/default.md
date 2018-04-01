---
title: Basics
visible: true
googletitle: 'Basics | The Guide'
googledesc: 'Building your own Media Server can lead you down a dark path. Here''s some tips  and tricks to try and help you through to the other side'
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

### Basic Knowledge

##### Linux OS

We generally recommend a Linux based OS due to its minimalist nature as most of the applications that we recommend do not provide a traditional GUI (graphical user interface), most provide a Web-Based frontend, accessed through a web browser, for management purposes. This means that we do not need to have a traditional "Desktop". It also means we can leave the media server in the corner of the household with no screen, no keyboard and no mouse plugged in. For this guide we will assume you are using a Debian based Linux distro (OS) like Ubuntu. To begin, simply install Ubuntu-Server on your media server and make sure the openssh packages are installed and port 22 is open as from here on out we will be doing everything over ssh.


### Basic Initialisation

Using the lines below will ensure that your media server has the correct folder structure that we will be using throughout the guide.

```bash
sudo apt update
sudo apt upgrade -y
mkdir -p /mnt/media
mkdir /mnt/media/(Books,Music,Movies,Series)
```

### Assumptions