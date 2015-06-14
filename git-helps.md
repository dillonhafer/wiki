# Git

## Initial Setup

Before doing any development on a new machine configure git with your name and email.

```
git config --global user.name "First Last"
git config --global user.email "your.email@youremail.com"
```

## Central Repository

The git repository can be accessed at https://github.com/dillonhafer/wiki. Connect over SSH with the user name _git_.

## Checking out an existing repository

```
git clone ssh://git@bitbucket.org:boondockwalker/existing-repo.git
```

## Basic Workflow

Ensure the master branch is checked out.
```
git checkout master
```

Pull in any changes from the remote repository.

```
git pull
```

Create a new branch.

```
git checkout -b my_feature
```

Make changes to files.

Add the files you have changed to the staging area.

To add a specific file:

```
git add path/to/changed/file
```

To add all changed files in the repository at once by adding the current directory path:

```
git add .
```

To delete a file from repository:

```
git rm path/to/file
```

Commit changes to local repository.

```
git commit
```

Keep adding, editing, deleting, and committing until the change is complete.

Checkout master again.

```
git checkout master
```

Re-pull to ensure you have the most recent changes on the remote repository.

```
git pull
```

Merge feature branch with squash option to mash entire feature into one commit.

```
git merge --squash my_feature
```

The merge puts everything in the staging area but does not automatically commit.

```
git commit
```

Push your feature to the remote repository.
```
git push
```

Delete your feature branch. (But you may want to wait a while to ensure you don't need to go back to any intermediate commits)
```
git branch -d my_feature
```

## View current status

```
git status
```

## Revert an uncommitted change

```
git checkout path/to/file/to/restore
```

## Changing the current branch

List local branches
```
git branch
```

List remote branches
```
git branch -r
```

List local and remote branches
```
git branch -a
```

```
git checkout branch_name
```

## Deleting a branch

Delete a local branch
```
git branch -d branch_name
```

Delete the branch remotely -- note the colon
```
git push origin :branch_name
```

## Cleaning up deleted remote branches

```
git remote prune origin
```

## Undo a commit

Only if the commit has not been pushed (if someone else sees your commit you can no longer rewrite history):
```
git reset --soft HEAD^
```

## Creating a new repository

On the git server (run commands as user *git*):

```
cd /var/git
mkdir new_repo.git
cd new_repo.git
git --bare init
cp /var/git/repo_name.git/hooks/post-receive hooks
```

On the client machine:

```
mkdir new_repo
cd new_repo
touch tmp.txt
git init
git add .
git commit -m 'Initial commit'
git remote add origin ssh://git@github.com/dillonhafer/new_repo.git
git push -u origin master
```

## Resources

* http://progit.org/book/ -- whole book on git
* http://book.git-scm.com/index.html -- another whole book on git
* http://gitref.org/ -- reference material
* http://help.github.com/ -- GitHub's help pages
