# Run Web page with self signed certificate behind HAProxy

## Description

Very simple & lightweight working solution shows how to serve web page with self signed sertificate handled by TLS1.2 protocol using HAProxy as a reverse proxy & docker-compose for building solution without docker swarm or kubernetes.

! It is not recommended to run in production mode pages which are not signed by trusted CA (see [letsencrypt](https://letsencrypt.org/) for free sertificates). This solution was created for very specific usecase.

## Modules

Solution consist of two docker containers:

* HAProxy configured for serve as reverse proxy
* WEB app (index.html as example) based on node:alpine & http-server

## Pre-requisites

Basic understanding of docker, docker-compose, HTTP, git & linux shell  

Linux server (tested on ubuntu 18.04) with installed:

* Docker (tested on Docker version 18.06.1-ce)
* Docker compose (tested on docker-compose version 1.23.0-rc3)
* openssl

### Known issue

App remains available on 8080 without HTTPS. It is possible to block port 8080 on host, but in case you know more elegant solution how to fix it - please create pull request.

## Create Self Signed certificate

```shell
sudo su
cd HAProxy
mkdir certs && cd certs
openssl genrsa -out proxytst.key 1024
sudo openssl req -new -key proxytst.key \
                   -out proxytst.csr
openssl x509 -req -days 365 -in proxytst.csr \
                    -signkey proxytst.key \
                    -out proxytst.crt
sudo cat proxytst.crt proxytst.key \
           | sudo tee proxytst.pem
```

## Run script

```shell
docker-compose up
```