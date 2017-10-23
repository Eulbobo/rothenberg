# Features
In the following, we assume that the command `make -f vendor/norsys/rothenberg/Makefile install` was made in the directory `path/to/project`.

## Docker and docker-compose configuration

`Rothenberg` creates a `docker-compose.yml` with some services pre-configured and an empty `docker-compose.override.yml` (only if this file does not exist) in the directory `path/to/project`.  
If you want to override some services's configuration, use [`docker-compose.override.yml`](https://docs.docker.com/compose/extends/#understanding-multiple-compose-files).

## Docker images management

`Rothenberg` pulls the lastest version of each docker image via `make start` or `make restart` (see below for more information about these commands).  
These images are:

- `nginx` ;
- `php-fpm` ;
- `php-cli` ;
- `composer` ;
- `node`.

It's possible to disable this feature via the `.rothenberg.config` file.

## Default PHP configuration for `CLI` and `FPM`

`Rothenberg` provides a `php.ini` for CLI and FPM in `path/to/project/env/php/cli` and `path/to/project/env/php/fpm` respectively.

## Helpers to hide `docker` and `docker-compose`

`Rothenberg` provides several helpers in `path/to/project/bin` to hide `docker` and `docker-compose` complexity.  
So, all scripts in `path/to/project/bin` can be run in the traditional way even if `docker` is used in the background.  
For example, to update PHP dependencies, just do `bin/composer update`.

## Atoum configuration

`Rothenberg` installs files `path/to/project/.atoum.php`, an atoum runner and a base test class in `path/to/project/tests/units`.

## Automated `nginx` virtual host management

`Rothenberg` provides an automated `nginx` virtual host management via the `make` variable `VIRTUAL_HOST`.  
To define the virtual host for your project, define its value before including `./env/Makefile` (see below for more information about that):

```
VIRTUAL_HOST := foo.bar

include env/Makefile
```

## Networking

`Rothenberg` allows you to share an [`nginx-proxy`](https://github.com/jwilder/nginx-proxy) docker's service between several projects, or any other services.  
For that purpose, it creates a network named according to the value of make's `ROTHENBERG_NETWORK` variable, which has `rothenberg` as default value.  
If you want to override its value, in the project's `Makefile`, just add `ROTHENBERG_NETWORK := yourNetworkName` before including `env/Makefile` (see below for more information about that).

## Environment management

`Rothenberg` allows you to install a project in several environments using the `make` variable `ENV` and [`SYMFONY_ENV`](http://symfony.com/doc/current/configuration/environments.html).  
Default value of `ENV` is `dev`, and the default value of `SYMFONY_ENV` is `ENV`.  
So, to install a project in a `prod` environmment using the `dev` Symfony environment, just do:

```
# make install ENV=prod SYMFONY_ENV=dev
```

By default, the Symfony debug mode is enabled, but you can disable it using the `make` variable `SYMFONY_DEBUG`:

```
# make install SYMFONY_DEBUG=false
```

## Private PHP package management

`Rothenberg` can handle SSH key needed to access some private PHP packages via `composer`.  
Out of the box, it will use the key `$(HOME)/.ssh/id_rsa`, but you can override this using `make <target> SSH_KEY=/path/to/your/ssh/key`.
Your secret key will never be copied by `Rothenberg`.

## Default `Makefile`

If your project has no `Makefile` during its installation, `Rothenberg` provides a default `Makefile` for it.  
Moreover, it provides in `path/to/project/env` a `Makefile` with some interesting targets (see below).  
This `Makefile` is already included in the default `Makefile` provided by `Rothenberg`.  
If the project already has a `Makefile` before `Rothenberg` installation, add `include env/Makefile` in it to use `Rothenberg` targets.

## Project Management

`Rothenberg` allows you to use *make* to manage a project, with the following `make` targets:

- `install` install localy `docker-compose`, `php-(?:cli|fpm)`, `composer`, `node`, `npm`, `nginx` and configure them ;
- `reinstall` restart the project ;
- `uninstall` to uninstall the project ;
- `start` start all services needed by the website (`nginx`, `php-fpm`…) ;
- `stop` stop all services needed by the project ;
- `restart` restart all services ;
- `status` display status of each services ;
- `security` to check security of PHP dependencies ;
- `check-style-php` to check PHP coding convention according to `env/php/check-style.xml` ;
- `fix-style-php` to fix PHP coding convention according to `env/php/check-style.xml` ;
- `unit-tests` to run all unit tests ;
- `rothenberg/update` to update `Rothenberg` (see the `Update` section below) ;
- `help` display a tiny help about each of available commands.

Some of these targets are available only if you use `rothenberg` to develop an application.  
Use `make help` to know available targets according to your type of project.

## Git configuration

`Rothenberg` installs files `.gitignore` and `.gitattribute` with default values in the directory `path/to/project`.  
Moreover, it installs a [pre-commit hook](https://git-scm.com/book/it/v2/Customizing-Git-Git-Hooks) to check coding convention via  `make check-style`.

## Assets watcher

`Rothenberg` provides an assets watcher via `bin/watchodg`, which is automatically started via `make start` or `make restart`.