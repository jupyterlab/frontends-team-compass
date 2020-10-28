# 2020 JupyterLab User Survey

Source: https://docs.google.com/document/d/1M-Qod4nByssdZJMlQ1HGr4LkjuZS0MjriD4C93kZg9w/edit

## General

**Are you a user and/ or developer of Jupyter?**

- End User: I just use Jupyter.
- Extension Developer: I develop extensions for Jupyter.
- Core Developer: I develop Jupyter projects daily.
- Neither: I primarily use other tools.


**How frequently do you use Jupyter?**

- Daily: 4 or more hours per day.
- Daily: 3 or less hours per day.
- Weekly.
- Monthly.
- I no longer use Jupyter. 
- I have never used Jupyter. 

**How long have you been using Jupyter?**

- 2+ years.
- 1-2 years.
- 6-12 months.
- 0-6 months (welcome 😃).

**Which front end of Jupyter do you use most? (see later questions for JupyterHub)**

- Jupyter Notebook (Classic Jupyter front end, url ends with /tree )
- JupyterLab (has files/ folders on the left panel, url ends with  /lab).

**What are your go-to tools for doing data science, scientific computing, and machine learning on your laptop/desktop (non-cloud) for data science? (pick top 2)**

DROP

- JupyterLab/ Jupyter Notebook.
- PyCharm.
- Spyder.
- RStudio.
- nteract.
- VS Code.
- Zeppelin.
- Sublime Text.
- Atom.
- Emacs.
- Vim.
- iPython (in the console/terminal).
- Other  [   text_field   ].

**How do you/ your team access Jupyter (machine and/ or platform)?**

- Local machine (laptop, desktop).
- HPC or on-premise server.
- Cloud server (e.g. EC2).
- JupyterHub - in cloud.
- JupyterHub - in an on-premise server.
- Cloud service - AWS: EMR, SageMaker.
- Cloud service - Azure: Notebooks, ML Studio.
- Cloud service - Google: AI Platform, Dataproc.
- Cloud service - IBM: Watson.
- Google Colab.
- Through a 3rd party SaaS app (e.g. Observable, CoCalc)
- Through a Python virtual environment (e.g. conda, pyenv, venv)
- Don’t know how, I just go to a URL.
- Other  [  text field  ]

**What languages do you use in Jupyter?**

- Python
- R
- Julia
- Spark SQL
- SQL
- Java
- Scala
- C (and derivatives)
- JavaScript
- NodeJS
- TypeScript
- PHP
- Ruby
- Rust
- I pipe in/ wrap other languages.
- My preferred language is not supported in Jupyter.
- Other [text field]

**In which fields is your work with Jupyter situated? (select multiple):**

DROP

- Machine learning
- Education 
- Scientific computing
- Data Science
- Other [   text_field   ]

**In what ways does Jupyter support these complex, high-level tasks in your workflow?**

Higher level tasks:

- Writing and running tests for software.
- Building/compiling a software package.
- Releasing a software package.
- Deploying code in production.
- Building a machine learning or statistical model.
- Importing data
- Tidying, cleaning, preparing or transforming data.
- Doing exploratory data analysis.
- Interactive data visualization.
- Using code to think about and understand data.

Matrix columns:

- I used Jupyter often for this task without much friction
- I used Jupyter for this task, but experience a great deal of friction
- I don’t often do this taskI never do this task, and don’t expect to
- I never do this task, but expect to do so in the next year
- I use another tool for this task and wish Jupyter made this easier
- I use another tool for this task and prefer it this way

**In what ways does Jupyter support these discrete/low-level tasks in your workflow?**

Low level tasks:

- Writing/run code interactively in a notebook
- Autocompletion
- Viewing code documentation and help
- Viewing interactive charts and visualizations
- Creating interactive charts and visualizations without writing code, using a graphical UI
- Writing markdown in a notebook
- Writing standalone markdown files
- Debugging code
- Refactoring code
- Read other people’s code in notebooks
- Reading other people’s code in text files
- Using the terminal/system shell
- Using version control (git)
- Writing code in standalone source code files
- Use interactive widgets (ipywidgets, shiny)

Matrix columns:

- I used Jupyter often for this task without much friction
- I used Jupyter for this task, but experience a great deal of friction
- I don’t often do this taskI never do this task, and don’t expect to
- I never do this task, but expect to do so in the next year
- I use another tool for this task and wish Jupyter made this easier
- I use another tool for this task and prefer it this way

**What are you likely to do after using Jupyter for a project?**

- Deploy to production
- Publishing a code package (pip, npm, etc.)
- Present
- Teach
- Share
- Publish content
- Make a decision
- Leave with a greater understanding and insight about a problem or dataset

Matrix columns:

- Often
- Sometimes
- Seldom 
- Never

**Rank the following new features and capabilities that we are considering implementing in JupyterLab in order of importance (1=highest).**

