# Qbittorrent - torrent client

## Docker hub
https://hub.docker.com/r/linuxserver/qbittorrent

## Container
```bash
docker run -d \
--name=qbittorrent \
-e PUID=1000 \
-e PGID=1000 \
-e TZ=Europe/Budapest \
-e WEBUI_PORT=9091 \
-p 9091:9091 \
-p 40640:6881 \
-p 40640:6881/udp \
-v /data/docker-volumes/qbittorrent:/config \
-v /data/torrent:/downloads \
--restart unless-stopped \
lscr.io/linuxserver/qbittorrent:4.6.2-libtorrentv1
```
