# All in one NGINX App Protect with an ELK stack
Forked from <https://github.com/464d41/f5-waf-elk-dashboards>

## Quick Start
### Deploying ELK Stack

You will likely need to increate memory to docker:
```
echo "vm.max_map_count=262144" | sudo tee -a /etc/sysctl.conf
sudo sysctl -w vm.max_map_count=262144
```

Use docker-compose to deploy your own ELK stack.
```
$ docker-compose -f docker-compose.yaml up -d
```
