---
layout: post
title:  "Getting Started with conda"
date:   2018-12-06 20:55:13 -0500
categories: data-science
tags:
- anaconda
- conda
---
There are some good resources for getting started with conda on the conda website:

- [conda cheat sheet](https://conda.io/docs/_downloads/conda-cheatsheet.pdf)
- [Getting started with conda](https://conda.io/docs/user-guide/getting-started.html)

Here are a few commands that I found useful as a complete newbie to conda:

Command | What it does
--- | ---
`conda info` | displays information about your setup
`conda info --envs` | lists your virtual environments
`conda create --name jupyter --python=3.7` | create a new virtual environment named `jupyter` with python version 3.7.x
`conda create --name jupyter "python>=3.7"` | same as above except python version is greater than or equal to 3.7 (in this case, has the same effect as the previous command); note that you need to use double quotes when using `>=`
`conda activate jupyter` | activate the virtual environment named jupyter; it's possible that your command might be different. You can also try `source activate jupyter` or `activate jupyter` in Windows.
`conda deactivate` | deactivate the current virtual environment; it's possible that your command might be different. You can also try `source deactivate` or `deactivate` in Windows.
`conda env remove --name jupyter` | delete the virtual environment named jupyter and everything in it
`python -V` | check which version of python you are using
`which python` | find the path to the version of python you are using
