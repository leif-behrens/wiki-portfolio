---
title: Setup
description: 
published: true
date: 2025-06-19T10:16:26.021Z
tags: 
editor: markdown
dateCreated: 2025-06-19T09:59:21.340Z
---

# Running Wiki.js Locally in Docker on Raspberry Pi

I wanted to run Wiki.js inside a Docker container. For the setup, I followed the [official Wiki.js Docker installation guide](https://docs.requarks.io/install/docker).

---
<br>

## Setting Up the Raspberry Pi

Docker was already installed on my Raspberry Pi from a previous project where I ran MISP. At that time, I had created a dedicated **docker** user under which my containers now run.  
I created a new directory `/home/docker/wikijs-docker` to host the Wiki.js setup.
<br>

## Setting Up Docker Compose

To manage the application cleanly and handle the database connection, I used Docker Compose.  
I created a `docker-compose.yml` file, copied the template from the official Wiki.js docs, and adjusted a few parameters.

By default, the example configuration contains hardcoded credentials. I moved those into a `.env` file, changed the values and referenced them via `${VARIABLE}` syntax inside the Compose file.  
I also changed the exposed port from `80:3000` to `3000:3000`, since port 80 was already in use on the Raspberry Pi.

```yaml
services:

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_USER: ${POSTGRES_USER}
    logging:
      driver: none
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: ghcr.io/requarks/wiki:2
    depends_on:
      - db
    environment:
      DB_TYPE: ${DB_TYPE}
      DB_HOST: ${DB_HOST}
      DB_PORT: ${DB_PORT}
      DB_USER: ${DB_USER}
      DB_PASS: ${DB_PASS}
      DB_NAME: ${DB_NAME}
    restart: unless-stopped
    ports:
      - "3000:3000"

volumes:
  db-data:
```

I pulled the images with `docker compose pull` and tried starting the stack with `docker compose up -d`, but encountered errors (unfortunately I didn’t save the exact message).
To narrow it down, I temporarily switched back to the default compose file using the example credentials — only changing the port — and that worked.

This indicated that something went wrong with passing environment variables from the `.env` file.
The passwords I had used were long and contained lots of special characters, which I suspected might be the problem. Using `docker compose config`, I noticed that some characters might have been improperly escaped.
After simplifying the passwords, the error persisted, this time pointing to a database connection failure.

I realized that I might have created a persistent volume with invalid database credentials during one of the first runs.
To reset everything, I removed the volumes and images and started fresh:

```bash
# Clean up containers, volumes, and images
docker compose down -v --remove-orphans
docker rmi ghcr.io/requarks/wiki:2
docker rmi postgres:15-alpine

# Pull fresh images and restart
docker compose pull
docker compose up -d

# Follow logs to verify startup
docker compose logs -f wiki
```

This time it worked. I could access the Wiki via my browser. However, as I navigated through the interface, I repeatedly received the following error:

![an_unexpected_error_occured.png](/services/wikijs/an_unexpected_error_occured.png)

I looked up this error but couldn't get any good insights. Using Firefox developer tools, I noticed that Wiki.js was trying to connect to external resources. I checked online what kind of external resources these are and it seems like it was trying to get different language packages. I suspected a DNS resolution issue inside the container. I verified this with:

```bash
docker exec -it 7d0c96dc3a76 ping google.com	# No response
docker exec -it 7d0c96dc3a76 ping 8.8.8.8			# Successful response
```

So the container could reach the internet by IP, but not by domain name. I found the issue and just had to let my Wiki.js container know, what DNS server it should use. 

I researched how to let my container know the DNS and I found two options:
- Specify DNS server(s) in the docker-compose.yml file (per container)
- Configure DNS globally for all containers via Docker daemon settings

I chose the global approach since I already have a central DNS server (Pi-hole) on the same Raspberry Pi.

I created `/etc/docker/daemon.json` with the following content:

```json
{
        "dns": ["192.168.178.40", "192.168.178.1", "8.8.8.8"]
}
```

192.168.178.40 is my Raspberry Pi. As a backout DNS server I used my home router (192.168.178.1) and the google DNS server.

Then I restarted the Docker service:

`sudo systemctl restart docker`

After that, everything worked as expected.