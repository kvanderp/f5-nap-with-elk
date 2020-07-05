# All in one NGINX App Protect with an ELK stack

Forked from <https://github.com/464d41/f5-waf-elk-dashboards>

Option of either:
a simple site that returns a few NGINX variables if the WAF doesn't block the request
or
nginx reverse proxy to the juice shop waf testing tool

Site runs on :80 (443 not used in this example, yet)
Kibana listens on :81

## Deployingment

You will likely need to increase memory to docker:

```
echo "vm.max_map_count=262144" | sudo tee -a /etc/sysctl.conf
sudo sysctl -w vm.max_map_count=262144
```

We use a shared docker network for the conainers, you'll need to create it:

```
docker network create shared-net
```

### Build the nginx app protect container for the simple site

Add your nginx-repo.crt and nginx-repo.key to the ssl directory then:

```
docker build --tag=nap -f Dockerfile.simple-site .
```

### OR build the nginx app protect container and start the juice shop

Add your nginx-repo.crt and nginx-repo.key to the ssl directory then:

```
docker build --tag=nap -f Dockerfile.juice-shop .
docker run -d -p 3000:3000 --network=shared-net --name=juice-shop bkimminich/juice-shop
```

### Bring up the stack

```
docker-compose -f docker-compose.yaml up -d
```
