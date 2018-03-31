---
title: Basics
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

## Table of Contents
1. [Basic Knowledge](#basic-knowledge)
2. [Basic Initialisation](#basic-initialisation)
3. [Assumptions](#assumptions)

### Basic Knowledge

##### Linux OS

We generally recommend the Linux OS for general use due to it's minimalist nature. As most of the applications that are used do not provide a GUI for you to use, most provide a Web-Based frontend so you can still access it. Because of this it means that we do not need to have a traditional "Desktop". It also means we can generally leave a computer in the corner of the household with no screen, no keyboard and no mouse plugged in. For this guide we will generally assume an Debian based OS like Ubuntu. We only need to install Ubuntu-Server for this as we will be doing everything over ssh.


### Basic Initialisation

Using the lines below will ensure that your setup right from the start has the folder structure that we will be using throughout the guide.

```bash
sudo apt update
sudo apt upgrade -y
mkdir -p /mnt/media
mkdir /mnt/media/(Books,Music,Movies,Series)
```

### Assumptions