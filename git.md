# Git

## Quick reference

### Push

`git push origin origin/tag:target_tag` - fast-forward remote tag to a target
tag. Everything-ish in `git` can be considered a tag: branch, commit, tag itself.

### Pull/fetch

`git fetch -p` - prune remote branches and keep history in `git log` clean

### Diff

`git diff-index -U --cached -G <regexp> HEAD` - search for a keyword in modified
files tracked by git

### Reflog

`git reflog refs/remotes/origin/master`- show your last local action for a
particular remote. Makes it easy to see history of pushes/pulls so you can see
what was deployed and when. Also is helpfgul when you want to pull commits from reflog
even if you have reset local branch to remote and lost your changes

### Stash

`git stash show <stash_entry> -p` - preview content of stashed entry

`git stash push -m` - name the stash your pushing
