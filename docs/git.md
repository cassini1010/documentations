# Getting Started

Git has three main states that your files can reside in *modified*, *staged*, and *committed*.

The most official build is available for download on the Git website. Just go to [Git - Downloading Package](https://git-scm.com/download/win) and the download will start automatically. 

Note that this is a project called Git for Windows, which is separate from Git itself; for more information on it, go to [https://gitforwindows.org](https://gitforwindows.org/).

#### Config

You can view all of your settings and where they are coming from using

```git
git config --list --show-origin
```

To view only settings

```git
git config --list
```

There are `--system` `--local` `--global` configurations in git. To list global settings/configurations and their origin

```git
git --list --global --show-origin
```

#### Help

Use `--help` to get a full-blown man page

Use `-h` to get a short refresher man page

```git
git status --help 
```

#### 

# Git Basics

#### Turn an existing directory into Git repository

Run `git init` in that directory.

```git
git init
```

#### Clone

This is another way to have a git repository. To have a desired name for the repository to be cloned use below command.

```git
git clone https://github.com/libgit2/libgit2 mylibgit
```

Here mylibgit is a desired name given to the cloned repo.

Above example uses the `https://` protocol, but you may also see `git://` or `user@server:path/to/repo.git`, which uses the SSH transfer protocol.

#### status

```git
git status        # to check the status of the local repo
git status -s     # gives a short status
```

#### add and commit

```git
git add <file/folder names> ....   # adds files/folders into staging area
git commit -m <commit message>     # uses the files in staging area to make a new commit.
```

<mark>Status, add and commit are the mostly used commands on daily basis in git.</mark>

### <u>diff</u>

To see what you’ve changed but not yet staged, type `git diff` with no other arguments. This command compares what is in your 'working directory' with what is in your 'staging area'.

```git
git diff
```

If you want to see what you’ve staged that will go into your next commit, you can use. This command compares your staged changes to your last commit.

```git
git diff --staged
```

If you run `git difftool` instead of `git diff`, you can view any of these diffs in software like emerge, vimdiff and many more (including commercial products). Run `git difftool --tool-help` to see what is available on your system.

#### To skip the `git add` part and directly commit the changes use `git commit -a -m "<commit message>"`. Adding the `-a` option to the `git commit` command makes Git automatically stage every file that is already tracked before doing the commit, letting you skip the `git add` part

#### Removing a file

```git
git rm <file name> ## to remove a file from git tracked local repo
git rm --cached <filename> ## to remove the file from staging area if the file was staged already
```

#### Rename file

If you want to rename a file in Git, you can run something like

```git
$ git mv file_from file_to
```

#### Log / commit history

```git
git log

git log --patch ##shows the difference introduced in each commit.
git log --patch -2 ## to limit the results to latest 2 commits

git log --graph ## gives a good graphicla representaiton of branching.

git log --oneline ## prints a brief description of every commit.
```

```git
git log --since=2.weeks
```

This command works with lots of formats — you can specify a specific date like `"2008-01-15"`, or a relative date such as `"2 years 1 day 3 minutes ago"`.

```git
git log -- path/to/file
```

 If you specify a directory or file name, you can limit the log output to commits that introduced a change to those files.

```git
git log <branch name>  ## commit history of desired branch

Much useful one:
git log --oneline --graph --all  ## oneline commit history of all branchs and a nice graph representation 
```

#### amend

```git
git commit --amend -m <commit message>
```

The obvious value to amending commits is to make minor improvements to your last commit, without cluttering your repository history with commit messages of the form, “Oops, forgot to add a file” or “Darn, fixing a typo in last commit”.

### remote

```git
git remote -v ##To list all the remotes that you have.

git remote add mint https://github.com/wingardium/leviousa ## adds a remote called mint to the list of remotes


git remote update 
```

### fetch

```git
git fetch origin
git fetch mint ## fetches the changes that remote has and local doesnt have
```

#### To see detials about remote

```git
git remote show <origin>
```

### renaming remote

```git
git remote rename mint ginger ##rename remote `mint` to `ginger`
```

### remove a remote

```git
git remote remove ginger  ## removes ginger remote.
```

### aliasing

```git
git config --global alias.co checkout
```

here `checkout` is aliased as co and you can use `git co` to run the commit command. This could be helpful to perform repeatative commands in a efficient way.

#### Tagging

 Tags represent specific points in a repository’s history as being ***important***.

```git
git tag [optional -l] ## lists the exisitng tags in the repository


git tag -a v1.0.0 -m "<message for tagging>" ## annotated tagging, consists of detailed info on a commit 
git tag v1.0.0 ## light-weight tagging, only contains the cheksum of the commit
```

To tag a commit in the later point;

```git
git tag -a v1.0.0 <commit number>
```

When pushing a commit to a remote repo the tags are not pushed. It has to be pushed explicitly.

```git
git push origin <tag-name>
```

To delete a tag;

```git
# Both the commands below are necessary to completely remove a tag from repo.
# first command removes it from local, while second from remote.
git tag -d <tag-name>
git push origin --delete <tag-name>
```

## Git graphical interface

When git is installed graphical visualisation tools like `gitk` and `git-gui` are also installed.

`gitk` is a graphical history viewer. Can be used as a powerful version of the `git log`

`git-gui`, on the other hand, is primarily a tool for crafting commits.

## pygit2

The bindings for Libgit2 in Python are called Pygit2, and can be found at [https://www.pygit2.org](https//www.pygit2.org/).

# Git Branching

```git
git checkout <branch name> OR  git switch <branch name> ## to switch to an existing branch


git checkout -b <branch name> OR git switch -c <branch name> ## to create and checkout to the new branch.
```

#### Merge a branch

If you take a new branch to implement a new feature and create a lot of commits in that branch. You still can keep the commit history clean before merging to the master branch by using below command

```git
git merge --sqaush <branch name>
```

If you want to use a graphical tool to resolve merge issues, you can run `git mergetool`, which fires up an appropriate visual merge tool and walks you through the conflicts.

```git
git mergetool --tool=<tool>
```

To see what branchs are merged/not merged to the current branch,

```git
git branch --merged [optional branch name]
git branch --no-merged [optional branch name]
```

#### list branches in remote

```git
git branch -r
```

#### Rebasing

With the `rebase` command, you can take all the changes that were committed on one branch and replay them on a different branch.

#### Renaming a branch

To change the branch name use `--move` flag in branch command. To change the name in remote too, push the changes to remote.

```git
git branch --move <oldt name> <new name>
git push --set-upstream origin <new name>
```

After pushing the changed branch name to remote, it now has both the old branch and new branch. To delete the old branch from remote;

```git
git push origin --delete <old-branch-name>
```

Ex; If the goal is to rename branch from `master` to `main` , run `git 

# <u>Git Plumbing and Porceline</u>

All the user friendly commands that we use like  `checkout`, `branch`, `remote`, and so on, are called “***porcelain***” commands.

"***Plumbing***" commands are lower-level commands, because they give you access to the inner workings of Git.

# Git Tools

#### Git interactive staging

If you run `git add` with the `-i` or `--interactive` option, Git enters an interactive shell mode for staging.

#### Stash

To save your half done work in order to swith to a different branch, use;

```git
git stash
```

To see which stashes you’ve stored, you can use;

```git
git stash list
```

To apply the stash after you are back to the branch wiht half done work use below command. This will apply the latest stash available in the list.

```git
git stash apply # apply latest stash

git stash apply stash@{3} # apply a specific stash with number 3 on the list.
```

#### Clean

The better way to use `git clean` command is with `interactive` flag;

```git
git clean -i -x
```

#### grep

Git ships with a command called `grep` that allows you to easily search through any committed tree, the working directory, or even the index for a string or regular expression.

In the below command git shows the line number where it has found the match.

```git
git grep -n main # here main is the search string.
```

To show the search result in a summary use

```git
git grep --count main # main is the searcch string
```
