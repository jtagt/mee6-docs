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

# Automatic Installation
Download `install.sh` from this repo.

Use `chmod` to make the installer executable:


`chmod 755 install.sh`

Then run it:

`./install.sh`

You can then remove it with:

`rm install.sh`.

# Alias Config
Now that all the dependencies are installed we can move onto confgiuring some of the variables.
```
export REDIS_URL=redis://localhost
export OAUTH2_CLIENT_ID=Discord client ID for your bot
export OAUTH2_CLIENT_SECRET=your Discord bot's client secret
export MEE6_TOKEN=Your Discord bot token
export OAUTH2_REDIRECT_URI=http://localhost:5000/confirm_login (change to your domain if needed.)
export MAL_USERNAME=username for account on http://myanimelist.net
export MAL_PASSWORD=password for above site
export TWITCH_CLIENT_ID=client ID for a twitch app
export GOOGLE_API_KEY=a youtube api key
export SECRET_KEY=1111 ***Change to a longer code, preferably longer than this***
```
If you are fine with not having some features work, simply remove the variable value and leave the empty assignment.

Now do:

`cd ~ && nano .bashrc`

Press Control-V to go to the end of the document (don't remove anything), and **paste in these variables**. Save and exit.
(To exit, press Control-X, then Y then Enter.)

