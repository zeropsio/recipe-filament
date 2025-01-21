# Zerops x Filament

This repository demonstrates how to set up and deploy Filament applications using Zerops for both development and
production environments.

![FilamentZerops](https://github.com/zeropsio/recipe-shared-assets/blob/main/covers/svg/cover-filament.svg)

<br/>

[Filament](https://filamentphp.com) is a collection of beautiful full-stack components. This recipe showcases how to run
a Filament application on Zerops, including all advanced functionalities, with sessions and cache stored in Redis and
files stored in Object Storage, making it suitable for production of any size.

## Deploy on Zerops

You can either click the deploy button to deploy development setup directly on Zerops or manually copy
the [import yaml](https://github.com/zeropsio/recipe-filament/blob/main/zerops-project-import.yml) to the
import dialog in the Zerops app.

[![Deploy on Zerops](https://github.com/zeropsio/recipe-shared-assets/blob/main/deploy-button/green/deploy-button.svg)](https://app.zerops.io/recipe/filament-local)

<br/>

## Understand Zerops Core Concepts
If you want to try integrating Zerops from scratch on a new Laravel project, check our [step-by-step tutorial](https://docs.zerops.io/frameworks/laravel/introduction) which demonstrates how to use Zerops effectively with Laravel.

<br/>

## Recipe Features

- Filament running on a load-balanced **Zerops PHP + Nginx** service
- Zerops **PostgreSQL 16** service as database
- Zerops KeyDB (**Redis**) service for session and cache
- Zerops **Object Storage** (S3 compatible) service as file system
- Proper setup for Laravel **cache**, **optimization**, and **database migrations**
- Logs set up to use **syslog** and accessible through Zerops GUI
- Utilization of Zerops built-in **environment variables** system
- Utilization of Zerops readiness check for proper **Zero downtime deployment**
- Utilization of Zerops health check for advanced **app monitoring**
- [Mailpit](https://github.com/axllent/mailpit) as **SMTP mock server**

<br/>

## Development vs. Production

### Development Setup

This setup includes tools and configurations for a rapid development cycle:

- Mailpit as the SMTP mock server
- Fully commented-out configurations that you can easily switch to production settings

### Production Setup

For a production-ready environment, consider the following modifications:

- Use a highly available version of the PostgreSQL database by changing `mode` from `NON_HA` to `HA` in the recipe YAML.
- Use at least two containers for the Filament service to achieve high reliability and resilience by adding
  `minContainers: 2` in the recipe YAML.
- Use a production-ready third-party SMTP server instead of Mailpit.

You can see a production example setup at [`zerops-project-production-import.yml`](https://github.com/zeropsio/recipe-filament/blob/main/zerops-project-production-import.yml).

## Changes Made Over the Default Installation

To modify your existing Filament app to run efficiently on Zerops, follow these steps:

- Add [zerops.yml](https://github.com/zeropsio/recipe-filament/blob/main/zerops.yml) to your repository. The provided
  example includes idempotent migrations, caching, and an optimized build process.
- Add [league/flysystem-aws-s3-v3](https://github.com/zeropsio/recipe-filament/blob/main/composer.json#L23) to your
  composer.json to support Object Storage file system.
- Setup health checks if needed. Health checks are enabled out of the box in Laravel 11.
- Utilize Zerops [environment variables](https://github.com/zeropsio/recipe-filament/blob/main/zerops.yml#L22-L73)
  and [secrets](https://github.com/zeropsio/recipe-filament/blob/main/zerops-project-import.yml#L13-L14) to setup S3 for
  file system, Redis for cache and sessions, and trusted proxies to work with reverse proxy load balancer.

<br/>

Need help setting your project up? Join the [Zerops Discord community](https://discord.com/invite/WDvCZ54).
