# Zerops x Filament - production setup

WORK IN PROGRESS - development enviroment

[Filament](https://filamentphp.com) is a collection of beautiful full-stack components. This recipe showcasing how to run production version in Zerops. It's based on [Filament Demo](https://github.com/filamentphp/demo) and 
icludes all the advanced functionality — session and cache
stored in Redis and files stored in Object Storage, this makes it perfectly suitable for production of any size.

<br/>

## Deploy on Zerops

You can either click the deploy button to deploy directly on Zerops, or manually copy
the [import yaml](https://github.com/zeropsio/recipe-laravel-jetstream/blob/main/zerops-project-import.yml) to the
import dialog in the Zerops app.

[![Deploy on Zerops](https://github.com/zeropsio/recipe-shared-assets/blob/main/deploy-button/green/deploy-button.svg)](https://app.zerops.io/recipe/laravel)

<br/>

## Recipe features

- Filament running on a load balanced **Zerops PHP + Nginx** service
- Zerops **PostgreSQL 16** service as database
- Zerops KeyDB (**Redis**) service for session and cache
- Zerops **Object Storage** (S3 compatible) service as file system
- Proper setup for Laravel **cache**, **optimization**, and **database migrations**
- Logs set up to use **syslog** and accessible through Zerops GUI
- Utilization of Zerops built-in **environment variables** system
- Utilization of Zerops readiness check for proper  **Zero downtime deployment**
- Utilization of Zerops health check for advanced  **app monitoring**
- [Mailpit](https://github.com/axllent/mailpit) as **SMTP mock server**
- [Adminer](https://www.adminer.org) for **quick database management** tool
- [S3browser](https://github.com/zeropsio/s3browser) for **quick S3 storage** testing and browsing

<br/>

## Production vs. development

Base of the recipe is for development purpose. For production environment setup check [Filament production setup](https://github.com/zeropsio/recipe-filament/tree/main)

[//]: # (- Use highly available version of the PostgreSQL database &#40;change `mode` from `NON_HA` to `HA` in recipe YAML, `db`)

[//]: # (  service section&#41;)

[//]: # (- Use at least two containers for Jetstream service to achieve high reliability and resilience &#40;add `minContainers: 2`)

[//]: # (  in recipe YAML, `app` service section&#41;)

[//]: # (- Use production-ready third-party SMTP server instead of Mailpit &#40;change `MAIL_` secret variables in recipe YAML `app`)

[//]: # (  service&#41;)

[//]: # (- Disable public access to Adminer or remove it altogether &#40;remove service `adminer` from recipe YAML&#41;)

<br/>

## Changes made over the default installation

If you want to modify your existing Filament app to efficiently run on Zerops, these are the general steps we
took:

- Add [zerops.yml](https://github.com/zeropsio/recipe-filament/blob/main/zerops.yml) to your repository, our
  example includes idempotent migrations, caching, and optimized build process
- Add [league/flysystem-aws-s3-v3](https://github.com/zeropsio/recipe-filament/blob/main/composer.json#L23) to
  your composer.json to support Object Storage file system
- Setup health check if needed. Health checks are enabled out of the box in Laravel 11.
- Utilize
  Zerops [environment variables](https://github.com/zeropsio/recipe-filament/blob/main/zerops.yml#L22-L73)
  and [secrets](https://github.com/zeropsio/recipe-filament/blob/main/zerops-project-import.yml#L13-L14) to
  setup S3 for file system, Redis for cache and sessions, and trusted proxies to work with reverse proxy load balancer

<br/>
<br/>

Need help setting your project up? Join [Zerops Discord community](https://discord.com/invite/WDvCZ54).
