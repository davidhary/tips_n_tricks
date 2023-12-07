# Unifi AP controller

## From version 8

### Create docker network for unifi
```bash
docker network create unifi
```

### MongoDB for Unifi controller
Create the init file `init-mongo.js`:
```
db.getSiblingDB("unifi").createUser({user: "unifi", pwd: "S0me-n1ce-Lo00ong-strong-PassW0rd", roles: [{role: "readWrite", db: "unifi"}]});
db.getSiblingDB("unifi_stat").createUser({user: "unifi", pwd: "S0me-n1ce-Lo00ong-strong-PassW0rd", roles: [{role: "readWrite", db: "unifi_stat"}]});
```

```bash
docker volume create unifi-mongo-data

docker run -dit --name unifi-mongo \
--network unifi \
-e PUID=1000 \
-e GUID=1000 \
-v ${PWD}/init-mongo.js:/docker-entrypoint-initdb.d/init-mongo.js:ro \
-v unifi-mongo-data:/data \
--restart unless-stopped \
mongo:7.0.3
```

### Container
```bash
docker volume create unifi-8-config

docker run -dit --name unifi-8 \
--network unifi \
-e PUID=1000 \
-e GUID=1000 \
-e TZ=Europe/Budapest \
-e MONGO_USER=unifi \
-e MONGO_PASS=S0me-n1ce-Lo00ong-strong-PassW0rd \
-e MONGO_HOST=unifi-mongo \
-e MONGO_PORT=27017 \
-e MONGO_DBNAME=unifi \
-e MEM_LIMIT=1024 \
-e MEM_STARTUP=1024 \
-v unifi-8-config:/config \
-p 8443:8443 \
-p 8080:8080 \
--restart unless-stopped \
lscr.io/linuxserver/unifi-network-application:8.0.7
```

### nginx virtual host settings

```
location / {
    proxy_pass https://127.0.0.1:8443;
    proxy_ssl_verify off;
    proxy_ssl_session_reuse on;
    proxy_buffering off;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_hide_header Authorization;
    proxy_set_header Referer '';
    proxy_set_header Origin '';
}

location /inform {
    proxy_pass http://127.0.0.1:8080;
    proxy_ssl_verify off;
    proxy_ssl_session_reuse on;
    proxy_buffering off;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_hide_header Authorization;
    proxy_set_header Referer '';
    proxy_set_header Origin '';
}

location /wss {
    proxy_pass https://127.0.0.1:8443;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Origin '';
    proxy_buffering off;
    proxy_hide_header Authorization;
    proxy_set_header Referer '';
}
```

---

## Version 7 (depracted since 2024.01.01.)
```bash
docker volume create controller-7-config

docker run -d \
  --name=unifi-controller7 \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/Budapest \
  -e MEM_LIMIT=1024 \
  -e MEM_STARTUP=1024 \
  -p 9443:8443 \
  -p 9080:8080 \
  -v controller-7-config:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/unifi-controller:7.5.187
```
