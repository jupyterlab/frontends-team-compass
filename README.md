# Jupyter Frontends team-compass

A repository for team interaction, syncing, and handling meeting notes across the JupyterLab ecosystem.

## Weekly Jupyter Frontends team meeting
Weekly team meetings take place on the [Jupyter Zoom room](https://zoom.us/j/95228013874?pwd=Ep7HIk8t9JP6VToxt1Wj4P7K5PshC0.1) on Wednesdays at 9:00 AM Pacific Time ([your time](https://www.thetimezoneconverter.com/?t=9%3A00%20am&tz=San%20Francisco)). Minutes will be taken at [Hackmd.io](https://hackmd.io/Y7fBMQPSQ1C08SDGI-fwtg). Each meeting's minutes will be added as a comment to an issue in this project.

## Weekly Jupyter triage meeting
Weekly triage meetings take place on the [Jupyter Zoom room](https://zoom.us/j/95228013874?pwd=Ep7HIk8t9JP6VToxt1Wj4P7K5PshC0.1) on Tuesdays at 9:00 AM Pacific Time ([your time](https://www.thetimezoneconverter.com/?t=9%3A00%20am&tz=San%20Francisco)). We look at [JupyterLab issues that need triage](https://github.com/jupyterlab/jupyterlab/labels/status%3ANeeds%20Triage) and [Jupyter Notebook issues](https://github.com/jupyter/notebook/issues/). Minutes will be taken at [Hackmd.io](https://hackmd.io/HaQ3S_nPSbqaRtk9rj59iA). Each meeting's minutes will be added as a comment to an issue in this project.

Each meeting's minutes will be added as a comment to an issue in this project.

## Code of Conduct
As an official Jupyter Project, all communication across all repositories in this organization should adhere to the [Project Jupyter Code of Conduct.](https://github.com/jupyter/governance/blob/master/conduct/code_of_conduct.md)

## Contributing extensions to the JupyterLab GitHub organization

JupyterLab is built to foster a rich ecosystem of plugins. Occasionally developers of an existing JupyterLab extension will want to contribute the extension to Project Jupyter and maintain the extension in the JupyterLab GitHub organization under [Project Jupyter governance](https://github.com/jupyter/governance), which includes:

* adopting the standard Jupyter license and copyright
* adhering to Project Jupyter community guidelines
* being subject to the Project Jupyter BDFL, Steering Council, and governance.

Project Jupyter has [official guidelines](https://github.com/jupyter/governance/blob/master/newsubprojects.md) for adopting new subprojects. More specifically for contributing extension codebases to the JupyterLab GitHub organization, the process for contributing is:

1. First consider contributing the extension to [jupyterlab-contrib](https://github.com/jupyterlab-contrib)
2. If you think the extension should be considered as a core extension, post an issue on this repo describing your extension and linking to the existing code. The issue should address each point of the [criteria for subprojects](https://github.com/jupyter/governance/blob/master/newsubprojects.md#criteria-for-official-subprojects).
3. The community reviews the proposal over at least a week. In addition to the criteria listed in the Project Jupyter governance:
   1. a core maintainer will review the existing code
   2. we will also take into account how involved the extension maintainers are in the JupyterLab community
   3. we may recommend that the extension belongs in `jupyterlab-contrib`
4. If the JupyterLab maintainers decide to accept the extension into the JupyterLab GitHub organization, the process in the Project Jupyter [incorporation guidelines](https://github.com/jupyter/governance/blob/master/newsubprojects.md#incorporation) is followed. Additionally:
   1. JupyterLab maintainers and other relevant Jupyter leadership (such as BDFL) are given permission to publish the package.
   2. Extension maintainers are given admin permission on the relevant `@jupyterlab/extension` npm package. To do this, a user must be added to a team, which then has access to packages (under "Teams"):
      1. Admin logs in to https://www.npmjs.com
      2. Select avatar dropdown and go to "Profile Settings"
      3. Select the jupyterlab org
      4. Go to Members
      5. Click "Invite Members..."
      6. Add the username or email
      7. Click "Invite"
      8. Click "Continue"
