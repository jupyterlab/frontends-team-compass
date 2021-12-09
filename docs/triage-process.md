An issue that is **ready** can be picked up and worked on with high confidence that we will accept it into the project.

# Definition of ready

**All requested information, where applicable, is provided.** From the templates in JupyterLab’s issues:

For a **bug**:

* Description, preferably including screen shots
* Steps to reproduce
* Expected behavior
* Context: OS, browser, JupyterLab version, relevant output

For a **feature request**:

* Description of the problem
* Description of the proposed solution
* Additional context

**The item should represent real, relevant, feasible work**. In short, if a knowledgeable person were to be assigned this item, they would be able to complete it with a reasonable amount of effort and assistance, and it furthers the goals of the Jupyter project.

* Issues should be unique; triage is the best time to identify duplicates.
* Bugs represent valid expectations for use of Jupyter products and services.
* Expectations for security, performance, accessibility, and localization match generally-accepted norms in the community that uses Jupyter products.
* The item represents work that one developer can commit to owning, even if they collaborate with other developers for feedback. Excessively large items should be split into multiple items, each triaged individually, or into [team-compass](https://github.com/jupyterlab/team-compass) items to discuss more substantive changes.

# Triage process

A bot applies the `Status: Needs Triage` label to all new bugs and enhancement requests as they are filed.

On a regular basis, Jupyter contributors should review JupyterLab items tagged with `Status: Needs Triage`, starting with the oldest, and determine whether they meet the definition of ready.

Once triaged, if the item is ready, the reviewer should remove the `Status: Needs Triage` label; no additional label is required. If there is not enough information in the item as filed, the triage reviewer should apply the `Status: Needs Info` label and leave `Status: Needs Triage` in place. If an item has remained in `Status: Needs Info` for more than 14 days without any follow-up communication, the reviewer should apply `status: Blocked`. A blocked item should be closed after another 14 days pass without a reply that unblocks it.

Our expectation is that every new item should be examined within a week of its creation.

