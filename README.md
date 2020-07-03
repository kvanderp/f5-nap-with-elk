# All in one NGINX App Protect with an ELK stack
Forked from <https://github.com/464d41/f5-waf-elk-dashboards>

Site runs on :80 (443 not used in this example, yet)
Kibana listens on :81

## Quick Start
### Deploying ELK Stack

You will likely need to increate memory to docker:
```
echo "vm.max_map_count=262144" | sudo tee -a /etc/sysctl.conf
sudo sysctl -w vm.max_map_count=262144
```

### Build the nginx app protect container
add your nginx-repo.crt and nginx-repo.key to the ssl directory then:
```
docker build --tag=nap .
```

### Bring up the entire stack:
```
$ docker-compose -f docker-compose.yaml up -d
```
