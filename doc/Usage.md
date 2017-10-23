# Installation

## For an application

You can install `Rothenberg` in a new project or in an existing one.  
For example, if your project is an application located in `path/to/project`:

1. `cd path/to/project` ;
2. Do `wget -O - https://github.com/norsys/rothenberg/raw/bundle/install.sh | sh`.

Once the install is done, if you already have a `./Makefile`, just add `include env/Makefile` in it to profit of `Rothenberg`'s targets.  
You can also define `VIRTUAL_HOST` variable before including `env/Makefile` (see above for more informations).  
Moreover, you can edit [`./docker-compose.override.yml`](https://docs.docker.com/compose/extends/#understanding-multiple-compose-files) to add specific `docker` services or networks.  
Finaly, do `make start` to download PHP depedencies and start services.

## For a bundle

1. `cd path/to/project` ;
2. Do `(export TARGET=bundle; wget -O - https://github.com/norsys/rothenberg/raw/bundle/install.sh | sh)`.

Once the install is done, if you already have a `./Makefile`, just add `include env/Makefile` in it to profit of `Rothenberg`'s targets.  
Moreover, you can edit [`./docker-compose.override.yml`](https://docs.docker.com/compose/extends/#understanding-multiple-compose-files) to add specific `docker` services or networks.

## Common steps for application and bundle

After installation was done, you can add and commit all new files in your project (yes, really, commit them in your project):

1. `git add .` ;
2. `git commit -m "<WHATEVER YOU WANT>"` ;
3. `git push`.

# Configuration for a project

## Configuration of `docker` and `docker-compose`

If your project needs some aditionnal `docker` services, define them in the [`./docker-compose.override.yml`](https://docs.docker.com/compose/extends/#understanding-multiple-compose-files).  
For example, to add `mysql`, edit `./docker-compose.override.yml` and add this in the `services` section:

```
mysql:
	image: mysql:5.6.31
	volumes:
		- ./var/mysql:/var/lib/mysql
```

If you want to link the `mysql` service to `php-fpm`, add this in the `services` section:

```
php-fpm:
	links:
		- mysql
```

If you want to know all services defined by `Rothenberg`, do `make rothenberg-docker-services`.  
For more informations about `./docker-compose.override.yml`, please read its [official documentation](https://docs.docker.com/compose/extends/#understanding-multiple-compose-files) and the `docker-compose` file [reference](https://docs.docker.com/compose/compose-file/).

## Configuration of `make`

You can add [prerequisites](https://www.gnu.org/software/make/manual/html_node/Rule-Syntax.html#Rule-Syntax) for targets defined by `Rothenberg`.  
For example, if you want to create the directory `var/mysql` via `make`, add in `./Makefile` after the include of `./env/Makefile`:

```
vendor/autoload.php: | var/mysql

uninstall/var: uninstall/var/mysql

var/mysql:
        $(MKDIR) $@
```

Some special targets defined by `Rothenberg` are used in this example:

- `vendor/autoload.php` is the trigger for `vendor` installation via [`composer`](https://getcomposer.org) ;
- `uninstall/var` is the target used to clean the `path/to/project/var` directory ;

Moreover, the target `uninstall/var/mysql` is handled by the [pattern rule](https://www.gnu.org/software/make/manual/html_node/Pattern-Intro.html#Pattern-Intro) `uninstall/%` which delete any file or directory defined by wildcard `%`.  

If you want to know all targets defined by `Rothenberg` to add some prerequisites to them, just do `make rothenberg-targets`.  
For more informations about `make`' syntax and features, please read its [official documentation](https://www.gnu.org/software/make/manual/html_node/).

## Configuration of `PHP`

You can customize PHP's configuration in `CLI` and `FPM` context.  
To do that for `CLI` context, edit `path/to/project/env/php/cli/php.ini` (or `path/to/project/env/php/fpm/php.ini` for `FPM`) and execute `make restart`.
For more information about PHP configuration, please read its [official documentation](http://php.net/manual/en/ini.core.php).

## Check styling

Out of the box, `Rothenberg` provides PHP style checking configured via `path/to/project/env/check-style.xml` and `make check-style`, but you can add style checking for some other languages.
For example, to add style checking for JavaScript using [`eslint`](http://eslint.org), add this in `path/to/project/Makefile`:

```
check-style: check-style-js

check-style-js: | bin/node ## Check coding conventions for JavaScript.
	bin/node eslint -c .eslintrc --ignore-path .eslintignore ./src
```