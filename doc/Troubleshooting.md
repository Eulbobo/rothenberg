# Update Rothenberg

To update `Rothenberg` in a project, just do:

1. `make rothenberg/update` ;
2. `git add .` ;
3. `git commit -m "<WHATEVER YOU WANT>"` ;
4. `git push`.

# Houston? We've got a problem!

First, don't panic.
Then execute `docker system prune -f` to clean the docker environment, and try to reproduce the problem.  
If the problem disappears, say thanks to Gandalf and enjoy!  
But if the problem always exists, open an issue to help us to improve `rothenberg`.  
If you open an issue, describe your problem precisely and give maximum information about your environment:

- Operating system ;
- `docker` version, do `docker --version` to obtain it ;
- `docker-compose` version, do `docker-compose --version` to obtain it ;
- `make version`, do `make --version` to obtain it ;
- Give output of `docker ps -a` ;
- Give output of `docker network ls` ;

Moreover, if you encounter a problem during installation, reexecute it with `(export WITH_DEBUG=yes; wget -O - https://github.com/norsys/rothenberg/raw/master/install.sh | sh)`, and add the output to your issue.  
And if you encounter a problem during a `make` command execution, reexecute it with `make <YOUR TARGET HERE> WITH_DEBUG=yes`, and add the output to your issue.  
Finaly, you can join the channel `##rothenberg` on the IRC network `freenode`:

1. Download an IRC client ;
2. Configure it with your personal information ;
3. Use it to [connect to the `freenode` network](https://freenode.net/kb/answer/chat) ;
4. Do `/j ##rothenberg` ;
5. Say `Hello!`.