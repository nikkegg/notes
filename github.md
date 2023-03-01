# Github

This file contains how-toes (hairy ones) and explanations of how to make GitHub
do what needs to be done in order for eng team to be happy.

## Branch protection rules

In any approach to version control there are few requirements we want our
git workflow to uphold:

- No one can push to the remote without their code being approved by someone else
- No one can force push to the remotes
- History is linear (no merge commits, fast-forward merges only)

The first requirement is due to security - if a device is lost or stolen, and
someone attempts to push to the remote, the remote will reject the request unless
a pull-request is raised and another developer approves the changes. This behaviour
is enforced by **Require a pull request before merging** and **Require approvals**
rules (under Branches -> Branch protection rules).
Depending on the project/branch (job-hobby/master-develop etc) you might also
want to enforce passing status checks, conflict resolution etc.

The second requirement is to prevent an accidental Armageddon of the repo. This
is enforced by unselecting **Allow force pushes** rule. In case if force-pushing
is required, repo admins can temporarily allow force-pushing, and then
disallow it again.

The final requirement is due to the fact that linear things in general are easier
to reason about than non-linear ones. In this approach, Git history is a simple,
append-only log of changes in a repository, which is easy to follow, tag,
and undo if needed. It also makes various git tools easier to
use (`git bisect` and `git log` are primary examples). This is enforced by
**Require linear history** rule, which disables the **Create a merge commit**
merging option in the GitHub UI.

The last requirement might be hard to implement in _Git Flow_ style workflow and
it is somewhat artificial/preferential. More details on this below.

## Git workflows

### Git flow

[Git Flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) workflow.

Approach to version control where multiple long-lived (mainline) branches exist
and are maintained.
Each mainline corresponds to a different environments.
Branches are merged one into another to move changes across the environments.
Generally seen as inferior and outdated to when compared with
[trunk-based approach](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development)
However, might be preferrable if preview functionality it important.

Example of `branch`:_environment_ mapping:

- `develop`:_development_
- `staging`:_staging_
- `master`:_production_

The full lifecycle of a commit typically looks like:

`feature-branch` -> `develop` -> `staging` -> `master`
I.e `develop` is being merged into `staging`, `staging` into
`master`.

#### Pushing to higher environments with Git Flow approach

This is more involved than merging in trunk-based approach. The reason for this
is that ideally, we want to combine two merging strategies in one repo:

1. We want to use **Squash and Merge** strategy when merging feature branches into
   our development branch.
2. When releasing changes from our development branch to higher environments,
   we want to perform a fast-forward merge like **Squash and Merge** does but
   without squashing.

We could consider using [**Rebase and Merge**](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/about-merge-methods-on-github#rebasing-and-merging-your-commits)
as an alternative to fast-forward in step 2,
however in order to avoid disadvantages of this approach, we would have to allow
force-pushing to remote which is not good. Unfortunately at the time of writing
this, there is no option in GitHub UI which would allow perform fast-forward
merge without squashing, so we will have to resort to command-line `git`.

In order to release from development branch upstream:

1. Create a branch containing commits you want to merge into mainline (or open
   pull-request in the UI if you want to move all commits) 2. In the CLI, do `git checkout mainline`
2. Do `git merge feature-branch —ff-only`
3. Do `git push`

Pushing to remote will push your changes to remote, trigger the CI, and close
the pull-request. However, as discussed earlier, pushing will fail unless you have opened a PR
and someone has approved it.

### Trunk-based approach

Nicely summarised [here](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development)

#### Pushing to higher environments with Trunk-based approach

Relatively simple:

Merge feature branches into the trunk using **Squash and merge** option.
This keeps upstream branch clean and allows to revert entire commit quickly and
reliably. By default **Squash and merge** performs fast-forward merge so
that works well with linear history requirement. To enable this allow
**Allow squash merging** under Pull Requests settings and dissallow everything else.

Contributors will have to rebase their feature branch on the trunk
before merging.
