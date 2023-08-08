# Uptime Kuma for Laravel Forge using Traefik for routing

Uptime Kuma is an easy-to-use self-hosted monitoring tool.

See the [Uptime Kuma GitHub repo](https://github.com/louislam/uptime-kuma) for more information on the tool itself.

Here is a link to the Traefik repo used in conjunction with this repo:

https://github.com/johnfmorton/traefik-for-laravel-forge

## An accompanying blog post

There is a related blog post I wrote about using Traefik and Plausible Analytics on Laravel Forge. Reading that post will help you understand how this repo functions. [*Analytics a different way. Plausible Analytics on Laravel Forge with Traefik and Docker.*](https://supergeekery.com/blog/plausible-analytics-on-laravel-forge-with-traefik-and-docker)

## About this repo

The docker-compose.yml file in this repo is based on the the [Uptime Kuma Docker Compose example](https://github.com/louislam/uptime-kuma/blob/master/docker/docker-compose.yml) with a few changes to make it work with Laravel Forge and Traefik.

## Laravel Forge preparation

The repo assumes you have Docker installed already. See the [johnfmorton/traefik-for-laravel-forge repo](https://github.com/johnfmorton/traefik-for-laravel-forge#laravel-forge-preparation) for more information.

## DNS setup

You will need to set up DNS to point your domain name with an A record to your server you've created with Laravel Forge. For example, `uptime-kuma.yourdomain.com` should point to your server's IP address.

## Setting up the `.env` file

In the .env file, set `URL_FOR_TRAEFIK` to this domain name. For example, `uptime-kuma.yourdomain.com`. Don't include the protocol (http or https) or a trailing slash.

Use the [`example.env`](/example.env) for reference in setting up the additional environmental variables.


## Laravel Forge Deployment script

Here is a basic version of the deployment script.

```
cd /home/forge/analytics

git pull origin $FORGE_SITE_BRANCH

docker-compose -f docker-compose.yml -f reverse-proxy/traefik/docker-compose.traefik.yml up -d --remove-orphans
```

For a more complete version of the deployment script, see the [`forge-deployment-script.sh`](./forge-deployment-script.sh) file in this repo.

## License

The source code for the site is licensed under the MIT license, which you can find in
the MIT-LICENSE.txt file.
