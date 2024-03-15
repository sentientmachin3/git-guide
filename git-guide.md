# Git CLI for the impatient

## Introduction

This is a guide for all users that want to learn (or are still learning) `git` from the command line. Despite the fact that there may be some errors in the following guide, I am not responsible for you destroying your production repository.

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

- `remote_name` will be the local reference name of the remote repo (conventionally "origin");
- `remote_url` is the address the remote reference points to; it can be an ssh address or an http(s) url, depending on the service you are hosting the remote on.

You can add a `.gitignore` file in the root directory of your project to specify files that you do not want to version, as an example, all files that may contain sensitive informations, such `.env`, configuration files for production and so on.

## Committing changes

The core concept of git is the **commit**. A commit is a set of changes that is recorded in the commit history. Let's say you made some changes to the codebase. You can view these changes by running the `git status` command: changes are now unstaged, and are completely new to git.

### Staging area

Git provides a staging area, where files are added before getting committed. Files can be added or removed from the staging area deliberately, and committed at any time.
In order to add some changes to the staging area, use the following command:

```
git add <file1> ... <filen>
```

or automatically, skipping file names and adding the `-A` flag.

To remove files from the staging area, use the command `git restore --staged <file1> ... <filen>`.

### Commits

Once you have some changes in the staging area, ready to be committed and/or added to production, you can to commit them.

To commit changes, run the `git commit` command:

```
git commit -m "<message>"
```

This command will generate a new commit on top of the current history, update the `HEAD` pointer (used to have a reference to the last commit) and use the `<message>` field to briefly describe the changes added. If you now run the `git status` command, the repository will show only changes you have not committed.

Some times you may want to commit all your local changes directly, for this cases I use a cool shortcut: if none of the changes happened to be on a new file, you can commit them directly adding the `-a` flag to the commit command. This will automatically add all the changes to the staging area and commit them, without the need to adding them manually. In case you have any new files though, changes have to be manually added to the staging area (at least to my experience).

## Syncing changes with remote

Cool, now we have committed changes locally, time to push to remote. This is pretty simple, just run

```
git push [--force] <remote_name> <remote_branch>
```

Changes will appear on the remote server, in the branch you are currently working on.

However, pushing to a remote without catching up with its newest changes may result in your changes not being accepted by the remote itself. The reason is simple: you are pushing a new history to the remote that does not contain some of the changes that already exist on the remote. There is a couple of ways you can fix this issue:

- merge remote changes into your branch, which the safest option;
- force pushing your changes (with the `--force` flag).

#### Force pushing

Force pushing will overwrite all remote changes with your local "branch status". Now suppose someone made some changes and pushed them to the same branch you are working on. You never merged those changes locally, so you don'thave them at all; in this case force pushing will result in changes of your coworker being deleted from the branch (and it's not very pleasant, I can assure you).

**Note: always specify the branch you are force pushing on, trust me.**

To avoid this inconveniences, the wisest option is to merge remote changes, always. There are a couple of cases you may want to force push though, which I tend to use frequently:

- you modified a local commit and want to overwrite the existing one on the remote;
- you squashed some commits together and want to update the remote history with the squashed version.

A safer option to use instead of `--force` is `--force-with-lease` (which I strongly suggest as the default). This will avoid overwriting other's commits on the remote branch.

### Pulling remote changes locally

Git allows you to merge other's people work into your local repository. To merge a remote branch, you have to run the `pull` command:

```
git pull <remote_name> <branch_name>
```

This command will merge all the changes you do not have locally, "automagically" integrating them into your version of the repository and updating the current `HEAD` pointer to the top of the updated branch.

#### Merge conflicts without getting crazy

Sometimes you and your coworker may have worked on the same files, and git may not be able to merge them correctly. In this case git generates what is called a **merge conflict**. A conflict occurs when you have some changes locally and you try to incorporate changes from another branch (which may or may not be on the remote).

Git of course will not make any assumptions on how to resolve the conflicts, allowing the developer to take the necessary actions to fix the issue. The portion of code interested by the conflict will look like this:

```
<<<<<<< HEAD
<your code>
=======
<their code>
>>>>>>> [git hash]
```

I agree this may look very scary (don't panic). It is indeed very simple: the first section marks the local code (the one your current HEAD points to); the bottom section contains the conflicting code pulled from the branch you are merging from. Note that `[git hash]` is the hash of the commit you are merging.

You have now four choices:

1. Forget about your code, remove it entirely and keep the code of the branch you are merging from;
2. Forget about your coworker's code, remove the bottom part and keep yours;
3. Merge the two sections to adjust the logic of the file to make some kind of sense;
4. Forget about the conflict, run `git merge --abort` and keep coding.

Once you have solved the issue (supposing you did), git enforces you to commit the changes. Personally, I like to specify which branch I was trying to merge.
