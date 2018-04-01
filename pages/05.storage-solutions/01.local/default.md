---
title: Local
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

## UnRAID

UnRAID is a complete operating system which is designed for this specific use case. Has many benefits over the other solutions with features such as a Web Interface, Docker Host and Virtual Machine Hypervisor. All this while also handling your files. You would be able to follow the rest of the guide with the "Docker Installation" sections for apps. The downside with this, is unlike one of its competitors like FreeNAS is that after a few hard drives, there is a one-time fee. However it is in our opinion that the benefits of this fee far outweigh any struggles you may end up having with other options.

## FreeNAS

FreeNAS like UnRAID is a complete operating system, also comes with features such as a Web Interface and supports Jails so you will be able to run some apps. One of the benefits is the cost, the clue is in the name. It's free. It handles hard drives more closely to a RAID setup, so does give you added reliability and resilience, but it does this at the cost of being quite strict with what it will and will not support. Like smaller HDD's, cache drives and the likes.

## Ubuntu

Ubuntu is just a standard operating system. We recommend installing Ubuntu-Server rather than the Desktop installation as we do not need the desktop. There is also no web interface, you have to be comfortable within the command line. However you can always install your own docker host, hypervisor and an application called SnapRAID which will provide similar functionality to UnRAID. This is good for people that already have a setup with some drives already and just want to provide some parity features to the system. However if you are a new setup, we would recommend FreeNAS or UnRAID over this.
