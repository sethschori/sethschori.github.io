---
layout: post
title:  "Getting Started with Jupyter notebook"
date:   2018-12-07 11:30:00 -0500
categories: data-science
tags:
- jupyter
---
Here are the steps I took to get started with Jupyter notebook:

## Make and activate a new conda virtual environment with Python 3

```shell
conda create --name jupyter "python>=3"
```

This creates a new conda virtual environment named `jupyter` with Python 3 installed. As of December 2018, the latest version is 3.7.1, which is the version that gets installed with the above command. And if the latest version when you're reading this happens to be 3.8.2, then you'll have 3.8.2 in your virtual environment.

```shell
conda activate jupyter
```

This activates the new `jupyter` virtual environment.

## Configure the environment to allow Python 3 for the Jupyter notebooks

When I first launched Jupyter, I found that I could only create Jupyter notebooks using Python 2. Python 2 is old and approaching the end of its life, so I wanted to be able to create Jupyter notebooks that use Python 3; plus, I prefer using Python 3's syntax.

Thanks to [this Stack Overflow answer](https://stackoverflow.com/a/30492913), I discovered that a couple of more lines of configuration did the trick: 

```shell
conda install notebook ipykernel
ipython kernel install --user
```

The first line installs the notebook and ipykernel packages into the active virtual environment (ipython is jupyter's old name).

I don't really understand the second line, but I believe it has something to do with registering the ipython kernel to make it available to Jupyter, and the `--user` flag just means that you're doing it only for your user account.

## Make a directory and optionally initialize git

I think it's a good idea to have a directory for one's Jupyter notebooks so that they're in one place (unless you want to file them in different directories). It also allows you to then use git on the directory for version control.

I made a directory called `jupyter`, but choose whatever directory name you want.

```shell
mkdir jupyter
cd jupyter
```

You can also (optionally) initialize git in order to start using version control on the directory:

```shell
git init
```

I'm not going to cover how to use git because that's beyond the scope of this post, but there are some resources [here on GitHub's site](https://try.github.io/).

## Start the Jupyter notebook server and make a notebook

```shell
jupyter notebook
```

This starts the server locally on your computer and automatically opens up a browser tab pointing to `http://localhost:8888/tree`, which is the default location and port (8888) for Jupyter notebooks.

If you already have created any files or notebooks in the directory then you'll see them there, but if not you'll see an empty directory.

In either case, you can make a new Jupyter notebook right in the browser. In the upper-right corner of the page you'll see a dropdown menu called `New`. If you click on that you should see an option to create a new notebook in whatever language(s) are available in this virtual environment. If you followed the directions above and they (hopefully) worked for you, then you should have an option to create a notebook using Python 3 and possibly Python 2. If you have other languages, you might see options to create notebooks in R, Julia, or perhaps other languages.

## Start using the notebook

Your new notebook will be blank and look something like this:

![blank Jupyter notebook](/img/jupyter_new.png)

Click on `Untitled` and give your notebook a name, such as `hello_world`.

Click in the first blank, gray rectangle (called a cell) and enter some Python code, such as this:

```python
squares = [num ** 2 for num in range(10)]
print("Hello world")
print(f"Here is a list of squares: {squares}")
```

Type SHIFT-ENTER to execute the code. Your notebook should now look something like this:

![Jupyter notebook with some Python code](/img/jupyter_hello_world.png)

Click the first icon which looks like a floppy disk to save your notebook (Jupyter will also autosave your notebook).

You can now optionally commit your changes to version control if you'd like.

Congratulations, you installed, configured, and created your first Jupyter notebook!
