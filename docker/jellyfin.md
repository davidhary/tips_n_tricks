# Jellyfin media center
## Docker Hub
https://hub.docker.com/r/linuxserver/jellyfin

## Volumes
docker volume create jellyfin-data
docker volume create jellyfin-config

## Container
docker run -d \
  --name=jellyfin \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/Budapest \
  -p 8096:8096 \
  -p 8920:8920 \
  -p 7359:7359/udp \
  --device=/dev/dri:/dev/dri \ # ONLY NEED ON BARE METAL HOST, OR DEDICATED VGA
  -v jellyfin-config:/config \
  -v jellyfin-data:/data/ \
  --restart unless-stopped \
lscr.io/linuxserver/jellyfin:latest