- Output saved even when notebook document is closed
- Variable inspector
- Display hidden files in file browser
- Improved autocompletion (LSP)
- Enabled hierarchical sections in notebooks to be collapsed
- Slow performance of large notebooks.
- Better mobile UX for JupyterLab
- Dashboarding notebooks
- Version controlling notebooks with git
- No --user install of lab extensions
- Workspaces UI
- A classic notebook mode (one notebook per page) for JupyterLab
- Internationalization
- Accessibility
- Commenting on notebooks and text files.
- Better undo/repo support.
- Other [text input]

**What are your primary job duties when you are using Jupyter? (pick 3 maximum)**

- Data scientist.
- Data engineer.
- Scientist/ researcher.
- Professor/ instructor/ teacher.
- Financial modeler/ analyst.
- Business analyst.
- Backend engineer.
- Front end/ web development.
- DevOps.
- Infrastructure engineer/ cloud architect.
- Sysadmin.
- Other [   text_field   ]

**Select which research-based and/ or academic fields you work in. (see previous question for commercial or civil industry)**

PROPOSED TO DROP AS IT IS MOSTLY REDUNDANT WITH THE PREVIOUS

[List of academic fields]

**Which JupyterLab Extensions do you use?**

- Spellchecker
- LaTeX 
- DrawIO
- Table of Contents
- Collapsable Headings 
- Go to definition 
- Code Formatter
- Elyra
- LSP 
- JupyterHub
- Vim
- Git
- GitHub
- neptune-notebooks
- Bokeh
- ipywidgets
- FASTA
- geojson
- katex
- plotly
- vega
- voyager 
- Dash 
- ipysheet 
- Material Darker 
- Atom Dark 
- AixViPMaP 
- jupyterlab_discovery 
- jupyterlab_debugger 
- lantern 
- ML Workspace 
- scriptedforms 
- Variable inspector Dask 
- Other  [  text field  ]

**WIP: Thinking about your general “pain points,” where do you get frustrated, spend too much time, or find yourself manually extending Jupyter?**

[Was a list of items, but it may be more useful for this to be a free response.]

**Do we have your permission to potentially recontact you for a user interview when we are ready to prioritize the roadmap and dive into new feature ideas?**

Email: [   Text box   ]

## Collaboration

These notes need to be turned into questions:

Is your collaboration primarily:

Synchronous
Asynchronous

Is the physical/geographic distribution of your collaborators primarily:

Same location/office/timezone.
Different locations/offices/timezones.

What is the nascent of your collaboration:

Developing
Routine
What is the planned permanence of your collaboration:

Short term
Long term

**What is your reason for sharing a notebook with someone else? What do you need from them?**

- Share knowledge.
- Review and comment on my logic.
- Review and comment on my code.
- Formal code review on my pull requests.
- Integrate my code/ data with their downstream or upstream processes.
- Contribute some of their own code cells.
- Edit my code cells.
- Peer programming. 
- Teach.
- Deploy my code/ model/ pipeline/ dashboard.
- Other [   text_field   ]

**How do you/  your team store and share notebooks?**

- Shared file system (e.g network or HPC drive).
- Repositories (GitHub, GitLab, BitBucket).
- Jupyter Binder/ BinderHub.
- SaaS app (e.g. Google Drive/ Colab, Dropbox, Box).
- Cloud service (e.g. Alibaba ML, AWS SageMaker, Azure ML, GCP AI, IBM Watson).
- 3rd party app.
- Other [   text_field   ]

**Thinking about your “collaboration challenges,” where do you get stuck, spend too much time, or find yourself manually extending Jupyter?**

WE MAY GET MORE USEFUL INFORMATION BY CONVERTING THIS TO A FREE RESPONSE QUESTION

- Other: please let us know! [   Text box   ]
- Lacking a shared folder for the team.
- No support for our version control system.
- Managing roles and permissions (e.g. read, run, write, folder access).
- Not being able to comment on notebooks.
- Working with people in other external organizations.
- Not being able to collaborate in real-time.
- Difficulty during code review due to notebook syntax.
- Display/ run notebook without revealing underlying code.
- Knowing what packages I have installed and/ or am actually using.
- Environment configuration for users who can’t manage their own env.
- When someone sends me a notebook I have to 'reconstruct their environment.'
- When someone sends me a notebook I have to 'reconstruct their data.' 
- Extensions don’t work in non-Jupyter environments.

## Data

This section originally contained 3 questions about the data format, sources, and data pain points. It isn't clear how these questions would lead to actionable insight for JupyterLab, so we were talking about removing this section. See the above Google Doc for the original questions.

## Visualization

This section originally contained 4 questions about data visualization. It isn't clear how these questions would lead to actionable insight for JupyterLab, so we were talking about removing this section. See the above Google Doc for the original questions.

## Machine learning

This section originally contained 5 questions about machine learning. It isn't clear how these questions would lead to actionable insight for JupyterLab, so we were talking about removing this section. See the above Google Doc for the original questions.

## Workload

This section originally contained 2 questions about workload. See the above Google Doc for the original questions.
