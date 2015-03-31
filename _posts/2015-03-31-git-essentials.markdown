---
layout: post
title: "Git Essentials"
date: 2015-03-31 20:00:00
categories:
- git
---

## File Lifecycle

untracted -> staging -> committed to local -> pushed to remote

## Commands

### Working locally

Init a repo:
```bash
$ git init
```

Checking status:
```bash
$ git status
```

Stage a file:
```bash
$ git add <file_name>
```

Stage all files including ones inside a subdirectory:
```bash
$ git add '*.txt'
```

Stage all files under a path:
```bash
$ git add -A <path>
```

Remove a file:
```bash
$ git rm <file_name>
```
`git rm` will not only remove the actual file from disk, but will also stage the removal of the files for us.

Commit:
```bash
$ git commit -m 'msg...'
```

View commits:
```bash
git log
```

### Working remotely

Add a remote repo:
```bash
$ git remote add <remote_name> <remote_url>
$ git remote add origin https://github.com/some-repo.git
```

Push to remote:
```bash
$ git push -u <remote_name> <local_branch_name>
$ git push -u origin master
```
`-u` tells Git to remember the parameters, so next time we can simply run `$ git push`.
The local/remote repo has a default branch named `master`.

Pull from remote:
```bash
$ git pull <remote_name> <remote_branch_name>
$ git pull origin master
```

Replace local with remote:
```bash
$ git fetch origin
$ git reset --hard origin/master
```
It will drop all your local changes and commits, fetch the latest history from the server and point your local `master` branch at remote's `origin/master`.

### Differenting

Diff working copy with last commit:
```bash
$ git diff HEAD
```
`HEAD` is a pointer to the last commit.

View staged diffs:
(view changed caused by recent `git add`)
```bash
$ git diff --staged
```

### Rolling back

Unstage a file:
```bash
$ git reset <staged_file>
```

Revert a file to its last committed status:
```bash
$ git checkout -- <changed_file>
```

### Branching

Create a branch:
```bash
$ git branch <branch_name>
```

Switch to a branch:
```bash
$ git checkout <branch_name>
```

Merge changes from another branch to the `master` branch:
```bash
$ git checkout master // switch back to master
$ git merge <branch_name> // do the merge
// resolve any conflicts...
$ git add <some_resolved_files...>
$ git commit -m 'Merge changes from <branch_name> to master...'
$ git push // push changes from local to remote
$ git branch -d <branch_name> // done with the branch, delete it now
```

Preview diffs between two branches:
```bash
$ git diff <branch_to_merge_from> <active_branch>
```

Push branch to remote:
(a branch only lives locally unless you push it to the remote and make it accessible by others)
```bash
$ git push <remote_name> <branch_name>
$ git push origin local-branch
```

### Tagging

It is recommended to create tags for software releases. This is a known concept which also exists in SVN.
```bash
$ git tag <tag_name> <commit_id>
$git tag 1.0.0 1b2e1d63ff
```
The `<commit_id>` stands for the first 10 characters of a commit id.

### History

See commits by a certain author:
```bash
$ git log --author=<username>
```

See each commit in one line:
```bash
$ git log --pretty=oneline
```

See ASCII art tree of all branches:
```bash
$ git log --graph --oneline --decorate --all
```

See only which files have changed:
```bash
$ git log --name-status
```

## References

- [Try Git](https://try.github.io)
- [Simple Git Guide](http://rogerdudler.github.io/git-guide/)
