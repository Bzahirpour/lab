Version 1

```yaml
redis: #name of container
	image: redis
db:
	image: postgres:9.4 #key is image, value is image to use
vote:
	image: voting-app
	build: ./vote #if you want to build a local image instead of getting from repo
	ports:
		- 5000:80 #host:cont
	links: # NO LONGER NEEDED in modern Docker Compose (v2+), services on the same network can automatically reach each other using their service name as the hostname without needing explicit links.
		- redis #name of the existing container OR db:db existingname:alias	

```

Version 2

```yaml
version: 2 #you must now include the version at the top of the file
services: #all servies now go under the services block
	redis: #name of container
		image: redis
		networks:
				- back-end
	db:
		image: postgres:9.4 #key is image, value is image to use
		networks:
				- back-end
	vote:
		image: voting-app
		build: ./vote #if you want to build a local image instead of getting from repo
		ports:
			- 5000:80 #host:cont
		depends_on: #added in version 2
			-redis
		networks:
				- front-end
				- back-end
			
	
	networks: #include a networks block in the root of the file, then list them in the services
			front-end:
			back-end: 
```

Version 3 supports docker swarm
```yaml
version: 3 #you must now include the version at the top of the file
services: #all servies now go under the services block
	redis: #name of container
		image: redis
	db:
		image: postgres:9.4 #key is image, value is image to use
	vote:
		image: voting-app
		build: ./vote #if you want to build a local image instead of getting from repo
		ports:
			- 5000:80 #host:cont
		depends_on: #added in version 2
			-redis
```