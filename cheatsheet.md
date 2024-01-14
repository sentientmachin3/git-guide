# Git cheat sheet

This is a personal cheat sheet for the commands I use. Feel free to report errors on github issues.

## Project initialization

| Command                                     | Description                              |
| ------------------------------------------- | ---------------------------------------- |
| `git init [--bare]`                         | Initialize a new emtpy repository        |
| `git remote add [remote-name] [remote-url]` | Add a new remote git server              |
| `git clone [--bare] [url] [folder-name]`    | Clone a new project from a remote server |

## Branching

| Command                                                   | Description                                        |
| --------------------------------------------------------- | -------------------------------------------------- |
| `git branch [branch-name]`                                | Create a new branch                                |
| `git checkout [branc-name]`                               | Move to a new branch (impacts local modifications) |
| `git branch [-a]`                                         | List branches                                      |
| `git branch -D [branch-name]`                             | Delete a local branch by name                      |
| `git merge [branch-name]`                                 | Merge the named branch into the current one        |
| `git worktree add [name] [source-branch] -b [branch-name] | Create a new worktree from a branch                |
| `git worktree list`                                       | List worktrees                                     |

## Committing changes

| Command                        | Description                                            |
| ------------------------------ | ------------------------------------------------------ |
| `git status`                   | List current changes and staging area contents         |
| `git add [-A] [files]`         | Add all files (`-A`) or some files to the staging area |
| `git restore --staged [files]` | Remove files from the staging area                     |
| `git commit [-a] -m [message]` | Commit all (`-a`) files with a message                 |
| `git reset --soft [commit]`    | Reset current branch to `[commit]`, preserving changes |
| `git reset --hard [commit]`    | Reset current branch to `[commit]`, removing changes   |

## Remote and local sync

| Command                            | Description                               |
| ---------------------------------- | ----------------------------------------- |
| `git fetch [remote-name] [branch]` | Fetch commit history from remote branch   |
| `git pull [remote-name] [branch]`  | Pull changes from branch into the current |
| `git push [remote-name] [branch]`  | Push changes to remote branch             |

Note: I normally use `git fetch -Ppaf` to prune unused local branches, helps keeping the local repository clean from stale or merged branches.

## Navigation in the history

| Command                          | Description                                      |
| -------------------------------- | ------------------------------------------------ |
| `git log [--oneline]`            | List local history of the current branch         |
| `git show [commit]`              | Show commit changes from a single commit         |
| `git diff [commit-1] [commit-2]` | Show differences between two commits or branches |
