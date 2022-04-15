## Proposal Title: Auto-filled; Maximum of 60 characters, including spaces.

Jupyter Notebook maintenance and community support.

## Amount Requested: Total budget amount requested in USD, including indirect costs; this number should be between $100,000 USD and $400,000 USD total costs over a two-year period.

$400,000 USD

## Proposal Summary/Scope of Work: Provide a short summary of the work being proposed (maximum of 500 words).

JupyterLab and the Classic Notebook are the two major user interfaces to manipulate Jupyter notebook documents. This document format is popular within the scientific community because it brings code, data analysis, and visualization together in one document.

This proposal is for the upcoming major version of the Classic Notebook that will be built with JupyterLab plugins that use newer web technologies. The three key ideas approved in the related migration enhancement proposal are:

1. Document-centric user experience
2. Extensions are critical to the community
3. Existing educational content relies on the current Notebook experience

We will try to minimize the user interface changes although new features will require adaptation. The extension API will be totally different.

The backlog of issues is growing because maintenance is done by only a couple of volunteers during their spare time. It is important to address this backlog by supporting extensions migration and by anticipating new user issues for the new software versions.

To mitigate those points, the actions in the grant frame can be grouped into two categories: documentation and code base. Here are the lists of envisaged actions in priority order.

- Documentation
  - Generate screencasts automatically.
  - Today the screencasts are recorded manually and published on YouTube. This complicates their updates, their translation and their availability for educators.
  - To produce screencasts, we will create a set of helpers to emulate keyboard and mouse interactions (to be published as a stand-alone package to allow its usage in other projects). Then, we will need to define the video scenarios. Finally, we will set up an automatic workflow to generate the videos.
  - Refactor the existing documentation, focusing on:
    - Centralize documentation that is currently spread across multiple websites
    - Focus on improving the documentation for new contributors and plugin developers starting from scratch or migrating from the old classical notebook extension paradigm.
    - Reorganizing the documentation following the four pillars approaches: tutorials, how-to guides, technical reference and explanation.
  - Set up an internationalized documentation website to gather the community around a common documentation source reducing educators' effort to produce their own contents.
  - The current tools do support internationalization. The goal will be to set up automation scripts for the internationalized documentation website publication and the documentation translation through a third-party service (like the one used for the interface translation).
  - Add interface guided tours
  - Today an extension to add interface tours exists. The goal will be to integrate it as part of the core plugin, to create meaningful tours and to document how to create new tours without coding.
- Code base
  - Support the community extensions authors to migrate their code
  - Address issues related to backward inconsistency in the new major classical notebook version
  - Reduce the issues backlog focusing on bug fixes and features requested by the biomedical community based on the 2021 survey; at the time of this proposal writing, the document generation features and easier extension creation are the candidates.

## Value to Biomedical Users: Describe the expected value of the proposed work to the biomedical research community (maximum of 250 words).

JupyterLab and Notebook are primary tools used for biomedical science education, research, and manufacturing. Their interface provides a set of tools allowing users to work with code and data in a common document. Jupyter’s growth in schools, universities and laboratories speak to the value of these technologies in science.
Moving to newer technologies for the classical notebook is required to ensure the maintenance cost stays manageable and the tool will keep up with new browser features and requirements.
Keep improving the tool, focusing on research code documentation, to facilitate sharing research results and to foster an understanding of new discoveries.

## Open Source Software Projects: Indicate the number of software projects involved in your proposal (up to five).

There are 5 projects involved: JupyterLab, Notebook, Lumino, JupyterLab server and Jupyter server. JupyterLab is the main target. It builds on Lumino, JupyterLab server and Jupyter server. The upcoming major version of Notebook will be based on JupyterLab.

| Software project name | Main code repository | Homepage |
| --- | --- | --- |
| JupyterLab | https://github.com/jupyterlab/jupyterlab |  https://jupyterlab.readthedocs.io/ |
| Notebook | https://github.com/jupyter/notebook/ | https://jupyter-notebook.readthedocs.io/ |
| Lumino | https://github.com/jupyterlab/lumino/ | https://lumino.readthedocs.io/ |
| JupyterLab server | https://github.com/jupyterlab/jupyterlab_server | https://jupyterlab-server.readthedocs.io/ |
| Jupyter server | https://github.com/jupyter-server/jupyter_server/ | https://jupyter-server.readthedocs.io/ |


## Landscape Analysis: Briefly describe the other software tools (either proprietary or open source) that the audience for this proposal primarily uses. How do the software project(s) in this proposal compare to these other tools in terms of user base size, usage, and maturity? How do existing tools and the project(s) in this proposal interact? (maximum of 250 words)

Other known desktop tools used by the scientific community to document code and visualized results are RStudio, JetBrains PyCharm/DataSpell, VSCode or nteract. Some tools are also available from online services like Google Colab(oratory) or CoCalc. Out of those three, RStudio is the most used tool in the scientific biomedical community as it supports R and is well established.
Lately VSCode has invested lots of time integrating them within the nowadays most popular open-source Integrated Development Platform. So their potential user base is bigger than Jupyter. But having a broader audience the extensibility of the tool is more constrained than the more dedicated Jupyter tools.
Except nteract and VSCode, the other tools are being developed by companies that provide paid versions. That financial source helps address bug fixes and reduce the backlog compared to the fully open source community-driven Jupyter tools.

## Category: Choose the two categories that best describe the software project(s) audience:

> TBC

- Bioinformatics
- Machine learning and data analysis

## Previous CZI funding:

- Did you previously apply for funding for this or a related proposal under the CZI EOSS program? Select Yes or No.
  - No - but there have been other proposal funded by CZI EOSS for Jupyter tools ([JupyterHub Fellow Program - EOSS-0000000142](https://chanzuckerberg.com/eoss/proposals/jupyterhub-contributor-in-residence-program/), [Real-Time collaboration - EOSS2-0000000084](https://chanzuckerberg.com/eoss/proposals/real-time-collaboration-in-jupyter/), [Accessibility - EOSS4](https://chanzuckerberg.com/eoss/proposals/inclusive-and-accessible-scientific-computing-in-the-jupyter-ecosystem/)
)

- Have you previously received funding for this proposal under the CZI EOSS program? Select Yes or No.
  - No
