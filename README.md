# micro-stack-traefik-v2

This microservice stak demostrates how to use the Traefik-v2 to secure the self-hosted web apps by enabling the https protocol with them (a whoami app & a wordpress site as the examples here). The stack is configured to use the dummy certificate for doamin "example.com" by account "tester<span>@</span>gmail.com". In practical use, you need to apply a certificate for your domain and update the "certificatesresolvers" section of the traefik config yaml file accordingly (line 31-33 in example here).

## A. Prerequirments

### 1. Docker-desktop

This demo needs the Docker-Desktop and Docker-Compose to run it. Install them if not yet.

### 2. Domain names are locally resolvable

#### a. Append the names to OS hosts

```code
...
<!-- 127.0.0.1   example.com -->
127.0.0.1   www.example.com
127.0.0.1   whoami.example.com
127.0.0.1   dashboard.example.com
```

#### b. Create nmae records in a local DNS

Config a local DNS server like Pi-hole & add A recored or CNAMEs to resolve
```
<!-- example.com -->
www.example.com
whoami.example.com
dashbaord.example.com
```

#### c. Check the domain name resolvers

```
ping w<span>ww.</span>.example.com
ping whoami.example.com
ping dashboard.example.com
```

> Pinging w<span>ww.</span>.example.com [127.0.0.1] with 32 bytes of data:
> Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> ...
> 
> Pinging whoami.example.com [127.0.0.1] with 32 bytes of data:
>  Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
>  Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> ...
> 
> Pinging dashboard.example.com [127.0.0.1] with 32 bytes of data:
> Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> Reply from 127.0.0.1: bytes=32 time<1ms TTL=128
> ...
> 

## B. Preparation

### 1. Create docker networks
```bash
docker network prune
```
```bash
docker network create micro-v2-net-front
docker network create micro-v2-net-back
```
### 2. Creater docker volumes
```bash
docker volume create micro-v2-wp-vol
docker volume create micro-v2-db-vol
```
### 3. Spin up the containers
```bash
docker compose up -d
```

## C. Validate the stack funtions

### 1. Check the WhoAmI app

```
http://whoami.example.com
```

### 1. Check the Wordpress website

```
http://www.example.com
```

### 2. Check the Traefik dashboard

```
http://dashboard.example.com
```
