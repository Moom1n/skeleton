
# Docker + PHP 8.3 + Xdebug 3 + Postgresql 13.6 + Nginx 1.21 + Symfony skeleton 7.1.*

## Description

This is a basic stack for **create y running Symfony project** into Docker containers.
Here are the docker-compose built images:

- `nginx`, acting as the webserver v1.21.
- `php`, the PHP-FPM container with the 8.1 version of PHP. Xdebug is available by default.
- `postgresql` which is the Postgresql database container with a **Postgresql 13.6** image.

## Installation

### Docker containers

1. Clone this repository
2. Go inside folder `./docker`
3. Edit environment variables in ``.env`` file
   1. The value of the variable `PROJECT_NAME` is the `server_name` used in NGINX.
   
4. Build/run containers.
   ```
   docker-compose build
   docker compose up -d
   ```
### Symfony project
1. You should work inside the `php` container.
   ```
   docker compose exec php bash
   ```
2. Check requirements for a Symfony application
   ```
   symfony check:requirements
   ```
   you will see the following output in the terminal
   ```
   [OK]                                             
   Your system is ready to run Symfony projects
   ```
3. Create a new Symfony project
   ```
   composer create-project symfony/skeleton:"7.1.*" .
   ```
You Symfony project will be installed in ``/app`` folder. Now you can access it from the browser through the domain that you have specified in the `NGINX_SERVER_NAME` variable of the `.env` file.

![alt text](https://alcales.com/wp-content/uploads/2022/01/2022-01-16-19_05_34-Welcome-to-Symfony-Brave.png)

## Xdebug
Available by default. Configure `/docker/php/xdebug.ini`
- In case you want to deactivate it:
```
xdebug.mode=off
```
- In case you need debug only requests with IDE KEY: PHPSTORM from frontend in your browser:
```
xdebug.start_with_request = no
xdebug.idekey=PHPSTORM
```
- In case you need debug any request to an api (by default):
```
xdebug.start_with_request = yes
```

## Directory strcuture
```
Project (/var/www/)
├── docker
│   ├── mysql
│   ├── nginx
│   └── php
└── app
    └── .. all symfony content
```
