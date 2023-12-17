# Git CLI for the impatient

## Introduction

This is a guide for all users that want to learn (or are still learning) `git` from the command line. Despite the fact that there may be some errors in the following guide, I am not responsible for you destroying your production repository.

Version 1 was written in LaTex, this one will not, for the following reasons:

- I am tired of writing LaTex and I do not like `pdflatex` compiler errors;
- everyone can open a PR if willing so;

Git is a code version control tool developed in 2005 by Linux Torvalds himself. It allows to quickly handle code changes among multiple developers, without any difficulties (most of the times).

## Environment setup

### Installation and configuration

Git installation is pretty straightforward. If you are using Linux, just use the package manager provided by your distro,`pacman`, `apt` or whatever. I think, since I am not a MacOS user, it can be installed via `brew`. On windows, download it from the [site](https://git-scm.com).

Git requires minimal configuration:

```
git config --global user.name "<username>"
git config --global user.email "<email>"
```

This commands will ensure your git configuration is coeherent amongst all repositories, both locally and on remotes.

## Usage

### Project start and initialization

When you first start a project, to initialize git as your versioning tool, you just run the command:

```
git init
```

This command will create a single `.git` directory, which contains all the basic informations git needs to track all of your changes (not really, but we will deep dive into it later on). Git will now work locally, since you did not setup a remote repo (yet).

A **remote** is basically a reference of a remote server. This will allow to sync changes to the codebase amongst all other developers working on the project. The remote server will contain a copy of your local repo, it will be (at each `push` command) in sync with your local repository.

To add a remote reference to your local repository, you need to run a command setting up the name and the url of the remote repo:

```
git remote add <remote_name> <remote_url>
```

where:

- `remote_name` will be the local reference name of the remote repo (conventionally "origin")
- `remote_url` is the address the remote reference points to; it can be an ssh address or an http(s) url, depending on the service you are hosting the remote on.
