---
layout: post
title:  "Developing with remote python environment"
date:   2021-11-22 12:15:00 +0100
categories: python, pycharm, remote, conda
---

# Install conda (miniconda) on remote machine
```
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
$ bash Miniconda3-latest-Linux-x86_64.sh -b
$ echo 'export PATH="/path/to/miniconda3/bin:$PATH"' >> ~/.bashrc
$ conda init
```

# Create new conda environment
```
$ conda create -n <environment_name> python=<python_version>
```

# Open your project locally
- Start PyCharm
- Optionally, clone your project from git `git clone /path/to/githubproject.git`
- Open the project in PyCharm

# Connect to conda environment
- Navigate to Preferences > Project: <Your Project Name> > Python Interpreter
- In the Python Interpreter dropdown, select Show All
- Press the plus icon
- Select SSH Interpreter
- Configure HostName, Username and Port and click Next
- In the interpreter dropdown, select our previously created conda environment: /path/to/miniconda3/envs/<environment_name>/bin/python
- In the sync folders dropdown, select /path/to/home/Development/<your_project>
- Press Finish
- Press the edit icon
- Click the 3 dots next to Deployment configuration
- Select the Excluded Paths tab and specify any data folder, so that your data & datasets are not automatically synced to the server. Otherwise, executing code might take a long time.
- Press Ok, Ok, Ok, Select our created Python Interpreter in the dropdown, Apply and Ok
- Finished! Try using the Python Console to confirm everything works :)
