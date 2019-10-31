# Nginx reverse proxy and auto tls certificates

An simple approach to start a reverse proxy, with auto generated TSL certificates using docker to automate
and simplify the deployment and configuration. With this configuration it will be possible
to run multiple websites on a single vpn with minimal configuration effort.

## Table of Contents

- [Getting started](#getting-started)
  - [1. Start reverse proxy](#1-start-reverse-proxy)
  - [2. Start website](#2-start-website)
- [Information](#information)
- [File Structure](#file-structure)
- [Reference](#references)

## Getting Started

### 1. Start reverse proxy

- Create the network for nginx proxy container:  
  `$ docker network create nginx-proxy-net`
- Rename the `.env.example` to .env and edit it. Set all environment variables
- Start the nginx proxy container with following command:  
  `$ docker-compose up -d`

### 2. Start website

- Start your static web site nginx container :  
  `$ docker-compose up -d`

## Information

## File structure

## References

Build with:

- [GitHub: jwilder/nginx-proxy][link-ref-ngx] - Automated nginx proxy for Docker containers using docker-gen
- [GitHub: JrCs/docker-letsencrypt-nginx-proxy-companion][link-ref-tls] - LetsEncrypt companion container for nginx-proxy
- [Docker Hub: jwilder][link-ref-dnx] - Images for jwilder/nginx-proxy
- [Docker Hub: JrCs][link-ref-dls] - Images for JrCs/docker-letsencrypt-nginx-proxy-companion

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

[link-ref-ngx]:     https://github.com/jwilder/nginx-proxy
[link-ref-tls]:     https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion
[link-ref-dnx]:     https://hub.docker.com/r/jwilder/nginx-proxy
[link-ref-dls]:     https://hub.docker.com/r/jrcs/letsencrypt-nginx-proxy-companion