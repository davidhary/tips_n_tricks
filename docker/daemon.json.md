 ```bash
echo '{ "registry-mirrors": ["https://mirror.gcr.io"] }' >> /etc/docker/daemon.json
systemctl restart docker
docker info
```
