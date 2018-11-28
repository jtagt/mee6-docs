**PLEASE VISIT https://jtagt.github.io/mee6-docs/ FOR CLEANER DOCS**

Need help? We have a support server! https://discord.gg/WD4pssB

If you're reading this on GitHub pages, remember that this is the docs for `https://github.com/jtagt/mee6`.

Update: It looks like we're the official selfhosting repo for MEE6! Hope to see more traffic soon...

NOTE: This only words with Python >= 3.5, but we will use Python 3.5. **DOES NOT WORK WITH PYTHON 2.x OR PYTHON 3.4**

We will assume you use `bash` for this tutorial, but Linux systems that use `apt` as a package manager like Mint, CentOS, Debian, and Raspbian should work fine.

VMs (Virtual Machines) are fine, but WSL (Windows Subsystem for Linux, if you don't already use it don't try) is not recommended.

You can install automatically or manually, see below.

# Installation

## Manual installation

If you prefer a more hands-on installation, pick the manual route. If you want full gusto and minimal things to go wrong, go ahead and use our install script, see Automatic Installation.

### Package Installation

In order to properly install packages, you first need to update your package repositories:

`sudo apt update`

Then, install Python 3, it's package manager (`pip3`), and a web server (we'll use `nginx`). You'll also need `redis`. The installation will also be easier if you install `git` (see below why):

`sudo apt install -y python3 python3-pip redis-server nginx git`

With the installation of packages out of the way, we need to install the wrapper for the Discord API. Hence...

`python3 -m pip install -U https://github.com/rapptz/discord.py/archive/async.zip#egg=discord.py[voice]`

### Obtaining a Copy of This Repo

If you installed `git` above, you can clone this repo:

`git clone https://github.com/jtagt/mee6/ && cd mee6/`

If you did not install `git`, do not fear, the repo is still accessible. Simply point your download agent (graphical, command line, whatever) at this location:

`https://www.github.com/jtagt/mee6/archive/master.zip`

If you need a download agent, you can install `wget` and use it:

`sudo apt install wget && wget https://github.com/jtagt/mee6/archve/master.zip`

If you take the `.zip` route, you will have to, of course, unzip the archive. If you haven't installed `unzip`, do so now with `sudo apt install unzip`. Armed with this tool, create a folder for the archive and extract:

`mkdir mee6 && mv master.zip mee6/ && cd mee6/`

`unzip master.zip`

If anything flops at this point, try again, and if things still go wrong, we have a problem, and you should join our Discord for help or open an issue here. Assuming things go right, you can get rid of the archive: 

`rm master.zip`

### Installing More Packages

Then, we need `pip` to install the necessary packages for the website script and the chat script. First, we will install the packages for the website script:

`cd website/ && pip3 install -r requirements.txt`

Then repeat, but for the bot script:

`cd ../chat-bot && pip3 install -r requirements.txt`

# Automatic Installation

### Obtaining a Copy

Clone this repo (See above in Manual Install for info on obtaining a copy of the repo) and, if you are not already in it, enter the `mee6` directory.

Then run the installer (feel free to read it first):

`./install.sh`

If all goes well, you can then remove it with:

`rm install.sh`.

# Alias Config

Now that all the dependencies are installed we can move onto confgiuring some of the variables.
```
export REDIS_URL=redis://localhost
export OAUTH2_CLIENT_ID=#Discord client ID for your bot
export OAUTH2_CLIENT_SECRET=#your Discord bot's client secret
export MEE6_TOKEN=#Your Discord bot token
export OAUTH2_REDIRECT_URI=http://localhost:5000/confirm_login #change to your domain if needed
export MAL_USERNAME=#username for account on http://myanimelist.net
export MAL_PASSWORD=#password for above site
export TWITCH_CLIENT_ID=#client ID for a twitch app
export GOOGLE_API_KEY=#a youtube api key
export SECRET_KEY=1111 #Change to a longer code, security is important
```

The variables printed above are also in `exports.sh`, which is included with this repo. Open that file. See below on what to do next.

In the above code block, the `#` and everything after it on the same line is commented out. In order to set a value, add its value in after the equal sign, *before the #*. 

### Setting Variables

You need not touch `REDIS_URL`, unless you have Redis installed elsewhere and you want to use that other machine as a database. Locally hosting the database is usually fine.

