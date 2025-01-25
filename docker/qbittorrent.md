# Qbittorrent - torrent client

## Docker hub
https://hub.docker.com/r/linuxserver/qbittorrent

## compose
```yaml
services:
  qbittorrent:
    image: lscr.io/linuxserver/qbittorrent:5.0.3
    container_name: qbittorrent
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Budapest
      - WEBUI_PORT=8080
      - TORRENTING_PORT=6881
    volumes:
      - ${PWD}/appdata:/config
      - /torrent:/downloads
    ports:
      - 8080:8080
      - 6881:6881
      - 6881:6881/udp
    restart: unless-stopped
```
