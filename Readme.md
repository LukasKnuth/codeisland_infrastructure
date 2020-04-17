# CodeIsland Docker Infrastructure

The container configuration for the CodeIsland server configuration via docker-compose.

## Preconditions

1. A Droplet running Docker (Easiest: [Official Docker Deployment](https://marketplace.digitalocean.com/apps/docker))
2. A Volume for storing persistent data
3. (Optional) Manage DNS through DigitalOcean (simple ACME via Traefik)

## Docker Machine

**Note:** While this is more convinient, it's not required. SSHing into the Droplet and using the local `docker` also works.

1. [Add your SSH key](https://cloud.digitalocean.com/account/security) to DigitalOcean
2. Create a new Droplet using the [Docker Solution](https://marketplace.digitalocean.com/apps/docker)
3. Find the IP address of the Droplet
4. Run the setup command for Docker Machine below:

	docker-machine create \
	    --driver generic \
	    --generic-ip-address=<droplet_ip> \
	    --generic-ssh-key <ssh-key> \
	    codeisland

**Every time** you want to connect, run `docker-machine env codeisland`, copy and execute the command in the shell. 

**Note:** This will connect _only_ the shell that the copied command is executed in! Another shell can be connected to another machine or the local Docker Desktop. Also, depending on the shell, the outputed command to connect is different. For example, the output from the default windows CMD will not work in the MySYS Git shell.

## Deploying

1. Rename `env.defaults` to `.env`
2. Replace values in `.env` with real-life values
3. Setup Docker-Machine or SSH into the Host running docker and copy over `docker-compose.yml`
4. Deploy the whole shabang with `docker-compose up -d`

## Check status

* Images on Server: `docker images`
* Running containers: `docker ps`
* Resource exhaustion: `docker stats`
