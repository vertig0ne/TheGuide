---
title: Logarr
media_order: logarr.PNG
published: true
metadata:
    Author: Roxedus
    Keywords: '''docker, selfhost, php, logs'''
taxonomy:
    category:
        - UnRAID
    tag:
        - Docker
        - Self-Host
googletitle: 'Guide | Logarr , UnRAID setup'
googledesc: 'Logarr is a Self-hosted, single-page, log consolidation tool written in PHP'
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

## [Logarr](https://github.com/Monitorr/logarr/tree/docker) is a Self-hosted, single-page, log consolidation tool written in PHP

A webpage to inspect logs, without using the terminal.
![logarr](logarr.PNG)

REPO IS BEEING BUILT

Nginx reverse proxy for subdomain
<pre><code class="nginx">
server { #Redirect non-ssl connections to ssl.
    listen 80;
    server_name logarr.FQDN.com;
    return 301 https://$host$request_uri;
}
 
server {
    listen 443 ssl http2;
    server_name logarr.FQDN.com;
 
    location / {
        proxy_pass http://10.0.0.11:4878/;
        add_header X-Frame-Options SAMEORIGIN;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    	}
}
</code></pre>