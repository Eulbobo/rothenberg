# Rothenberg

`Rothenberg` allows a developper to create or maintain a Symfony application or a Symfony bundle very easily and without install something on his workstation (Mac or PC, Windows is not currently supported).  
It is not a standalone project, so it must be used in the context of an another project.

## Quick Start

If you have an UNIX operating system and `docker`, `GNU make` and an Internet access, to use `Rothenberg` to develop or maintain a Symfony application, execute the following command in a terminal:

```
wget -O - https://github.com/norsys/rothenberg/raw/master/install.sh | sh
```

Or to use it in the context of a Symfony bundle, do:

```
(export TARGET=bundle; wget -O - https://github.com/norsys/rothenberg/raw/master/install.sh | sh)
```

`Rothenberg` use a docker image during the installation process. To be sure to use the last version of this image, prefix the above commands with `docker pull norsys/rothenberg`:

```
docker pull norsys/rothenberg && wget -O - https://github.com/norsys/rothenberg/raw/master/install.sh | sh
```

But… maybe you should read the following information before executing one of these commands!

## Features
 - Docker and docker-compose configuration
 - Docker images management
 - Default PHP configuration for `CLI` and `FPM`
 - Helpers to hide `docker` and `docker-compose`
 - Atoum configuration
 - Automated `nginx` virtual host management
 - Networking
 - Environment management
 - Private PHP package management
 - Default `Makefile`
 - Project Management
 - Git configuration
 - Assets watcher

All features are detailled in the [Features](doc/Features.md) section

## Installation and Usage
All you need to know about how to install is available in the [Usage](doc/Usage.md) file

## Update / TroubleShooting
Got a problem? What to update ?
Check [TroubleShooting](doc/Troubleshooting.md) guide !

## Contributing
If you want to contribute, please refer to the [Contribution](Contributing.md) section

## Languages and tools

- [*docker*](https://docs.docker.com) ;
- [*docker-compose*](https://docs.docker.com/compose/) ;
- [*atoum*](http://docs.atoum.org) ;
- [*make*](https://www.gnu.org/software/make/manual/make.html) ;
- [*Symfony*](http://symfony.com/doc/current/index.html).

## History

Primary version of `Rothenberg` was born in the PHP business unit of [Norsys](http://norsys.fr), based in [Lyon, France](https://www.google.fr/maps/place/Lyon/@45.75801,4.8001016,13z/data=!3m1!4b1!4m5!3m4!1s0x47f4ea516ae88797:0x408ab2ae4bb21f0!8m2!3d45.764043!4d4.835659).  
It was made with love to industrialize our PHP development based upon Symfony.  
This project was a success, because we can now bootstrap a project or integrate a team and start to develop some features of fix bugs in a few minutes.  
So, we decided to open-source it, because we thinks that this kind of tools must be shared with the PHP community.

## Why `Rothenberg`?

[David Rothenberg](http://www.davidrothenberg.net) is a book author and a song composer which has made music with whales.  
This project uses `docker`, which has a whale as logo, and `composer`, `docker-compose` to set up a Symfony environment.  
So, `Rothenberg` seems to be a good choice as name ;).