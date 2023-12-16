# Git CLI for the impatient

## Introduction

This is a guide for all users that want to learn (or are still learning) `git`
from the command line. Despite the fact that there may be some errors in the
following guide, I am not responsible for you destroying your production
repository.

Git is a code version control tool developed in 2005 by Linux Torvalds himself. It allows to quickly handle code changes among multiple developers, without any difficulties (most of the times).

Version 1 was written in LaTex, this one will not, for the following reasons:

- I am tired of writing LaTex and I do not like `pdflatex` compiler errors;
- everyone can open a PR if willing so;

## Environment setup

### Installation and configuration

Git installation is pretty straightforward. If you are using Linux, just use the package manager provided by your distro,`pacman`, `apt` or whatever. I think, since I am not a MacOS user, it can be installed via `brew`. On windows, download it from the [site](https://git-scm.com).

Git requires minimal configuration:

```
git config --global user.name "<username>"
git config --global user.email "<email>"
```

This commands will ensure your git configuration is coeherent amongst all repositories, both locally and on remotes.

