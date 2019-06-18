# laravel-docker
Up and running Laravel with Docker with ease

## Feature highlights
- Nothing is required on host machine except Docker and Docker Compose
- Docker Compose with `web` service (php7.2), `database` service (mysql 5.6) and `MySql client` service (adminer)
- Web service is pre-installed with composer, laravel cli, curl, vim and dnsutils package

## Code structure

- `Dockerfile`: steps to be run to set up the `web` service, please have a look to see what it installs
- `docker-compose.yml`: Docker Compose file to define the 3 services `web`, `database` and `MySql client`

## Usage

- Put the 2 files `Dockerfile` and `docker-compose.yml` into your current project folder (in case you have already got 1 project set up) or an empty folder where your project is supposed to be placed.
- Run `docker-compose up -d`, after this step, there should be 3 containers up and running.
- Your current folder is mounted into `web` container's `/code` folder
- Run `docker exec -it <web-service-container-name> /bin/bash` to ssh into `web` service container.
- In case you do not have a Laravel project yet, create one by running `laravel new myfirstproject`.
- cd into `/code/myfirstproject`, start the web server by running `php artisan serve --host=0.0.0.0 --port=8000` (please notice the part *--host=0.0.0.0*)
- Access the Laravel web app from host machine by accessing `http://localhost:8000`
- Config MySql for your Laravel app using the following info: `host: db, username: root, password: admin` (this password is set up in `docker-compose.yml`

## Further installation

- If you would like to install more services such as `redis`, just put the service config into docker-compose.yml and rebuild the containers using `docker-compose build`

## Other info

- The `web` service is derived from the image `php:7.2`
- Laravel was at 5.8 at the moment this document was written

## Troubleshooting

- If you have ports conflicting, please change accordingly in the `Dockerfile` and `docker-compose.yml`
- If you cannot access the web app from host machine, please be sure you set `--host=0.0.0.0` when running `php artisan serve`
- If other issues occur, please report them [here](https://github.com/vukhuu/laravel-docker/issues).
