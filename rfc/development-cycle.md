
# Jupyter Development Cycle

The goal of this document is to outline a development cycle for JupyterLab which makes it very easy to do releases. As [documented in this issue](https://github.com/jupyterlab/jupyterlab/issues/8195), it's currently a quite laborious and specialized process. If we can make releases easier to manage, and push any of the hard work around so it's tackled by the authors of the PRs instead of the release managers, we can release more easily and free up core developer time for other matters.

This is meant to support our existing release cycles, not change them, but just provide some standardization and tooling to aid us in keeping to them.

## Assumptions

I have found it helpful to try to first outline the assumptions of our release and development process.

Please give feedback on these first.

You can consider these in addition to the [SemVer 2.0.0](https://semver.org/) spec, having more to do with the relations between the code evolution between multiple versions. They assume we are already following SemVer.


**alpha, beta, rc**: Each release goes through some optional number of alpha, beta, and RC release, before the final. For some final release `{x}.{y}.{z}` it can be modeled with this state machine

1. Start by releasing one of these:
    1. `{x}.{y}.{z}a0`
    2. `{x}.{y}.{z}b0`
    3. `{x}.{y}.{z}rc0`
    4. `{x}.{y}.{z}`
2. Then the next release can be either an increment of the last number or a release of one of the initial following your
   release. For example after `{x}.{y}.{z}b10` you could release `{x}.{y}.{z}b11` or `{x}.{y}.{z}rc0` or `{x}.{y}.{z}` (final).

**Previous Ancestor**: The next increment will be the git ancestor of the previous increment.

* Patch: `{x}.{y}.{z}` is an ancestor of `{x}.{y}.{z+1}`.
* Minor: `{x}.{y}.0` is an ancestor of `{x}.{y+1}.0`.
* Major: `{x}.0.0` is an ancestor of `{y+1}.0.0`.

**Single Active**: No commits will be queued up for a release until the previous increment was fully release
(this also falls out of the above assumption). 

* Patch: No commits towards `{x}.{y}.{z}` till `{x}.{y}.{z-1}` final is released.
* Minor: No commits towards `{x}.{y}.0` till `{x}.{y-1}.0` final is released.
* Major: No commits towards `{x}.0.0` till `{x-1}.0.0` final is released.

The last two mean you have to totally finish a release on one branch before you start on the next one. For example, it would be illegal to have releases in this order: `1.2.0a0`, `1.3.0a0`, `1.2.0`, then `1.3.0`. However, you could have `1.2.0a0`, `1.1.1a0`, `1.2.0`, then `1.1.1`, because these would be on different branches, `1.x.0` and `1.1.x`.

**JavaScript versions In Sync** We are ok always keeping the JS version bumps in sync. Meaning that if we do a major release of the Python package we also do a major release of all JS versions.

## Strategy

Based on these assumption we can create a consistant branching strategy.

### Branches

Each branch should be aligned to different releases:

1. Patch: `{x}.{y}.x` branches.
2. Minor: `{x}.x.0` branches. After final release `{x}.{y}.0` create new patch `{x}.{y}.x` branch.
3. Major: `master` branch. After release `{x}.0.0` create new minor `{x}.x.0` branch and new patch `{x}.0.x` branch.

Each increment has a corresponding "latest" branch for the greatest working version. For example with two branches `2.x.0`, `1.x.0`  the "latest" minor branch is `2.x.0`. The latest major branch is always `master`.

*Note: We could instead have separate branches for each version, but this isn't necessarily if we are going by the **Single Active** assumption above.*


### PR Semver Tags

Each PR should be tagged with one of three tags `semver:patch`, `semver:minor`, `semver:major` before it is merged. We could do this manually or by possibly giving a first guess [using type analysis](https://api-extractor.com/) or some commit message keywords. We should have a bot that blocks merging if one of these is not added.

If you have change that is *only* a backprt, and should not appear in master, then you can target that branch as the base of this merge.

### PR Backports
Once a PR is merged into master, backport PRs should be opened against all other open branches of the corresponding increment. 
This will likely result in some cases where backports are proposed that are not appropriate, in which case they can be closed. 

1. Patch: Backport to all `{x}.{y}.x` branches and all `{x}.x.0` branches.
2. Minor: Backport to all `{x}.x.0` branches.
3. Major: No backports.


### Milestones

Each branch therefore always has an "active" milestone associated with it, which corresponds to the next final release
on that branch. If we don't wish to make any more releases from a branch, we should delete it.

Each PR's milestone should reflect active milestone of the branch it targets.

### Changelog

Each PR should add or edit a file in a directory full of files corresponding to unreleased changes, [like matplotlib does](https://matplotlib.org/devel/contributing.html#contributing-pull-requests). During a final release, these items are deleted
from that file and compiled to a changelog file for that release. All of these files are included in the master changelog.

The changelog entries should be kept in chronological order, instead of semver ordering.

## Example

I went back and looked at all our tags since `v1.1.0` to see if I could create a branch diagram for them (using [`gitgraph.js`](https://github.com/nicoespeon/gitgraph.js/)) if we had been using the technique I proposed above. I don't include any commits, besides releases and merges. Also, I designate still open branches by giving them each a final commit at the end. So this would be under the assumption that the only version branches open in the repo are `master`, `2.x.0`, `2.1.x`, and `1.2.x`. ([src](https://codepen.io/saulshanabrook/pen/xxwryBa?editors=1010)). 

![](https://gist.githubusercontent.com/saulshanabrook/6d92df6e1872a5560674e097efd4abf3/raw/1e4f533196d24e9db9955dc8c0ba487e0633edc7/codepen----gitgraph-js-playground%2520(2).svg)

## Division of labor

There are many moving parts to the proposal. I thought it would be helpful to lay out what would be the responsibility of the different parties, including the bots.

The "Bots" section is also a roadmap of what would need to be implemented to move forward on this.

### Pull request author

**Semver Label**: Make sure pull request has appropriate semver label.
You can set it by either adding a commit with `semver:patch`, `semever:minor`, or `semver:major`, or setting the label in GitHub.

**Changelog entry**: Add a new markdown or RST file in `docs/source/changes/new`. Use the current data and some rough title for the filename, so it is unique. If you want it to be under a subheader, make a subdirectory for that. Some common ones are `Bug fixes`, `For developers`, `User-facing changes`. If your change is small, just make it a single bullet in a list. 


**Milestone**: Don't touch this, it will be set automatically.

**Branch base**: Normally don't touch this. However, if this PR is not meant for the latest release, but instead only for a backport to an older release, set the branch base to correspond to the branch you want to merge it against. For example if you have a fix only for the next 1.2.x release, but the latest semver release is 2.1.2, then use this label and set the base branch to `1.2.x`.


### Pull request merger

**Semver Label**: Verify the correct semver label is applied to the change.

**Changelog entry**: Verify that any changes add or change an existing changelog entry.

**Review backports**: After you merge it, review all the backport PRs that were created and merge them if appropriate. Close any that are not relevent. Also for any backports the bot failed to make automatically, make them manually if they are necessary.

### Release Manager

To make a release go to {as yet unspecified page we will build} and you will see a list of all the open branches. Each branch will show you the number of commits since the last release on that branch. Also on each branch will be buttons for each of the releases you can make from that branch. Any branch which has a release ongoing (currently running) will show that. You can also delete any version branch from this UI where the last commit was a final version.



### Bots


**Semver label**: Whenever a PR has new commits, scan them for the semver label names in the messages, and if it finds any merge it with the existing, choosing the more breaking. Also look at special label like `feature:Bug` (patch) and `feature:Enhancement` (minor).


**Semver check**: Fail (and don't allow merging on this failure) on any PR that doesn't have one, and only one, of the `semver:patch`, `semver:minor`, `semver:major` labels.

**Create backports**: After a PR is merged into the `master` brnach, create backports for that release. It should target all other branches of the same increment according to the "PR Backports" logic above.


**Base check**: Verify that the semver label corresponds to the increment of the branch of the base, if it isn't master.


**Update/create milestone**: Set the milestone to the next final release of the base branch. Update after every change of base branch and after every commit on the base branch. Create the milestone if it does not exist.

**Do release**:  This should be an action with an API endpoint. It is the most complicated and involved action. It takes place in a number of stages:

1. Input/pre-release check
2. Bump JS and push release
3. Create python release and test (optional)
4. Push python python release
5. Create new branches and create merge commits (on final release)
7. Create PRs to other repos for new version (on final release)

It takes three inputs, the branch you are releasing from, whether it's a pre release, and whether to force release without testing. If it is a pre-release, it should be one of `rc`, `beta`, `alpha`.

Before starting it checks to make sure the branch is version branch and that the pre release is valid. You can skip pre release phases, but you cannot go backwards.
This means if you just did a beta, you cannot do an rc, and if you just did an rc, you cannot do a beta or alpha.

Next, it will checkout the branch in question and create a clean environment. Then it will run the appropriate `jlpm bumpversion` command (these will need to be updated) to create and publish the packages. 

Then it will publish all the JS packages `npm run publish:all`.

Next it will run the end to end tests in a clean environment, if we are not doing a force release, (not the normal unit tests. This let's us publish even if these are failing). If these fail it will push what the JS version changes, but not the python one and exit.

If they succeed, it will upload the wheel to python and push all tags and commits.

Now, if this was a final release, it has some more work to do! First, it will try to merge this release into another branch, as the "Branch Merging" logic dictates above. Then create new branches according to the "Branches" logic above. Push all of that.

Then it will open PRs to the cookiecutter repos, if this was the latest release, to update them.

For any type of release, it will also open a PR against the conda forge repo, to release this version. It will create it on the same branch as the branch we made the release on in JupyterLab.


## Open questions

1. How do we deal with changelogs properly? Where do we deploy them from?

## Further work:

**Changelog bot**: Bot that helps you auto generate changelog entries from git commits or PR descriptions. Comment `bot:generate-changelog` in the PR to create one from the github issue contents. It will replace/create a changelog file using the title of the PR and the issue number. 
