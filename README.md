# Mee6 Selfhosting Guide

NOTE: This only words with Python 3.5/3.6, but we will use Python 3.5. **DOES NOT WORK WITH PYTHON 2 OR PYTHON 3.4**

We will be using Ubuntu 14 for this tutorial, but linux systems that use `apt` package manager like Mint, CentOS, Debian, and Raspbian should work fine.

There's nothing wrong with using a virtual machine.

You can install automatically or manually, see below.
# Manual installation

Install python3, pip3, redis, and nginx:

`apt install -y python3 python3-pip redis-server nginx`

Then, discord.py:

`python3 -m pip install -U https://github.com/rapptz/discord.py/archive/async.zip#egg=discord.py[voice]`

The next thing we need to do is clone this repo from github:

`git clone https://github.com/jtagt/mee6/`

Then, we need `pip` to install the necessary packages for the website script and the chat script. First, we will install for the website script:

`cd mee6/website && pip3 install -r requirements.txt`

Then we will do the same command, but for the chat script:

`cd ../chat-bot && pip3 install -r requirements.txt`
