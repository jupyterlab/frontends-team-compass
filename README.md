# team-compass

A repository for team interaction, syncing, and handling meeting notes across the JupyterLab ecosystem.


## Process for adding new projects

If you have an existing JupyterLab extension, or would like to create one, this is the process
for doing so on the core `jupyterlab` organization:

1. You post an issue on this repo describing your extension and linking to any existing code. You should describe who will maintain it and why it will be useful to the community.
2.  A core maintainer reviews any existing code as a sanity check.
3.  Relicense any existing code to https://github.com/jupyterlab/team-compass/blob/master/LICENSE.
4.  Give the community roughly a week to comment on the proposal.
5. Pending any objections, create a new repository.
   1. Give any maintainers admin privileges on that repo
   2. Add them as maintainers on the relevant NPM packages. A user must be added to a team, which then has access to packages (under "Teams").
      1. Admin logs in to https://www.npmjs.com
      2. Select avatar dropdown and go to "Profile Settings"
      3. Select the jupyterlab org
      4. Go to Members
      5. Click "Invite Members..."
      6. Add the username or email
      7. Click "Invite"
      8. Click "Continue"
