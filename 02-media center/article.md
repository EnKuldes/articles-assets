
# Media Server Setup using **Jellyfin**+**Jellyseer** & Download tools

## What is Media Server

As I quote from Wikipedia "A **media server** is a [computer appliance](https://en.wikipedia.org/wiki/Computer_appliance "Computer appliance") or an [application software](https://en.wikipedia.org/wiki/Application_software "Application software") that stores [digital media](https://en.wikipedia.org/wiki/Digital_media "Digital media") (video, audio or images) and makes it available over a network.". In more simpler way version of mine, a **media server** mean an app that can be accessed via network to play movies, images or any stored digital media.

Media server have a lot of options to choose, from Plex, Kodi, etc. But the one im choosing is Jellyfin. Why Jellyfin? Because its open source and free from ads. Before im choosing Jellyfin, I try using Plex, its a good media server, theres a lot of feature in it such as online connectivity with public, but there is one thing I didnt like, that is ads. I dont want to watch my own self hosted video while ads showing on my login page, while im watching the movies. That one things making me run from Plex, and I found Jellyfin. This is the new upcoming media server released on 2018 have a lot of things going on and good support/documentation. Other reason is also because I dont have any intention of make my media server be accessible from outside my LAN network so its better to use Jellyfin with its simple configuration.

I also will add Jellyseer as a plugin for Jellyfin. Jellyseer will be media request management which user on jellyfin can request what movies/animes/series they want to watch. Jellyseer also can be integrated with other \*Arr app but I havent configure it. As for now Jellyseer will be used to manage request.

## Installing Jellyfin & Jellyseer

To install both these apps im gonna use Docker or more specificaly docker-compose. Here are my directory tree

```
📦 Home Lab
├─ jellyfin
│  ├─ docker-compose.yml
│  └─ README.md
└─ jellyseer
   └─ docker-compose.yml
```

Below are snippets of docker-compose for each jellyfin and jellyseer folder:

- Jellyfin docker compose

```
version: "3"
services:
  jellyfin:
    image: lscr.io/linuxserver/jellyfin:latest
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Jakarta
    volumes:
      - ${JELLYFIN_LIBRARY}:/config
      - ${JELLYFIN_TV_SERIES}:/data/tvshows
      - ${JELLYFIN_MOVIES}:/data/movies
      - ${JELLYFIN_ANIME}:/data/anime
    ports:
      - 8096:8096
      #- 8920:8920 #optional
      #- 7359:7359/udp #optional
      #- 1900:1900/udp #optional
    restart: unless-stopped

```

- Jellyseer docker compose

```
version: '3'
services:
  jellyseerr:
    image: fallenbagel/jellyseerr:latest
    container_name: jellyseerr
    environment:
      - LOG_LEVEL=debug
      - TZ=Asia/Jakarta
      # - PORT=5055 #optional
    ports:
      - 5055:5055
    volumes:
      - ./config:/app/config
    restart: unless-stopped
```