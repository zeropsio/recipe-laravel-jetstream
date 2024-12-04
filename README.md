# Zerops x Laravel Jetstream

[Laravel Jetstream](https://jetstream.laravel.com/introduction.html) is an advanced starter kit by Laravel. [Zerops](https://zerops.io) recipe for Jetstream includes all the advanced functionality — session and cache stored in Redis and files stored in Object Storage, this makes it perfectly suitable for production of any size.

![laravel](https://github.com/zeropsio/recipe-shared-assets/blob/main/covers/svg/cover-laravel.svg)

<br/>

## Deploy on Zerops
You can either click the deploy button to deploy directly on Zerops, or manually copy the [import yaml](https://github.com/zeropsio/recipe-laravel-jetstream/blob/main/zerops-project-import.yml) to the import dialog in the Zerops app.

[![Deploy on Zerops](https://github.com/zeropsio/recipe-shared-assets/blob/main/deploy-button/green/deploy-button.svg)](https://app.zerops.io/recipe/laravel)

<br/>

## Recipe features

- Laravel + Inertia.js running on a load balanced **Zerops PHP + Nginx** service
- Zerops **PostgreSQL 16** service as database
- Zerops KeyDB (**Redis**) service for session and cache
- Zerops **Object Storage** (S3 compatible) service as file system
- Proper setup for Laravel **cache**, **optimization**, and **database migrations**
- Logs set up to use **syslog** and accessible through Zerops GUI
- Utilization of Zerops built-in **environment variables** system
- [Mailpit](https://github.com/axllent/mailpit) as **SMTP mock server**

<br/>

## Production vs. development

Base of the recipe is ready for production, the difference comes down to:

- Use highly available version of the PostgreSQL database (change `mode` from `NON_HA` to `HA` in recipe YAML, `db` service section)
- Use at least two containers for Jetstream service to achieve high reliability and resilience (add `minContainers: 2` in recipe YAML, `app` service section)
- Use production-ready third-party SMTP server instead of Mailpit (change `MAIL_` secret variables in recipe YAML `app` service)

<br/>

## Changes made over the default installation

If you want to modify your existing Laravel/Jetstream app to efficiently run on Zerops, these are the general steps we took:

- Add [zerops.yml](https://github.com/zeropsio/recipe-laravel-jetstream/blob/main/zerops.yml) to your repository, our example includes idempotent migrations, caching, and optimized build process
- Add [league/flysystem-aws-s3-v3](https://github.com/zeropsio/recipe-laravel-jetstream/blob/main/composer.json#L14) to your composer.json to support Object Storage file system
- Setup [Jetstream config](https://github.com/zeropsio/recipe-laravel-jetstream/blob/main/config/jetstream.php#L79) to use object storage for file system
- Utilize Zerops [environment variables](https://github.com/zeropsio/recipe-laravel-jetstream/blob/main/zerops.yml#L25-L75) and [secrets](https://github.com/zeropsio/recipe-laravel-jetstream/blob/main/zerops-project-import.yml#L12-L16) to setup S3 for file system, Redis for cache and sessions, and trusted proxies to work with reverse proxy load balancer

<br/>
<br/>

Need help setting your project up? Join [Zerops Discord community](https://discord.com/invite/WDvCZ54).
