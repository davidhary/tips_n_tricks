 ```bash
echo '/etc/docker/daemon.json' >> { "registry-mirrors": ["https://mirror.gcr.io"] }
systemctl restart docker
docker info
```
