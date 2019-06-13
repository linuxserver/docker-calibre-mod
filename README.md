[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)](https://linuxserver.io)

The [LinuxServer.io](https://linuxserver.io) team brings you another container release featuring :-

 * regular and timely application updates
 * easy user mappings (PGID, PUID)
 * custom base image with s6 overlay
 * weekly base OS updates with common layers across the entire LinuxServer.io ecosystem to minimise space usage, down time and bandwidth
 * regular security updates

Find us at:
* [Discord](https://discord.gg/YWrKVTn) - realtime support / chat with the community and the team.
* [IRC](https://irc.linuxserver.io) - on freenode at `#linuxserver.io`. Our primary support channel is Discord.
* [Blog](https://blog.linuxserver.io) - all the things you can do with our containers including How-To guides, opinions and much more!

# [linuxserver/calibre-mod](https://github.com/linuxserver/docker-calibre-mod)
[![](https://img.shields.io/discord/354974912613449730.svg?logo=discord&label=LSIO%20Discord&style=flat-square)](https://discord.gg/YWrKVTn)
[![](https://images.microbadger.com/badges/version/linuxserver/calibre-mod.svg)](https://microbadger.com/images/linuxserver/calibre-mod "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/linuxserver/calibre-mod.svg)](https://microbadger.com/images/linuxserver/calibre-mod "Get your own version badge on microbadger.com")
![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/calibre-mod.svg)
![Docker Stars](https://img.shields.io/docker/stars/linuxserver/calibre-mod.svg)
[![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Pipeline-Builders/docker-calibre-mod/master)](https://ci.linuxserver.io/job/Docker-Pipeline-Builders/job/docker-calibre-mod/job/master/)
[![](https://lsio-ci.ams3.digitaloceanspaces.com/linuxserver/calibre-mod/latest/badge.svg)](https://lsio-ci.ams3.digitaloceanspaces.com/linuxserver/calibre-mod/latest/index.html)

[Calibre-mod](https://calibre-ebook.com/) **is not a standalone container** but an additional docker layer for the LinuxServer.io Calibre-Web container which adds the binaries and dependencies necessary to enable ebook conversion in Calibre-web on x86-64 utilising Calibre.


[![calibre-mod](https://github.com/kovidgoyal/calibre/raw/master/resources/images/lt.png)](https://calibre-ebook.com/)

## Supported Architectures

Our images support multiple architectures such as `x86-64`, `arm64` and `armhf`. We utilise the docker manifest for multi-platform awareness. More information is available from docker [here](https://github.com/docker/distribution/blob/master/docs/spec/manifest-v2-2.md#manifest-list) and our announcement [here](https://blog.linuxserver.io/2019/02/21/the-lsio-pipeline-project/). 

Simply pulling `linuxserver/calibre-web` should retrieve the correct image for your arch, but you can also pull specific arch images via tags.

The architectures supported by this image are:

| Architecture | Tag |
| :----: | --- |
| x86-64 | amd64-latest |


## Usage

Here are some example snippets to help you get started creating a Calibre-Web container utilising this mod.

### docker

```
docker create \
  --name=calibre-web \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/London \
  -e DOCKER_MODS=linuxserver/calibre-mod:latest \
  -p 8083:8083 \
  -v <path to data>:/config \
  -v <path to calibre library>:/books \
  --restart unless-stopped \
  linuxserver/calibre-web
```


### docker-compose

Compatible with docker-compose v2 schemas.

```
---
version: "2"
services:
  calibre-mod:
    image: linuxserver/calibre-web
    container_name: calibre-web
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - DOCKER_MODS=linuxserver/calibre-mod:latest
    volumes:
      - <path to data>:/config
      - <path to calibre library>:/books
    ports:
      - 8083:8083
    restart: unless-stopped
```

## Parameters

Container images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| :----: | --- |
| `-p 8083` | WebUI |
| `-e PUID=1000` | for UserID - see below for explanation |
| `-e PGID=1000` | for GroupID - see below for explanation |
| `-e TZ=Europe/London` | Specify a timezone to use EG Europe/London. |
| `-e DOCKER_MODS=linuxserver/calibre-mod:latest` | Adds the ability to convert books on x86-64 |
| `-v /config` | Where calibre-web stores the internal database and config. |
| `-v /books` | Where your calibre database is locate. |

## Application Setup

In the Calibre-Web admin page (Basic Configuration:External Binaries) set the path to converter tool to `/usr/bin/ebook-convert`

## Building locally

If you want to make local modifications to these images for development purposes or just to customize the logic: 
```
git clone https://github.com/linuxserver/docker-calibre-mod.git
cd docker-calibre-mod
docker build \
  --no-cache \
  --pull \
  -t linuxserver/calibre-mod:latest .
```
Once registered you can define the dockerfile to use with `-f Dockerfile.aarch64`.

## Versions

* **12.06.19:** - Initial release.
