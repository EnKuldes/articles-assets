
# Media Server Setup using **Jellyfin**+**Jellyseer** & Download tools

## What is Media Server

As I quote from Wikipedia "A **media server** is a [computer appliance](https://en.wikipedia.org/wiki/Computer_appliance "Computer appliance") or an [application software](https://en.wikipedia.org/wiki/Application_software "Application software") that stores [digital media](https://en.wikipedia.org/wiki/Digital_media "Digital media") (video, audio or images) and makes it available over a network.". In more simpler way version of mine, a **media server** mean an app that can be accessed via network to play movies, images or any stored digital media.

Media server have a lot of options to choose, from Plex, Kodi, etc. But the one im choosing is Jellyfin. Why Jellyfin? Because its open source and free from ads. Before im choosing Jellyfin, I try using Plex, its a good media server, theres a lot of feature in it such as online connectivity with public, but there is one thing I didnt like, that is ads. I dont want to watch my own self hosted video while ads showing on my login page, while im watching the movies. That one things making me run from Plex, and I found Jellyfin. This is the new upcoming media server released on 2018 have a lot of things going on and good support/documentation. Other reason is also because I dont have any intention of make my media server be accessible from outside my LAN network so its better to use Jellyfin with its simple configuration.

I also will add Jellyseer as a plugin for Jellyfin. Jellyseer will be media request management which user on jellyfin can request what movies/animes/series they want to watch. Jellyseer also can be integrated with other \*Arr app but I havent configure it. As for now Jellyseer will be used to manage request.

## Installing Jellyfin & Jellyseer

To install both these apps im gonna use Docker or more specificaly docker-compose. Here are my directory tree:

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
    ports:
      - 5055:5055
    volumes:
      - ./config:/app/config
    restart: unless-stopped
```

Here are few explaination regarding my snippets.


- PUID and GUID are user and group identifiers, this useful because sometimes we got an permission issue between our host and container when we are using Docker Volume. By default the value is `1000`, but you can reconfirm it on your terminal by running this 

```
id your_user
```

For my case it's like this:

```
uid=1000(farhan) gid=1000(farhan) groups=1000(farhan)
```

- TZ basically a timezone setting.
- Volumes or Docker Volume are a way to store/read data outside the container. For example at Jellyseer snippet, I connect the data inside container of /app/data to host at jellyseer directory, if we put in tree view it would look like this after you successfully run the docker compose.

```
📦 Home Lab
└─ jellyseer
   └─ docker-compose.yml
   └─ config
   │  ├─ cache
   │  ├─ db
   │  ├─ logs
   └─ └─ setting.json
```

This also include the Jellfin snippets, the difference is on Jellyfin snippet I'm using enviroment variable. I set it up by adding it to all users on `/etc/enviroment`, below are my enviroment variables

```
JELLYFIN_LIBRARY="/home/homelab/jellyfin/config"
# Media Library Path here
JELLYFIN_TV_SERIES="/home/media-library/TV"
JELLYFIN_MOVIES="/home/media-library/Movies"
JELLYFIN_ANIME="/home/media-library/Anime"
```
With this being setup now every config/cache related to jellyfin will be stored inside my host `/home/homelab/jellyfin/config` path, while my media is being readed by jellyfin based on those paths.

- Ports are mapper between host and container, in this case I use default port of 8096 and 5055.

Now let's run the container, we can run it using docker compose command by access its directory

```
# incase there is warning when running it, its probably because the enviroment variables is not refreshed, can be fix it by relogin your SSH/telnet or entering and exiting root
docker compose up -d
# or
sudo docker compose up -d
```

It will building and you can see the progress by doing this command

```
# remove -f if dont wanna tailing the output
docker logs -f (container_name)
# for jellyfin
docker logs -f jellyfin
# for jellyseer
docker logs -f jellyseerr
```

After building is done, I can access it through my IP and port which is

- 192.168.1.97:8096 for Jellyfin
- 192.168.1.97:5055 for Jellyseerr