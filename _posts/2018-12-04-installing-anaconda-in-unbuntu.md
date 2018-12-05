---
layout: post
title:  "Installing Anaconda in Ubuntu"
date:   2018-12-04 22:32:13 -0500
categories: anaconda data-science
---
## Why I chose to install Anaconda in Ubuntu Linux

I want to start learning data science and there are a bunch of resources I want to try out (more on those another time). I watched the first two videos of Kevin Markham's [Data School video series about pandas](https://www.dataschool.io/easier-data-analysis-with-pandas/). But, in order to get going with pandas I needed to install it. He recommends using the [Anaconda distribution of Python](https://docs.anaconda.com/anaconda/) which is supposed to have the easiest package installation (numpy, pandas, etc.). From what I've read online, the ease of installation argument is less important for Linux machines where you have admin privileges than for, say, Windows machines where you don't. However, I figured I'd go with the recommended distribution so I could eliminate potential problems and also because I may end up working on a Windows machine later on, so I'd prefer the cross-platform ease of installation of Anaconda. 

## The PATH variable problem that tripped me up

I found installing Anaconda to be really easy. I just went to the [installation page](https://docs.anaconda.com/anaconda/install/), chose the [Installing on Linux](https://docs.anaconda.com/anaconda/install/linux/) option and followed the instructions, including verifying the MD5 hash.

I followed the [FAQ](https://docs.anaconda.com/anaconda/user-guide/faq/#distribution-faq-linux-path)'s advice and let the installer add the path to Anaconda to my system's PATH variable. This works fine from Anaconda's perspective, but it changes the default system Python to the version of Python installed with Anaconda. In other words, if you type `python` at the command line, you'll be running the version of python in the Anaconda directory instead of the default directory (in my case, `/usr/bin/python`).

After way too much time trying to resolve this, the solution I stumbled on turned out to be very simple. Here's the code block that Anaconda added at the end of my `~/.bashrc` file:

```bash
# added by Anaconda3 5.3.1 installer
# >>> conda init >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$(CONDA_REPORT_ERRORS=false '/home/seth/anaconda3/bin/conda' shell.bash hook 2> /dev/null)"
if [ $? -eq 0 ]; then
    \eval "$__conda_setup"
else
    if [ -f "/home/seth/anaconda3/etc/profile.d/conda.sh" ]; then
        . "/home/seth/anaconda3/etc/profile.d/conda.sh"
        CONDA_CHANGEPS1=false conda activate base
    else
        \export PATH="/home/seth/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda init <<<
```

The `\export PATH="/home/seth/anaconda3/bin:$PATH"` prepends the Anaconda directory to the beginning of your PATH variable's existing values. This is great, except that it means that when the system looks for the Python binaries, it finds them in the Anaconda directory and stops looking there.

The solution I came up with (thanks to Piotr Dobrogost's comment on [this Stack Overflow question](https://stackoverflow.com/questions/24664435/use-default-python-rather-than-anaconda-installation-when-called-from-the-termin)) is to add the default Python directory to the beginning of the PATH variable, prior to the Anaconda directory.

To accomplish that, here's the extra two lines of code that I added **after** the Anaconda code block:

```bash
# added by Anaconda3 5.3.1 installer
# >>> conda init >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$(CONDA_REPORT_ERRORS=false '/home/seth/anaconda3/bin/conda' shell.bash hook 2> /dev/null)"
if [ $? -eq 0 ]; then
    \eval "$__conda_setup"
else
    if [ -f "/home/seth/anaconda3/etc/profile.d/conda.sh" ]; then
        . "/home/seth/anaconda3/etc/profile.d/conda.sh"
        CONDA_CHANGEPS1=false conda activate base
    else
        \export PATH="/home/seth/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda init <<<

# add /usr/bin to beginning of PATH so that python, python3, python2 use default system python not Anaconda python 
export PATH="/usr/bin:$PATH"
```

Is there a better, cleaner solution than this? Probably. I notice that this solution ends up putting `/usr/bin` in my PATH variable twice, which doesn't seem great. But at the moment this seems to be working, so I'm writing it up as a solution to this problem that I ran into.

## Useful commands

- `echo $PATH` will print the contents of the PATH variable to the screen. Note that directories are separated by colons.
- `source ~/.bashrc` will run your `.bashrc` file and recreate your PATH variable, although note what the Anaconda FAQ has to say about this:

> If you have any terminal windows open, close them all then open a new one. You may need to restart your computer for the PATH change to take effect. 

## Disclaimer

I'm definitely not a command line or bash expert. Your setup may be different than mine and so these instructions may not apply to you. Of course, if you notice anything that's wrong or could be improved in this post, I'd be glad to hear!