Then, replace `OAUTH2_CLIENT_ID` with the user ID of your Discord bot. If you do not know how to get this, you can easily get it by typing in a ping for your bot (**Don't send it yet**), then adding a backslash (`\`) and sending it. The numbers you get are the Client ID.

The `OAUTH2_CLIENT_SECRET` variable must be set to your Discord Bot secret. This is accessibke on your Discord Developer dashboard, at `https://discordapp.com/developers/applications/me`. Select the application that matches your bot, and find `Secret`.

`MEE6_TOKEN` is the last piece for a minimal bot. It is your Discord bot's token, which is it's replacement for a user and password to get into Discord. Revavigate to your Discord Apps dashboard (again, it's at `https://discordapp.com/developers/applications/me`), find your bot application, and find `Bot Token`. Press `Click to Reveal`, and you have your client token.

The next value, `OAUTH2_REDIRECT_URI` is the location of your web dashboard for MEE6. We're using a localhost port, but you can change it to a location under your domain name if you want, to have a full functional dashboard accessible to all. After you choose a location, you will need to add `/confirm_login`, as that is the page you need (don't worry about creating anything in your web server data directories, it is done for you through Python).

The next two, `MAL_USERNAME` and `MAL_PASSWORD`, are for the website `https://myanimelist.net`. There are some anime search features within the search module, so if you want that to work, enter a valid username-password pair for MyAnimeList.

`TWITCH_CLIENT_ID` is a Client ID for a Twitch Developers application. Like the MyAnimeList variables, this is needed for the Twitch search element of the search module. f you do not have one already, you can create a Twitch app at `https://glass.twitch.tv/console/apps`. If necessary, sign into a Twich account, and authorize all the access to your Twich account. Click the `Register` button to make a new application, and work through the setup process. When you finish (or once you open an existing application), you should see a `Client ID` field. Its contents are what you need.

`GOOGLE_API_KEY` is a key for the YouTube API. If you have one, you can put it here. Otherwise, you can create one by following `yt-key.md`.

Finally, `SECRET_KEY` is a numeric code for security. We highly recommend changing it to something longer and more erratic.

### Applying Variables

With a completed `exports.sh`, you can now add that to the end of your `.bashrc` file, which is run by `bash` every time it starts. To append `.bashrc`, run:

`cat exports.sh >> ~/.bashrc`

In order to make the changes to `.bashrc` read (without going through the startup process again, a.k.a. restarting the shell), run `source ~/.bashrc`. This preserves your current shell session (including shell history), while reloading `.bashrc`.

# Website Config

In order to make you web dash board accessible to the world, follow both "Local Only" and "Going Global". Otherwise, just follow the first.

### Local Only

If the web dashboard is to be mobile-device accessible, we need to proxy behind `nginx` (mobile browsers refuse to pull up `localhost` pages). To do so, we need to edit the `nginx` config file:

First, clear the default enabled sites on nginx:

`> /etc/nginx/sites-enabled/default`

Then, edit it (Use a text editor of choice even though we use `nano`):

`nano /etc/nginx/sites-enabled/default`

Then paste in:
```
server {
        listen 80;
        server_name www.example.com example.com;
        root /var/www/html/;
        
        location / {
            proxy_pass http://localhost:5000/;
            include /etc/nginx/proxy_params;
        }
}
```
Now save and exit.
(To exit `nano`, press ^X, Y, and Enter.)

In order to make the config changes effective, we must restart `nginx`:

`service nginx restart`

Now, the dashboard will be accessible at your computer's local IP address, which should be something like `192.168.1.xx` or `192.168.x.xx`.

### Going Global

To make your dashboard accessible to the outside world you must port-forward your computer, or follow this installation on an already port-forwarded computer (servers count, of course). Visit here for help on port-fowarding:

https://portforward.com/router.htm

If you installed this on a web server, change the above `/etc/nginx/sites-enabled/default` to include your domain name as `server_name`. Make sure it follows the same format as above.

If you own a domain, you can update it (if it doesn't already point to a server with this installed) to point to the **external** IP address of your box (now armed with a MEE6 installation), and you have a website just like `mee6.xyz`!

# Running MEE6 (Desktop/SSH)

So that's it! You installed it! If you want to do nothing and sit back, you can stop reading.

You'll need a root shell to start the bot, so get one:

`sudo -i`

Then start the bot. `cd` to the location of this repo on your computer (we'll assume it as `~/mee6`), then into the `bot` folder:

`cd ~/mee6/bot`

Then, we run this script:

`python3 bot.py`

This starts the side of the bot that interfaces with Discord.

Then, open another shell, navigate to the MEE6 folder again, and run:

`cd website/ && python3 app.py`

Do note that you may have to reboot after stopping the script for the website to work again, 
as `python` does not automatically unbind from the port.

# Running Mee6 (Console)

**Chat-Bot**
Run `cd ~/mee6/chat-bot/ && python3 bot.py`. Hit Control and Z, then type bg.
**Website**
Run `cd ~/mee6/website/ && python3 app.py`. Hit Control and Z, then type bg.

You are left with a ready prompt. To stop it, type `killall python3`.

# Conclusion

Sadly, not enough source code is available to make everything work, but we do our best!

If you find any problems, please join our dedicated Discord server, link at the top of this document.

PLEASE NOTE: Not all features may work as this repo is in the process of being updated.