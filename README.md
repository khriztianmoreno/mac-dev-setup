# Mac OS X Dev Setup

This document describes how I set up my developer environment on a new MacBook or iMac. We will set up [Node](http://nodejs.org/) (JavaScript), [Python](http://www.python.org/), and [Ruby](http://www.ruby-lang.org/) environments, mainly for JavaScript and Python development. Even if you don't program in all three, it is good to have them as many command-line tools use one of them. As you read  and follow these steps, feel free to send me any feedback or comments you may have.

The document assumes you are new to Mac. The steps below were tested on **OS X Mountain Lion**.

If you have any comments or suggestions, feel free to give me a shout [on Twitter](https://twitter.com/nicolahery)!

- [System update](#system-update)
- [System preferences](#system-preferences)
- [Google Chrome](#google-chrome)
- [iTerm2](#iterm2)
- [Homebrew](#homebrew)
- [Consolas](#consolas)
- [Beautiful terminal](#beautiful-terminal)
- [iTerm2](#iterm2)
- [ohmyZSH](#ohmyzsh)
- [Git](#git)
- [Node.js](#nodejs)
- [MongoDB](#mongodb)
- [Redis](#redis)
- [Elasticsearch](#elasticsearch)
- [Projects folder](#projects-folder)
- [Apps](#apps)

## System update

First thing you need to do, on any OS actually, is update the system! For that: **Apple Icon > Software Update...**

## System preferences

If this is a new computer, there are a couple tweaks I like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:

- Trackpad > Tap to click
- Keyboard > Key Repeat > Fast (all the way to the right)
- Keyboard > Delay Until Repeat > Short (all the way to the right)
- Dock > Automatically hide and show the Dock

## Google Chrome

Install your favorite browser, mine happens to be Chrome.

Download from [www.google.com/chrome](https://www.google.com/intl/en/chrome/browser/). Open the **.dmg** file once it's done downloading (this will mount the disk image), and drag and drop the **Google Chrome** app into the Applications folder (on the Mac, most applications are installed this way). When done, you can unmount the disk in Finder (the small "eject" icon next to the disk under **Devices**).

## iTerm2

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/) (the newest version, even if it says "beta release").

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**, **Working Directory** select **Reuse previous session's directory**

In the tab **Profiles**, create a new one with the "+" icon, and rename it to your first name for example. Then, select **Other Actions... > Set as Default**. Finally, under the section **Window**, change the size to something better, like **Columns: 125** and **Rows: 35**.



When done, hit the red "X" in the upper left (saving is automatic in OS X preference panes). Close the window and open a new one to see the size change.

## Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for OS X is [Homebrew](http://brew.sh/).

### Install

An important dependency before Homebrew can work is the **Command Line Tools** for **Xcode**. These include compilers that will allow you to build things from source.

Now, Xcode weights something like 2GB, and you don't need it unless you're developing iPhone or Mac apps. Good news is Apple provides a way to install only the Command Line Tools, without Xcode. To do this you need to go to [http://developer.apple.com/downloads](http://developer.apple.com/downloads), and sign in with your Apple ID (the same one you use for iTunes and app purchases). Unfortunately, you're greeted by a rather annoying questionnaire. All questions are required, so feel free to answer at random.

Once you reach the downloads page, search for "command line tools", and download the latest **Command Line Tools (OS X Mountain Lion) for Xcode**. Open the **.dmg** file once it's done downloading, and double-click on the **.mpkg** installer to launch the installation. When it's done, you can unmount the disk in Finder.

**Note**: If you are running **OS X 10.9 Mavericks**, then you can install the Xcode Command Line Tools directly from the command line with `$ xcode-select --install`, and you don't have to go through the download page and the questionnaire.

Finally, we can install Hombrew! In the terminal paste the following line (without the `$`), hit **Enter**, and follow the steps on the screen:

    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

One thing we need to do is tell the system to use programs installed by Hombrew (in `/usr/local/bin`) rather than the OS default if it exists. We do this by adding `/usr/local/bin` to your `$PATH` environment variable:

    $ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile

Open a new terminal tab with **Cmd+T** (you should also close the old one), then run the following command to make sure everything works:

    $ brew doctor
    
### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

    $ brew install <formula>
        
To update Homebrew's directory of formulae, run:

    $ brew update
    
**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

    $ cd /usr/local
    $ git fetch origin
    $ git reset --hard origin/master

To see if any of your packages need to be updated:

    $ brew outdated
    
To update a package:

    $ brew upgrade <formula>
        
Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

    $ brew cleanup

To see what you have installed (with their version numbers):

    $ brew list --versions

## Consolas

I really like the Consolas font for coding. Being a Microsoft (!) font, it is not installed by default. Since we're going to be looking at a lot of terminal output and code, let's install it now.

There are two ways we can install it. If you bought **Microsoft Office for Mac**, install that and Consolas will be installed as well.

If you don't have Office, follow these steps:

    $ brew install cabextract
    $ cd ~/Downloads
    $ mkdir consolas
    $ cd consolas
    $ curl -O http://download.microsoft.com/download/f/5/a/f5a3df76-d856-4a61-a6bd-722f52a5be26/PowerPointViewer.exe
    $ cabextract PowerPointViewer.exe
    $ cabextract ppviewer.cab
    $ open CONSOLA*.TTF

And click **Install Font**. Thanks to Alexander Zhuravlev for his [post](http://blog.ikato.com/post/15675823000/how-to-install-consolas-font-on-mac-os-x).

## Beautiful terminal

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. What follows might seem like a lot of work, but trust me, it'll make the development experience so much better.

Let's go ahead and start by changing the font. In **iTerm > Preferences...**, under the tab **Profiles**, section **Text**, change both fonts to **Consolas 13pt**.

Now let's add some color. I'm a big fan of the [Solarized](http://ethanschoonover.com/solarized) color scheme. It is supposed to be scientifically optimal for the eyes. I just find it pretty.

Scroll down the page and download the latest version. Unzip the archive. In it you will find the `iterm2-colors-solarized` folder with a `README.md` file, but I will just walk you through it here:

- In **iTerm2 Preferences**, under **Profiles** and **Colors**, go to **Load Presets... > Import...**, find and open the two **.itermcolors** files we downloaded.
- Go back to **Load Presets...** and select **Solarized Dark** to activate it. Voila!

**Note**: You don't have to do this, but there is one color in the **Solarized Dark** preset I don't agree with, which is *Bright Black*. You'll notice it's too close to *Black*. So I change it to be the same as *Bright Yellow*, i.e. **R 83 G 104 B 112**.

Not a lot of colors yet. We need to tweak a little bit our Unix user's profile for that. This is done (on OS X and Linux), in the `~/.bash_profile` text file (`~` stands for the user's home directory).

We'll come back to the details of that later, but for now, just download the files [.bash_profile](https://raw.githubusercontent.com/khriztianmoreno/mac-dev-setup/master/.bash_profile), [.bash_prompt](https://raw.githubusercontent.com/khriztianmoreno/mac-dev-setup/master/.bash_prompt), [.aliases](https://raw.githubusercontent.com/khriztianmoreno/mac-dev-setup/master/.aliases) attached to this document into your home directory (`.bash_profile` is the one that gets loaded, I've set it up to call the others):

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/khriztianmoreno/mac-dev-setup/master/.bash_profile
    $ curl -O https://raw.githubusercontent.com/khriztianmoreno/mac-dev-setup/master/.bash_prompt
    $ curl -O https://raw.githubusercontent.com/khriztianmoreno/mac-dev-setup/master/.aliases
    
With that, open a new terminal tab (Cmd+T) and see the change! Try the list commands: `ls`, `ls -lh` (aliased to `ll`), `ls -lha` (aliased to `la`).

At this point you can also change your computer's name, which shows up in this terminal prompt. If you want to do so, go to **System Preferences** > **Sharing**. For example, I changed mine from "Nicolas's MacBook Air" to just "MacBook Air", so it shows up as `MacBook-Air` in the terminal.

Now we have a terminal we can work with!

(Thanks to Mathias Bynens for his awesome [dotfiles](https://github.com/mathiasbynens/dotfiles).)

## ohmyzsh 

Oh-My-Zsh is an open source, community-driven framework for managing your ZSH configuration. It comes bundled with a ton of helpful functions, helpers, plugins, themes, and a few things that make you shout...

```bash
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## Git

What's a developer without [Git](http://git-scm.com/)? To install, simply run:

    $ brew install git
    
When done, to test that it installed fine you can run:

    $ git --version
    
And `$ which git` should output `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig) file to your home directory:

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/khriztianmoreno/mac-dev-setup/master/.gitconfig

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

    $ git config --global user.name "Your Name Here"
    $ git config --global user.email "your_email@youremail.com"

They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we're going to use the recommended HTTPS method (versus SSH). So you don't have to type your username and password everytime, let's enable Git password caching as described [here](https://help.github.com/articles/set-up-git):

    $ git config --global credential.helper osxkeychain
    
**Note**: On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your `.gitignore` files. You can take a look at this repository's [.gitignore](https://github.com/nicolashery/mac-dev-setup/blob/master/.gitignore) file for inspiration.
    

## Node.js

### **NVM** 
Node Version Manager - Simple bash script to manage multiple active node.js versions

#### Installation

##### Install script

To install or update nvm, you can use the [install script][2] using cURL:

```sh
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```

or Wget:

```sh
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```

<sub>The script clones the nvm repository to `~/.nvm` and adds the source line to your profile (`~/.bash_profile`, `~/.zshrc`, `~/.profile`, or `~/.bashrc`).</sub>

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

You can customize the install source, directory, profile, and version using the `NVM_SOURCE`, `NVM_DIR`, `PROFILE`, and `NODE_VERSION` variables.
Eg: `curl ... | NVM_DIR=/usr/local/nvm bash` for a global install. Ensure that the `NVM_DIR` does not contain a trailing slash.

<sub>*NB. The installer can use `git`, `curl`, or `wget` to download `nvm`, whatever is available.*</sub>

**Note:** On Linux, after running the install script, if you get `nvm: command not found` or see no feedback from your terminal after you type:

```sh
command -v nvm
```
simply close your current terminal, open a new terminal, and try verifying again.

**Note:** On OS X, if you get `nvm: command not found` after running the install script, one of the following might be the reason:-
  - your system may not have a [`.bash_profile file`] where the command is set up. Simply create one with `touch ~/.bash_profile` and run the install script again
  - you might need to restart your terminal instance. Try opening a new tab/window in your terminal and retry.

If the above doesn't fix the problem, open your `.bash_profile` and add the following line of code:

`source ~/.bashrc`

- For more information about this issue and possible workarounds, please [refer here](https://github.com/creationix/nvm/issues/576)

### Homebrew
Install [Node.js](http://nodejs.org/) with Homebrew:

    $ brew update
    $ brew install node
    
The formula also installs the [npm](https://npmjs.org/) package manager. However, as suggested by the Homebrew output, we need to add `/usr/local/share/npm/bin` to our path so that npm-installed modules with executables will have them picked up.

To do so, add this line to your `~/.path` file, before the `export PATH` line:

```bash
PATH=/usr/local/share/npm/bin:$PATH
```
        
Open a new terminal for the `$PATH` changes to take effect.

We also need to tell npm where to find the Xcode Command Line Tools, by running:

    $ sudo xcode-select -switch /usr/bin

(If Xcode Command Line Tools were installed by Xcode, try instead:)

    $ sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer

Node modules are installed locally in the `node_modules` folder of each project by default, but there are at least two that are worth installing globally. Those are [CoffeeScript](http://coffeescript.org/) and [Grunt](http://gruntjs.com/):

    $ npm install -g coffee-script
    $ npm install -g grunt-cli

### Npm usage

To install a package:

    $ npm install <package> # Install locally
    $ npm install -g <package> # Install globally

To install a package and save it in your project's `package.json` file:

    $ npm install <package> --save

To see what's installed:

    $ npm list # Local
    $ npm list -g # Global

To find outdated packages (locally or globally):

    $ npm outdated [-g]

To upgrade all or a particular package:

    $ npm update [<package>]

To uninstall a package:

    $ npm uninstall <package>


## MongoDB

[MongoDB](http://www.mongodb.org/) is a popular [NoSQL](http://en.wikipedia.org/wiki/NoSQL) database.

### Install

#### Docker
`docker run --name mongo-dev -d -v /data/db  -p 27017:27017 mongo` 

Installing it is very easy through Homebrew:

    $ brew update
    $ brew install mongo
    $ mkdir -p /data/db

### Set permissions for the data directory
Ensure that user account running mongod has correct permissions for the directory:

```bash
sudo chmod 0755 /data/db
sudo chown $USER /data/db
```

### Usage

In a terminal, start the MongoDB server:

    $ mongod

In another terminal, connect to the database with the Mongo shell using:

    $ mongo

I'll let you refer to MongoDB's [Getting Started](http://docs.mongodb.org/manual/tutorial/getting-started/) guide for more!

## Redis

[Redis](http://redis.io/) is a blazing fast, in-memory, key-value store, that uses the disk for persistence. It's kind of like a NoSQL database, but there are a lot of [cool things](http://oldblog.antirez.com/post/take-advantage-of-redis-adding-it-to-your-stack.html) that you can do with it that would be hard or inefficient with other database solutions. For example, it's often used as session management or caching by web apps, but it has many other uses.

### Install

To install Redis, use Homebrew:

    $ brew update
    $ brew install redis

### Usage

Start a local Redis server using the default configuration settings with:

    $ redis-server

For advanced usage, you can tweak the configuration file at `/usr/local/etc/redis.conf` (I suggest making a backup first), and use those settings with:

    $ redis-server /usr/local/etc/redis.conf

In another terminal, connect to the server with the Redis command-line interface using:

    $ redis-cli

I'll let you refer to Redis' [documentation](http://redis.io/documentation) or other tutorials for more information.

## Elasticsearch

As it says on the box, [Elasticsearch](http://www.elasticsearch.org/) is a "powerful open source, distributed real-time search and analytics engine". It uses an HTTP REST API, making it really easy to work with from any programming language.

You can use elasticsearch for such cool things as real-time search results, autocomplete, recommendations, machine learning, and more.

### Install

Elasticsearch runs on Java, so check if you have it installed by running:

```bash
java -version
```

If Java isn't installed yet, a window will appear prompting you to install it. Go ahead and click "Install".

Next, install elasticsearch with:

```bash
$ brew install elasticsearch
```

**Note**: Elasticsearch also has a `plugin` program that gets moved to your `PATH`. I find that too generic of a name, so I rename it to `elasticsearch-plugin` by running (will need to do that again if you update elasticsearch):

```bash
$ mv /usr/local/bin/plugin /usr/local/bin/elasticsearch-plugin
```

Below I will use `elasticsearch-plugin`, just replace it with `plugin` if you haven't followed this step.

As you guessed, you can add plugins to elasticsearch. A popular one is [elasticsearch-head](http://mobz.github.io/elasticsearch-head/), which gives you a web interface to the REST API. Install it with:

```bash
$ elasticsearch-plugin --install mobz/elasticsearch-head
```

### Usage

Start a local elasticsearch server with:

```bash
$ elasticsearch -f
```

(The `-f` option tells it to run in the foreground, so you can stop it with `Ctrl+C`.)

Test that the server is working correctly by running:

```bash
$ curl -XGET 'http://localhost:9200/'
```

If you installed the elasticsearch-head plugin, you can visit its interface at `http://localhost:9200/_plugin/head/`.

Elasticsearch's [documentation](http://www.elasticsearch.org/guide/) is more of a reference. To get started, I suggest reading some of the blog posts linked on this [StackOverflow answer](http://stackoverflow.com/questions/11593035/beginners-guide-to-elasticsearch/11767610#11767610).

## Projects folder

This really depends on how you want to organize your files, but I like to put all my version-controlled projects in `~/Projects`. Other documents I may have, or things not yet under version control, I like to put in `~/Dropbox` (if you have Dropbox installed), or `~/Documents`.

## Apps

Here is a quick list of some apps I use, and that you might find useful as well:

- [Dropbox](https://www.dropbox.com/): File syncing to the cloud. I put all my documents in Dropbox. It syncs them to all my devices (laptop, mobile, tablet), and serves as a backup as well! **(Free for 2GB)**
- [Google Drive](https://drive.google.com/): File syncing to the cloud too! I use Google Docs a lot to collaborate with others (edit a document with multiple people in real-time!), and sometimes upload other non-Google documents (pictures, etc.), so the app comes in handy for that. **(Free for 5GB)**
- [1Password](https://agilebits.com/onepassword): Allows you to securely store your login and passwords. Even if you only use a few different passwords (they say you shouldn't!), this is really handy to keep track of all the accounts you sign up for! Also, they have a mobile app so you always have all your passwords with you (syncs with Dropbox). A little pricey though. There are free alternatives. **($50 for Mac app, $18 for iOS app)**
- [Marked](http://markedapp.com/): As a developer, most of the stuff you write ends up being in [Markdown](http://daringfireball.net/projects/markdown/). In fact, this `README.md` file (possibly the most important file of a GitHub repo) is indeed in Markdown, written in Sublime Text, and I use Marked to preview the results everytime I save. **($4)**
- [Path Finder](http://cocoatech.com/pathfinder/): I love OSX, it's Unix so great for developers, and all of it just works and looks pretty! Only thing I "miss" from Windows (OMG what did he say?), is a decent file explorer. I think Finder is a pain to use. So I gladly paid for this alternative, but I understand others might find it expensive just to not have to use Finder. **($40)**
- [Evernote](https://evernote.com/): If I don't write something down, I'll forget it. As a developer, you learn so many new things every day, and technology keeps changing, it would be insane to want to keep it all in your head. So take notes, sync them to the cloud, and have them on all your devices. To be honest, I switched to [Simplenote](http://simplenote.com/) because I only take text notes, and I got tired of Evernote putting extra spaces between paragraphs when I copy & pasted into other applications. Simplenote is so much better for text notes (and it supports Markdown!). **(Both are free)**
- [Moom](http://manytricks.com/moom/): Don't waste time resizing and moving your windows. Moom makes this very easy. **($10)**




