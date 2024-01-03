# Private Docker Registry

This folder contains the infrastructure to run a private Docker registry, proxied through Nginx.

## Prerequisites

 - `docker`
 - `docker-compose`
 - `apache2-utils` (for `htpasswd`)

## Getting started

Create a username and password with:
```bash
htpasswd -Bc auth/registry.htpasswd [username]
```

With the `-B` flag a Bcrypt hash is made, which is required for Docker.

Now spin up the Docker composition with:
```bash
docker compose up
```

Add the `--build` flag to trigger the build for the webserver container explicitely.

## How to use

Now on the Docker client machine, run:

```bash
docker login http://[host] --username [username]
```

And enter the password you created before.
The login should be succesful now.

Now push and pull images like:
```bash
docker image tag [old_name]:[tag] [host]/[name]:[tag]
docker push [host]/[name]:[tag]
```

```bash
docker pull [host]/[name]:[tag]
```
