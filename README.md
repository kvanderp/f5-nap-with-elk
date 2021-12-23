# All in one NGINX App Protect with an ELK stack

Make SURE to update docker-compose to version 1.28.5 or higher

Forked from <https://github.com/464d41/f5-waf-elk-dashboards>

Option of either:
a simple site that returns a few NGINX variables if the WAF doesn't block the request
or
nginx reverse proxy to the juice shop intentionally insecure app.

Site runs on :80 (443 not used in this example, yet)
Kibana listens on :81


## Deploying

You will likely need to increase memory to docker:

```
echo "vm.max_map_count=262144" | sudo tee -a /etc/sysctl.conf
sudo sysctl -w vm.max_map_count=262144
```

On WSL, run this (thanks @gallarda!)

```
wsl -d docker-desktop sysctl -w vm.max_map_count=262144
```

Add your nginx-repo.crt and nginx-repo.key to the ssl (with the your-cert-go-here) directory

### Build the nginx app protect container for the simple site

```
docker-compose -f docker-compose-simple-site.yaml up
```

### OR build the nginx app protect container and start the juice shop

```
docker-compose -f docker-compose-juice-shop.yaml up
```

### Access the demo

- The site you are protecting will be availible on host:80
- Kibana will take a minute to spin up, then availible on host:81
- NGINX Plus dashboard is availible on host:8080
- Once Kibana is up, import the dashboards (note that jq is required):

```
sh kibana-dashboards-import.sh
```

### Simple test on juice shop

Navigate to the juice shop login page that is not protected on :3000 and use ' as the username with any password, then try it on :80 and note that the request it blocked by the WAF.
