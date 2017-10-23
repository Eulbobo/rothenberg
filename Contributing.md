# Contributing

## About workflow

We're using pull request to introduce new features and bug fixes.  
Please, try to be explicit in your commit messages:

1. Explain why the change was made ;
2. Explain technical implementation (you can provide links to any relevant tickets, articles or other resources).

You can use the following template:

```
# If applied, this commit will...

# Explain why this change is being made

# Provide links to any relevant tickets, articles or other resources
```

To use it, just put it in a text file in (for example) your home and define it as a template:

```
# git config --global commit.template ~/.git_commit_template.txt
```

## About testing

There are some `make` targets to test `Rothenberg`, especially install and update of bundle and application.  
To run them, just do `make tests`.  
Please, do not omit to update tests before implemeting new feature or doing a bug fix.  
To update tests, just update the content of the `references` directory.