# CI/CD local setup

## Goal

To create usable local installation of CI/CD toolset, using Docker and docker-compose.

## Elements

This repository contains `docker-compose.yml`, which creates

* PostgreSQL database for SonarQube
* SonarQube
* Jenkins

Jenkins uses dockerized build nodes.

## Prerequisities

1. Docker and docker-compose must be installed.

2. SonarQube uses built-in ElastcSearch, and it requires changes in memory settings to grant enough space for creating indices by ES.

```bash
sudo sysctl -w vm.max_map_count=262144
```

In order to make changes permament, update `/etc/sysctl.conf`

3. Enable docker secrets in your environment

First, enable swarm mode

```bash
docker swarm init
```

Create secrets

```bash
echo "admin" | docker secret create jenkinspassword -
echo "jenkins" | docker secret create jenkinsnodepassword -

```

4. Allow Jenkins to connect to docker.sock on host

You can change permissions

```bash
sudo chmod o+rw /var/run/docker.sock
```

But this is a risky way. However, I didn't find better way using WSL2 on Windows.


## Use of dockerized build nodes

First, build the Dockerfile located in images/buildNodeDefault.