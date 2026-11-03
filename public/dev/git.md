---
date: 2025-02-13 15:33
title: Git
slug: 2c0d30db
---

## git config

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## git remote

### list all remotes
```
git remote -v
```
### add a remote
```
git remote add <name> <url>
```
### set a existing remote's url
```
git remote set-url <name> <url>
```

## git checkout / git switch
### switch branch
```
git checkout <branch-name>
git switch <branch-name>
```
### create a branch, switch to it
```
git checkout -b <branch-name>
git switch -c <branch-name>
```

## git branch
### see what branch you're on
```
git branch
```
### create a branch
```
git branch <branch-name>
```
### rename branch
```
git branch -m <new-branch-name>
```

```
git branch -m <old-branch-name> <new-branch-name>
```

## git fetch
### fetch all branch from remote, not merging to local branch
```
git fetch <remote>
```

## git pull
### fetch current branch from remote, and merge to local branch
```
git pull <remote>
```

### git commit

```
-m "commit message"
```

```
--author="John Doe <john.doe@example.com>"
```
