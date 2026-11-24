
# Jupyter Development Cycle

The goal of this document is to outline a development cycle for JupyterLab which makes it very easy to do releases. As [documented in this issue](https://github.com/jupyterlab/jupyterlab/issues/8195), it's currently a quite laborious and specialized process. If we can make releases easier to manage, and push any of the hard work around so it's tackled by the authors of the PRs instead of the release managers, we can release more easily and free up core developer time for other matters.

This is meant to support our existing release cycles, not change them, but just provide some standardization and tooling to aid us in keeping to them.

## Assumptions

We start with a list of assumptions/guarantees to constrain the possible space of solutions. 

You can consider these in addition to the [SemVer 2.0.0](https://semver.org/) spec, having more to do with the relations between the code evolution between multiple versions. They assume we are already following SemVer.


**alpha, beta, rc**: Each release goes through some optional number of alpha, beta, and RC release, before the final. For some final release `{x}.{y}.{z}` it can be modeled with this state machine:

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

**Single Active**: No commits will be queued up for a release until the previous increment was fully released
(this also falls out of the above assumption). 

* Patch: No commits towards `{x}.{y}.{z}` till `{x}.{y}.{z-1}` final is released.
* Minor: No commits towards `{x}.{y}.0` till `{x}.{y-1}.0` final is released.
* Major: No commits towards `{x}.0.0` till `{x-1}.0.0` final is released.

The last two means you have to totally finish a release on one branch before you start on the next one. For example, it would be illegal to have releases in this order: `1.2.0a0`, `1.3.0a0`, `1.2.0`, then `1.3.0`. However, you could have `1.2.0a0`, `1.1.1a0`, `1.2.0`, then `1.1.1`, because these would be on different branches, `1.x.0` and `1.1.x`.

**JavaScript versions In Sync** We are OK always keeping the JS version bumps in sync. Meaning that if we do a major release of the Python package we also do a major release of all JS versions.

## Strategy

Based on these assumptions we can create a consistent branching strategy.

### Branches

Each branch should be aligned to different releases:

1. Patch: `{x}.{y}.x` branches.
2. Minor: `{x}.x.0` branches. After final release `{x}.{y}.0` create new patch `{x}.{y}.x` branch.
3. Major: `master` branch. After release `{x}.0.0` create new minor `{x}.x.0` branch and new patch `{x}.0.x` branch.

Each increment has a corresponding "latest" branch for the greatest working version. For example with two branches `2.x.0`, `1.x.0` the "latest" minor branch is `2.x.0`. The latest major branch is always `master`.

*Note: We could instead have separate branches for each version, but this isn't necessary if we are going by the **Single Active** assumption above.*


### PR SemVer Tags

Each PR should be tagged with one of three tags `semver:patch`, `semver:minor`, `semver:major` before it is merged. We could do this manually or by possibly giving a first guess [using type analysis](https://api-extractor.com/) or some commit message keywords. We should have a bot that blocks merging if one of these is not added.

If you have change that is *only* a backport, and should not appear in master, then you can target that branch as the base of this merge.

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

If there are no new changelog entries, we should not be able to make a release.

The changelog entries should be kept in chronological order, instead of SemVer ordering.

## Example

I went back and looked at all our tags since `v1.1.0` to see if I could create a branch diagram for them (using [`gitgraph.js`](https://github.com/nicoespeon/gitgraph.js/)) if we had been using the technique I proposed above. I don't include any commits, besides releases and merges. Also, I designate still open branches by giving them each a final commit at the end. So this would be under the assumption that the only version branches open in the repo are `master`, `2.x.0`, `2.1.x`, and `1.2.x`. ([src](https://codepen.io/saulshanabrook/pen/xxwryBa?editors=1010)). 

![](https://gist.githubusercontent.com/saulshanabrook/6d92df6e1872a5560674e097efd4abf3/raw/1e4f533196d24e9db9955dc8c0ba487e0633edc7/codepen----gitgraph-js-playground%2520(2).svg)

## Division of labor

There are many moving parts to the proposal. I thought it would be helpful to lay out what would be the responsibility of the different parties, including the bots.

The "Bots" section is also a roadmap of what would need to be implemented to move forward on this.

### Pull request author

**SemVer Label**: Make sure pull request has appropriate SemVer label.
You can set it by either adding a commit with `semver:patch`, `semever:minor`, or `semver:major`, or setting the label in GitHub (optionally [using a bot](https://github.com/jupyterlab/jupyterlab/blob/master/CONTRIBUTING.md#tag-issues-with-labels)).

**Changelog entry**: Add a new markdown or RST file in `docs/source/changes/new`. Use the current data and some rough title for the filename, so it is unique. If you want it to be under a sub-header, make a subdirectory for that. Some common ones are `Bug fixes`, `For developers`, `User-facing changes`. If your change is small, just make it a single bullet in a list. 


**Milestone**: Don't touch this, it will be set automatically.

**Branch base**: Normally don't touch this. However, if this PR is not meant for the latest release, but instead only for a backport to an older release, set the branch base to correspond to the branch you want to merge it against. For example if you have a fix only for the next 1.2.x release, but the latest SemVer release is 2.1.2, then set the base branch to `1.2.x`.


### Pull request merger

**SemVer Label**: Verify the correct SemVer label is applied to the change.

**Changelog entry**: Verify that any changes add or change an existing changelog entry.

**Review backports**: After you merge it, review all the backport PRs that were created and merge them if appropriate. Close any that are not relevant. Also, for any backports the bot failed to make automatically, make them manually if they are necessary.

### Release Manager

Find the pull request to release the version you want and merge it. This will trigger the release of the packages. There should be different pull requests for each in progress branch for the different types of next release, like `alpha`, `beta`, `rc`, and `final`.

Once this release has been done, a list of open PRs will be posted to this PR, for any additional merges that need to happen in other repos. Also, you should delete the release branch if this was a final release and you don't want to do any more releases off of this branch.


### Extension Authors

Be sure to allow multiple major versions of a package, like `^2 || ^3` if they are both compatible. We should be clear about documenting this so extension authors
can release extensions that are compatible with multiple major versions of JupyterLab.


### Bots


**SemVer label**: Whenever a PR has new commits, scan them for the SemVer label names in the messages, and if it finds any merge it with the existing, choosing the more breaking. Also look at special label like `feature:Bug` (patch) and `feature:Enhancement` (minor).


**SemVer check**: Fail (and don't allow merging on this failure) on any PR that doesn't have one, and only one, of the `semver:patch`, `semver:minor`, `semver:major` labels.

**Create backports**: After a PR is merged into the `master` branch, create backports for that release. It should target all other branches of the same increment according to the "PR Backports" logic above.


**Base check**: Verify that the SemVer label corresponds to the increment of the branch of the base, if it isn't master.

**Update/create milestone**: Set the milestone to the next final release of the base branch. Update after every change of base branch and after every commit on the base branch. Create the milestone if it does not exist.

**Changelog Release Check**: On each release PR, fail if there are no new changelog entries in the branch.

**Create Release PR**: After a new release is successful or when a new version branch is created, create other branches, in a fork of this repo, for each possible new release type. Run the command to bump all the JS versions properly for that release type, without actually publishing those versions. Also bump the Python version, without releasing. Then open a PR to merge that branch into the original branch. We should also run the command to consolidate the documentation to a new release file.

**Test Release PR**: On each release PR, run a special test for verifying the release works. This works by running a Verdaccio server, publishing the NPM packages to that server, and then installing the Python package with that proxy server. Then a number of integration tests are run, like opening a notebook and running some cells. It should persist these built packages as artifacts on GitHub actions.

**Do release**: After a release PR is merged, pull in the artifacts from the release PR and publish them to NPM and PyPi. Once that is successful it will push back tags for that release to the GitHub merge commit. 


**After final release, create new branches**: Once new tags have been pushed for a final release, create new branches based on the "Branches" logic above.

**After latest final release, update other repos**: After a final release that is the latest release, by SemVer, open a PR to each cookiecutter repos, and other extension repos, to upgrade them. Post a link to these on the release PR.

**After release, create conda packages**: After any release, create a PR against the conda forge repo to release that version. It will create it on the same branch as the branch we made the release on in JupyterLab, on some fork of that repo. Post a link to this on the release PR.


## Open questions

1. How do we deal with changelogs properly? Where do we deploy them from?

## Further work:

**Changelog bot**: Bot that helps you auto generate changelog entries from git commits or PR descriptions. Comment `bot:generate-changelog` in the PR to create one from the GitHub issue contents. It will replace/create a changelog file using the title of the PR and the issue number. 
