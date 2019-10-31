# Nginx reverse proxy with auto tls certificates

[ ![shield-version] ][link-ghb-rep]
[ ![shield-issues] ][link-ghb-iss]
[ ![shield-license] ][link-ghb-lcs]

An simple approach to start a reverse proxy, with auto generated TSL certificates using docker to automate  
and simplify the deployment and configuration. With this configuration it will be possible to run multiple  
websites on a single vpn with minimal configuration effort.

## Table of Contents

- [Getting started](#getting-started)
  - [1. Install docker](#1-install-docker)
  - [2. Start reverse proxy and website](#2-start-reverse-proxy-and-website)
- [Additional info](#additional-info)
- [File Structure](#file-structure)
- [Reference](#references)

## Getting Started

### 1. Install docker

- Install [docker][link-ref-dok] and [docker-compose][link-ref-dkc] on your server
- Clone this repository `$ git clone git@github.com:tikkerei/docker-nginx-proxy-tls.git`

### 2. Start reverse proxy and website

- Create the network for nginx proxy container:  
  `$ docker network create nginx-proxy-net`
- Rename the `.env.example` to `.env` edit it and set environment variables.

  ```bash
  ### One liner, change directory copy .env and edit it
  $ cd docker-nginx-proxy-tls && cp .env.example .env && nano .env
  ### Following variables in .env file MUST be changed
  DOMAIN=website.tld
  EMAIL=your@mail.com
  ```

- Start the nginx proxy container with following command:  
  `$ docker-compose up -d`
- Start your static web site nginx container :  
  `$ docker-compose -f docker-compose.web.yml up -d`

Put your website into /www/website.tld/ folder.  
That's it.

## Additional info

All generated certificates and nginx configuration will be stored is ./nginx-data,  
if not changed in .env. The docker compose will create the folder automatically on first start.  
If you want to add custom nginx configuration to the repository  
don't forget to remove `./nginx-data/` line from the .gitignore file.

### Useful commands

Check docker compose configuration file:  
`$ docker-compose -f <docker-compose.web.yml> config`

Show running containers:  
`$ docker ps`

Show container logs:  
`$ docker logs <nginx-proxy>`

Stop container:  
`$ docker stop <container id>`

Remove all UNUSED containers, networks, images:  
`$ docker system prune`

WARNING! Remove ALL containers, networks, images, volumes:  
`$ docker system prune -a`

## File structure

```bash
.                           # This repository
├── nginx-data/             # Will be created on first start, nginx config files
├── www/website.tld/        # Will be created on first start, place for your website
├── .env.example            # Should be renamed to .env, environment variables
├── .gitignore              # List of git ignored files and directories
├── LICENSE                 # Licence agreement
├── README.md               # This README.md file
├── docker-compose.web.yml  # Docker compose file for nginx proxy and letsencrypt container
└── docker-compose.yml      # Docker compose file for your website
```

## References

Build with:

- [GitHub: jwilder/nginx-proxy][link-ref-ngx] - Automated nginx proxy for Docker containers using docker-gen
- [GitHub: JrCs/docker-letsencrypt-nginx-proxy-companion][link-ref-tls] - LetsEncrypt companion container for nginx-proxy
- [Docker Hub: jwilder][link-ref-dnx] - Images for jwilder/nginx-proxy
- [Docker Hub: JrCs][link-ref-dls] - Images for JrCs/docker-letsencrypt-nginx-proxy-companion

Docs:

- [Docker install docs][link-ref-dok]
- [Docker compose install docs][link-ref-dkc]

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

[link-ref-ngx]:     https://github.com/jwilder/nginx-proxy
[link-ref-tls]:     https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion
[link-ref-dnx]:     https://hub.docker.com/r/jwilder/nginx-proxy
[link-ref-dls]:     https://hub.docker.com/r/jrcs/letsencrypt-nginx-proxy-companion
[link-ref-dok]:     https://docs.docker.com/install/linux/docker-ce/ubuntu/
[link-ref-dkc]:     https://docs.docker.com/compose/install/
[link-ghb-rep]:     https://github.com/tikkerei/docker-nginx-proxy-tls
[link-ghb-iss]:     https://github.com/tikkerei/docker-nginx-proxy-tls/issues
[link-ghb-lcs]:     https://github.com/tikkerei/docker-nginx-proxy-tls/blob/master/LICENSE

[shield-version]:   https://img.shields.io/github/v/release/tikkerei/docker-nginx-proxy-tls
[shield-issues]:    https://img.shields.io/github/issues/tikkerei/docker-nginx-proxy-tls
[shield-license]:   https://img.shields.io/github/license/tikkerei/docker-nginx-proxy-tls