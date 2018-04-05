---
title: Encoding
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

Once we have the content on the machine ready to manipulate, we will describe the process of encoding the files from its raw format into a packaged format, in both "Remux" format and encoded. While a Remux is technically a package of the original stream it still uses the same encoding applications so will generally be considered a similar process. For the encoding process... While you are able to manipulate the files a little further, we will only cover our "recommended" quality settings at each stage. We will also not be giving out any time frame on how long this takes as it heavily depends on the level of encoding and the power of the machine doing it. 

## Video Media

### 4K

#### Remux

#### H.265 Encode

### 1080p

#### Remux

```bash
makemkvcon mkv file:~/movie 0 .
```

or

```bash
mkvmerge -o output.mkv input.m2ts
```

#### H.264 Encode
```bash

# Extract files from decrypted bluray backup
ffmpeg -i ~/movie/BDMV/STREAM/00002.m2ts -vcodec copy -an film.m4v
ffmpeg -i ~/movie/BDMV/STREAM/00002.m2ts -acodec copy -vn film.dts

# Encode Elements
x264 --crf 19 --preset veryslow -o film.mp4 film.m4v

```

### 720p

### 560p

### 480p


## Audio Media

### FLAC

### AAC

### MP3