# reggie - A Python Registrator clone

Reggie is a simple Docker service bridge for Consul, similar to [Registrator](https://github.com/gliderlabs/registrator).  It dynamically adds and removes Consul services provided by Docker containers based on Docker events.  It also stores config information in Consul's K/V store for basic outage recovery.

This project primarily aimed at teaching meself Python (and the code quality reflects it), so do not rely on it for any kind of production use.

## Running reggie
```sh
usage: reggie [-h] [-i ifname] [-c host:port] [-d endpoint] [--use-docker-ip]

Update Consul catalog with Docker containers

optional arguments:
  -h, --help       show this help message and exit
  -i ifname        Network interface
  -c host:port     Consul endpoint
  -d endpoint      Docker endpoint
  --use-docker-ip  Use Docker IP for service registration
```

When reggie starts it attempts to update Consul with the currently running containers and clean up any stale containers.  As containers are started or stopped, reggie will add or remove their services based on the container's `SERVICE_NAME` and `SERVICE_PORT` environment variables