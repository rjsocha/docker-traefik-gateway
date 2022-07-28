
Traefik gateway for docker(-compose) services.

## Info

Do not start both instances (vpn, public) from same project directory...


## Start
```
	git clone https://github.com/rjsocha/docker-traefik-gateway.git
	cd docker-traefik-gateway
	docker-compose up -d
```

## Verification
```
	docker network ls -f "name=service-gateway" --no-trunc
	docker ps -f "name=traefik-docker-gateway" --no-trunc
	docker logs traefik-docker-gateway
```

## Examples 
Example (hello.domain.example is example domain - make sure to point your DNS to the gateway):

```
docker-compose -p example -f examples/example.yml up -d
docker-compose -p example -f examples/example.yml down

curl -v 127.0.0.1
curl -v -H "Host: hello.example.com" 127.0.0.1

```
