# Quick OS Setup Software Setup for new OS install: Fedora, Ubuntu, Alpine

IDE config https://docs.google.com/document/d/1dZJI20D7uIknT1pdlTSmlHH1WPYdVhs2PSUyH1qdnUo/ 
Fedora Release Schedules: https://fedorapeople.org/groups/schedule/ 
dnf guide: https://www.rootusers.com/25-useful-dnf-command-examples-for-package-management-in-linux/ 
       https://linuxize.com/post/cp-command-in-linux/ 
ssh https://docs.github.com/en/authentication/connecting-to-github-with-ssh   
gpg https://docs.github.com/en/authentication/managing-commit-signature-verification  
gpg google: https://www.google.com/linuxrepositories/ 
$ nano ~/.bash_history
Cheatsheet:
```
$ dnf clean all
$ time dnf makecache
```
Snap Note: May have to do a first sudo dnf update and restart for snap to work

## Primary Overall Steps:
1.  Do vanilla install without installing anything new or any custom setup yet.
2.  Check for recommended software updates (software app). Reboot
3.  Check what has been installed already: Delete software you will not use daily. Reboot.
4.  Proceed with custom setup below.

## Secondary Overall Steps:
1.  Set up Mozilla
2.  Install and set up Chrome (log in)
3.  Install github cli
4.  Log in: Slack, github
5.  Install editors/ide: helix, Lapce
6.  Set up ssh (e.g. for github)
7.  Setup gpg (e.g. for github)
8.  open page: https://arxiv.org/list/cs/new 
9.  borkmark news directory ai-ml-ds https://docs.google.com/document/d/1Qpu-zhGbtD1VkhmmLgP9O1Ov_nleeVD4fGLb0ErdH7M/edit 

#### Turn off auto-resize when window hits edge ("hot corners"?)
```bash
$ gsettings set org.gnome.mutter edge-tiling false
```
Setup shortcuts such as Ctrl+Alt+t for gnome-terminal
https://docs.fedoraproject.org/en-US/quick-docs/gnome-setting-key-shortcut/ 

Fedora: To Enable additional RPM repositories
(or use GUI in software tool)
$ sudo dnf install \
  https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm

Tweak Gnome
	- software installer -> tweaks -> install
	- tweaks -> top bar -> seconds, day of week
	- window titlebars -> minimize, maximize


## Configure Firefox:
	- Amnesiac (do not remember anything)
- https://addons.mozilla.org/en-US/firefox/addon/privacy-badger17/
	- set to work on 'private' tabs
	- note this may not configure GPC(see below)
	- Duck Duck Go (default search)
	- secure DNS'
	- no spell checking
	- no history remembering
	- no cookie remembering
	- Dark Mode browser theme (browser setting)
	- no auto-fill
- simple dark mode invert (extension I made) 
   https://addons.mozilla.org/en-US/firefox/addon/invert-colors/
- very good but maybe not safe dark mode invert
   https://addons.mozilla.org/en-US/firefox/addon/darkreader/ 
- (add other better if not trust-able dark-mode extension)
- add bookmark for news links
   https://docs.google.com/document/d/1JR6VkpgPAD8yd1xZk1T1gj5asz3ka5q0K-_ALbyCOto/edit 

- GPC global privacy control: make sure these are 'TRUE'
1. Type about:config in the URL bar of your Firefox browser.
2. In the search box, type `globalprivacycontrol`
3. Toggle `privacy.globalprivacycontrol.enabled` to true.
4. Toggle `privacy.globalprivacycontrol.functionality.enabled` to true.
https://blog.mozilla.org/netpolicy/2021/10/28/implementing-global-privacy-control/ 
To make sure GPC is turned on in Firefox Nightly, visit https://globalprivacycontrol.org/ . The website will flag if the GPC signal has been detected.













lapce (Rust based)
https://github.com/lapce/lapce/ 

Maybe better way to install...build in cargo
https://github.com/lapce/lapce/blob/master/docs/building-from-source.md 


## Ubuntu:
1. follow instructions here:
https://github.com/lapce/lapce/blob/master/docs/building-from-source.md 

```
cargo build --release
```

2. Follow instruction below to set path to lapce, where path to 
lapce is like: 
```
home/YOURNAME/lapce/target/release/lapce
```

3. Create a symbolic link:
   - Open a terminal and run the following command to create a symbolic link from the executable to the chosen directory:
     ```bash
     ln -s home/YOURNAME/lapce/target/release/lapce ~/.local/bin/
     ```

4. Add the directory to PATH (if necessary):
     ```bash
     export PATH="home/YOURNAME/lapce/target/release/lapce:$PATH"
     ```

5. Refresh the shell:
   - Run the following command to reload the shell configuration:
     ```
     source ~/.bashrc
     ```

6. Now you can call "lapce ." or "lapce --version" from cli

















## Fedora:
follow instructions here:
https://github.com/lapce/lapce/blob/master/docs/building-from-source.md 
modified here to add perl-core
```bash
sudo dnf install cargo clang libxkbcommon-x11-devel libxcb-devel vulkan-loader-devel wayland-devel perl-File-Compare perl-FindBin perl-core
```

```bash
git clone https://github.com/lapce/lapce.git ~/lapce
```

```bash
cd lapce
```


this works
```bash
cargo build --release
```

Follow instructions below to set path to lapce, where path to 
lapce is like: 
```
home/YOURNAME/lapce/target/release/lapce
```



2.1  Install Perl (from official fedora source) to avoid a build-fail

https://developer.fedoraproject.org/tech/languages/perl/perl-installation.html
```bash
$ sudo dnf install perl-core
sudo dnf install perl-core
```



2.2 Create the ~/.local/bin directory
```bash
mkdir -p ~/.local/bin
```

2.3  Create a symbolic link:

   - Open a terminal and run the following command to create a symbolic link from the executable to the chosen directory:
```bash
ln -s /home/YOURNAME/lapce/target/release/lapce ~/.local/bin/lapce
```

2.4  Add the directory to PATH (if necessary):
```bash
export PATH="$PATH:$HOME/.local/bin"
```

2.5  Refresh the shell:
   - Run the following command to reload the shell configuration:
     ```
     source ~/.bashrc
     ```

Now you can call "lapce ." or "lapce --version" from cli


https://copr.fedorainfracloud.org/coprs/titaniumtown/lapce/ 
```bash
$ sudo dnf copr enable titaniumtown/lapce 
$ sudo dnf install lapce
```
helix (Rust based)
https://docs.helix-editor.com/install.html
```bash 
$ sudo dnf install helix
```

Configure Chrome:
- in URL bar: chrome://flags/
- sync nightmare: sync offline, delete cache, delete extensions, delete files in hidden: 
/home/NAME/.config/google-chrome/Default
	- on start: where you left off
	- DNS: google-dns (broken in linux???)
	- 3rd party cookies: https://drive.google.com (so you can download YOUR own files)


Languages: Japanese:
	Fedora: -> settings -> keyboard -> + Japanese -> Anthy -> add

Default Font google-docs:
https://www.howtogeek.com/434380/how-to-change-the-default-font-in-google-docs/ 
1. Format -> Paragraph styles -> Normal -> Update Normal
2. Format -> Paragraph styles -> Options -> Save

Configure Terminal for dark mode Ubuntu 22(Jellyfish)
```
setting -> appearance:
- dark
- launcher-bar
set window buttons
(gnome text editor -> preferences -> fonts -> e.g. oblivion)
```

py venv cheatsheet:
```bash
	$ python3 -m venv env; source env/bin/activate
```

gcc cheatsheet:
```bash
# Step 1: Compile
$ gcc -o executable_file_name source_file_name.c

# Step 2: Run
$ ./executable_file_name 
```

Fedora Check for Updates, & Restart
```bash
$ sudo dnf update
$ sudo dnf update --refresh
```

## Ubuntu
Note: for ubuntu, log in so you can actually get updates. A shame.

Ubuntu: Update Package Lists etc.
```bash
$ sudo apt update; sudo apt-get update
$ sudo apt upgrade
```

https://www.linuxcapable.com/how-to-install-python-on-fedora-linux/ 

Python
To find out if something is installed or which version, e.g. python3
method 1
```bash
$ python --version
$ python3 --version

$ pip --version
```
	(will prompt to install if not yet installed after running this version check)

Fedora: dnf
(venv is usually pre-installed in fedora)
      ```bash
$ sudo dnf install python3-pip -y
$ sudo dnf install python3-venv -y
```

Ubuntu/Debian: apt
      ```bash
$ sudo apt install python3-pip
$ sudo apt install python3-venv
 	```


pip (update)
	(You may need to do this every time you make a new venv)
```bash
	$ python3 -m pip install --upgrade pip
```

python 3.9, 3.8, 3.7, etc.
	if odd, many DS/ML/AI packages (and AWS installs)
still require python 3.9, 3.8 or even 3.7

Even if you do not have the version you need, type in the version you need, e.g.
Type in:
	$ python3.9 --version

You should then see instruction in the terminal to install that (if it is not already installed):
(Terminal Reply)
Install package 'python3.9' to provide command 'python3.9'? [N/y] 	
	Follow the prompts (say yes, 'y')  to install the desired version.

	When you make the venv (python environment) for a given project that requires a 
specific version of python, specify: e.g. $ python3.9 -m venv env

	AWS lambda functions can in later 2021 use python 3.9, 
	but packages like SciKitLearn require python3.8 so
	specify python3.8 when needed, e.g. $ python3.8 -m venv env


venv is slightly more annoying to turn-on, but overall it may be more useful and practical than pipenv. 
1. for AWS you are required to use venv, because AWS uses venv.
2. The env directory is not hidden, so you won't get lost in mysterious hidden nested python environments. Delete the env folder, and that's all to get rid of that env. No more invisible residue hanging around forever to confuse things. 

	(optional: if you want to use pipenv-shell, venv is just fine 
(if harder to remember how to turn on...)
pipenv
	https://fedoramagazine.org/install-pipenv-fedora/
$ sudo dnf install pipenv


Editors/IDE:
helix (he)
lapce()
lapce (Rust based)
https://github.com/lapce/lapce/blob/master/docs/installing-with-package-manager.md  

helix (Rust based)
https://docs.helix-editor.com/install.html 



System Monitors
	https://itsfoss.com/linux-system-monitoring-tools/ 
	top
	htop
	atop
	vtop
	gtop
	nmon
	bashtop
	glances
	

	should be available for all POSIX
	(nethogs is like 'top,' but for network traffic by 'pid' (process id) )
	Fedora
		$ sudo dnf install top
$ sudo dnf install nethogs
$ sudo dnf install htop


top vs. htop
top is very resource light compared with ether gnome monitor or even htop  
https://www.tecmint.com/htop-vs-top-in-linux/ 
#### Top:
- type 'h'
- Kill process: Scroll with arrows until your target process is at the top of the list. Type 'k'. 
- Scroll all tasks: You can, just use arrow and page keys. Don’t use the terminal scrollbar.
- Tree view: type 'V'. (shift v)
- Colors: type 'z'. Customize colors: 'Z' (shift z)
- Bar-graphs: type 'm' and 't' repeatedly.



C programming Basics: gcc, gdb
	Debian
		$ sudo apt install build-essential

	Fedora:
		Already installed!

Chrome
https://www.google.com/chrome/
set to install by default-software/gui (rather than save file to local drive)
- don't make default browser
- set to pick up where left off (if wanted)

&
use different versions to sandbox different accounts (-y says yes to y/n questions)
$ sudo dnf install google-chrome-stable -y
$ sudo dnf install google-chrome-beta -y
$ sudo dnf install google-chrome-unstable -y

Debian install version 1:
$ sudo apt-get install google-chrome-stable
$ sudo apt-get install google-chrome-beta
$ sudo apt-get install google-chrome-unstable

Debian Reinstall v1:
$ sudo apt install --reinstall google-chrome-unstable


Debian install version 2:
$ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
$ sudo apt install ./google-chrome-stable_current_amd64.deb

$ wget https://dl.google.com/linux/direct/google-chrome-unstable_current_amd64.deb
$ sudo apt install ./google-chrome-unstable_current_amd64.deb

$ wget https://dl.google.com/linux/direct/google-chrome-beta_current_amd64.deb
$ sudo apt install ./google-chrome-beta_current_amd64.deb

Debian Reinstall v2:
$ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
$ sudo apt install --reinstall ./google-chrome-unstable_current_amd64.deb

Manual Downloads:
https://www.google.com/chrome/ 
https://www.google.com/chrome/beta/ 
https://www.google.com/chrome/canary/ (no linux here?)

Older package versions (if current is broken)
https://www.ubuntuupdates.org/package/google_chrome/stable/main/base/google-chrome-unstable 

see:
https://stackoverflow.com/questions/49070206/install-specific-version-of-google-chrome-unstable 

$ sudo apt-get update
$ wget http://dl.google.com/linux/deb/pool/main/g/google-chrome-unstable/google-chrome-unstable_98.0.4758.9-1_amd64.deb
$ sudo apt-get install -f ./google-chrome-unstable_98.0.4758.9-1_amd64.deb


Fedora (podman should be installed)
	$ podman --version 




# Postman
https://snapcraft.io/install/postman/fedora 

1.
```bash
$ sudo dnf install snapd
```

2. Log out and back in again, or restart your system, to ensure snap’s paths are updated correctly. 

3. enable classic snap support
```bash
$ sudo ln -s /var/lib/snapd/snap /snap
```

4. install postman
```bash
$ sudo snap install postman
```



# Docker:
	to turn off requiring sudo for docker: 
	```bash
	$ sudo usermod -a -G docker $USER
	```
	
Fedora
	https://docs.docker.com/engine/install/fedora/ 

	Ubuntu
	https://docs.docker.com/engine/install/ubuntu/

	
	SNAP Docker is HORRIBLE 
	do NOT use it. follow instructions from 
	https://docs.docker.com/engine/install/ubuntu/




Google Colab Setup:

1. settings: darkmode
chrome://flags/  (in url bar)
search for: dark mode

2.
you can show line numbers in Google Colab with
the shortcut (Ctrl + M + L)


snap
	$ sudo dnf install snapd
Note: may have to do a first sudo dnf update and restart for snap to work
(for debian/ubuntu snap (no 'd') may be already installed)atom

and sometimes
$ sudo ln -s /var/lib/snapd/snap /snap

firefox
- set to not store any history or cookies
- default search duck duck go
- check 3rd party cookie settings
- check dns
- enable DNS over HTTPS
- disable access to mic, camera, etc.
- Enable HTTPS-Only Mode in all windows


atom
got to https://atom.io/
- for Fedora: click download .rpm file, open file with default software installer
~ select: open with/set to install by gui (rather than save file to local drive)

Configuration Notes: https://docs.google.com/document/d/1dZJI20D7uIknT1pdlTSmlHH1WPYdVhs2PSUyH1qdnUo/edit?usp=sharing
- for lite/dark mode: edit-> preferences -> themes -> ~Onelight/OneDark
Install Packages:
- linter: linter-flake8
- formatter: python-black


github cli
https://github.com/cli/cli/blob/trunk/docs/install_linux.md 
https://github.com/cli/cli/blob/trunk/docs/install_linux.md 
$ sudo dnf install gh
$ gh auth login


Adding ssh:
Run:
$ ssh-keyscan github.com >> ~/.ssh/known_hosts

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent 

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account 

$ ssh-keygen -t ed25519 -C "your_email@example.com"

> Your public key has been saved in:
/home/YOURNAME/.ssh/id_ed25519.pub

$ ssh-add /home/YOURNAME/.ssh/id_ed25519

$ cat ~/.ssh/id_ed25519.pub

via githb website:
add these output (2 lines, key and email) to github
settings -> ssh keys -> add

Run:
$ ssh-keyscan github.com >> ~/.ssh/known_hosts

	make sure known hosts file exists and is named correctly

https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints 

otherwise you may get: 
Error "The authenticity of host 'github.com' can't be established. RSA key fingerprint "


	More User Setup:
      $ git config --global user.email "YOUR_EMAIL@Email.com"
	$ git config --global user.name "YOUR_GITHUB_NAME"




GPG:
1. https://github.com/settings/keys 
ssh https://docs.github.com/en/authentication/connecting-to-github-with-ssh 
gpg https://docs.github.com/en/authentication/managing-commit-signature-verification 

$ gpg --full-generate-key
follow defaults

$ gpg --list-secret-keys --keyid-format=long

"id" here -> sec   ed25519/YOURKEYID 2020-14-14

$ gpg --armor --export YOURKEYID
+ go to github setting ssh gpg and add new key

PLUS:
 more local setup
$ git config --global user.signingkey YOURKEYID
$ git config --global commit.gpgsign true

$ gpg --list-secret-keys --keyid-format LONG
$ git config --global user.email "your_email@example.com"

 Test: (in a github repo directory)
$ eval $(gpg-agent --daemon)
$ GIT_TRACE=1 git commit -S -m "test"







Azure CLI

 Import the Microsoft repository key:
$ sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

Create a new file under /etc/yum.repos.d/
$ echo -e "[AzureCLI]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" | sudo tee /etc/yum.repos.d/azure-cli.repo

Install
$ sudo dnf install azure-cli
upgrade
$ az upgrade
check version, is updated
$ az --version

login
$ az login
	or this, if you have no GUI
$ az login --use-device-code




slack (use browser in dev-chrome, saver)
https://docs.google.com/document/d/1rvnHl_0Pe2HiDcZRv6VEIe-dX-T1KtHm_nYtGFAx9Kk/edit   

zoom
Horribly glitchy, does not work, avoid if possible. Use google-meet.
https://zoom.us/download

To Update Zoom:

1. remove zoom with:
$ sudo dnf remove zoom

2. re-download from zoom's website (type of linux, etc.)
https://zoom.us/download 
3. install with this line in terminal: (software installer won't work)
$ sudo rpm -i zoom_x86_64.rpm

maybe -u for upgrade? 
$ sudo rpm -u zoom_x86_64.rpm





vs code
	Actual versions seem to be available as of 2020.11
https://code.visualstudio.com/download

Great software...when there is an update...completely uninstall and then reinstall and reconfigure from scratch. What year is this, 1823?

gga vsCode configuration notes:
https://docs.google.com/document/d/1dZJI20D7uIknT1pdlTSmlHH1WPYdVhs2PSUyH1qdnUo/edit






Google Docs: change default font-text settings
 Step 1: Write some text in what you want to be the default, and highlight it.
 Step 2: Format -> Paragraph styles -> Options -> Save as my default styles
 Step 3: Format -> Paragraph styles -> Update normal text to match.
        or
	   Format -> Paragraph styles -> Options -> Use my default styles
 (seems a bit glitchy and rubish)


Fedora Screen Record: 
For some basic screen record the gnome one will do, hit PrtSc button. BUT this will omit the mouse and various items on the screen.

For full screen share, optional audio etc.:
Obs does work on Fedora36 wayland, configuration takes a few minutes but not impossible. 

	Method 1:
	https://snapcraft.io/install/obs-studio/fedora 

	or
	Method 2:
https://www.linuxandubuntu.com/home/obs-studio-stream-from-linux
Fedora: Enable additional RPM repositories
$ sudo dnf upgrade --refresh
$ sudo dnf install \
https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
$ sudo dnf install obs-studio -y


For Fedora and derivatives distros –
```
$ sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

$ sudo dnf install obs-studio
```


Ubuntu Screen Record:
	https://screenrec.com/screen-recorder/linux-screen-recorders/ 


heruku cli via snapd:
https://snapcraft.io/install/heroku/fedora
$ sudo dnf install snapd
$ sudo ln -s /var/lib/snapd/snap /snap
$ sudo snap install heroku --classic

AWS CLI
For current version: 
https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html 
	$ aws redshift help


aws eb cli
https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install-linux.html
$ pip install awsebcli --upgrade --user

R
https://cran.r-project.org/bin/linux/redhat/
to launch (terminal console R only)
$ R
to run a script
$ Rscript script_name.r

Scala
	Basic Repl install:
	# check that you have java installed: (1.8 or up is ok)
		$ javac -version
	# basic scala repl:
		$ sudo dnf install scala
	To use:
		$ scala


	For sbt:
https://www.scala-sbt.org/download.html 
$ curl https://bintray.com/sbt/rpm/rpm > bintray-sbt-rpm.repo
$ sudo mv bintray-sbt-rpm.repo /etc/yum.repos.d/
$ sudo yum install sbt
	To use:
	$ sbt

Instructions on testing install:
https://docs.scala-lang.org/getting-started/sbt-track/testing-scala-with-sbt-on-the-command-line.html





quick jupyter notebook / lab setup

$ python3 -m venv env; source env/bin/activate
(env)$ pip install jupyter pandas



...

For markdown 
https://snapcraft.io/remarkable


...

for VScode setup:
Tobias Reaper
Every time I set up a new virtual environment I run
pipenv install -d --pre black pylint pytest




Japanese Language Setup:
		Ubuntu
https://moritzmolch.com/blog/2503.html 
	settings -> region language -> manage installed languages -> 
-> install / remove language -> Japanese --> install/add
	restart computer (or maybe log-out and log-in)
note: "input method" should auto-set up as of 2022.06
The "A" in the upper right for input method should be visible after a reboot.
	
Fedora
	Settings -> Keyboard -> Input Sources -> +
	Japanese -> Japanese (Anthy) -> Add
	[Done, requires no reboot]
	See language icon in top right: "en"
	Japanese（Anthy)　ー＞Hiragana
あ
	



Email Clients: Thunderbird on Fedora 
https://www.lifewire.com/access-outlook-in-thunderbird-3572532 

Github CLI
$ gh auth login
https://cli.github.com/manual/ 
https://docs.github.com/en/github/setting-up-and-managing-your-github-user-account/managing-email-preferences/setting-your-commit-email-address 



python black:
	https://github.com/psf/black 
	notebook:
$ pip install black[jupyter]
normal from devs:
$ pip install git+git://github.com/psf/black


For graphics driver issue Nvidia (maybe just last one worked??)
? https://www.linuxcapable.com/how-to-install-nvidia-drivers-on-fedora-37-linux/ 

# and reboot if you are not on the latest kernel
$ sudo dnf update -y

# install free rpm fusion 
$ sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm

# install not free rpm fusion
$ sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm  https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

$ sudo dnf config-manager --set-disable copr:copr.fedorainfracloud.org:kwizart:xorg-x11-server_nvidia

# rhel/centos users can use kmod-nvidia instead
$ sudo dnf install akmod-nvidia 	

#optional for cuda/nvdec/nvenc support
$ sudo dnf install xorg-x11-drv-nvidia-cuda 	




python black:
6. Check with:
     $ pipenv graph

* * *
alt. If virtual env is required for a project:
$ python3 -m venv env; source env/bin/activate
        
(env) $ pip install git+https://github.com/psf/black pytest pylint
or
$ pip install -r requirements.txt

$ pip freeze -> requirements.txt


Bug Reports:

https://help.ubuntu.com/stable/ubuntu-help/report-ubuntu-bug.html.en 

Fedora Bug Reporting:
https://docs.fedoraproject.org/en-US/quick-docs/howto-file-a-bug/ 



tmux

a nice clean minimal terminal (not many dependencies, etc.)
Fedora
$ sudo dnf install tmux
Alpine
# apk add tmux

https://superuser.com/questions/266725/tmux-ctrlb-not-working 

To split the pane horizontally
    1. Press Ctrl+b
    2. Release pressed keys in Step 1
    3. Press "  (on many keyboards, this is Shift-key + "-key, two keys at the time time)

To split the pane vertically
    1. Press Ctrl+b
    2. Release pressed keys in Step 1
    3. Press %  (on many keyboards, this is Shift-key + 5-key, two keys at the same time)

To tottle panes
    1. Press Ctrl+b
    2. Release pressed keys in Step 1
    3. Press o (letter lower case 'o' key', one key)



alpine linux
rust for alpine: 
https://www.geeksforgeeks.org/how-to-install-rust-on-alpine/

main:
tmux
startx

To install / remove software
# apk update
# apk upgrade

# apk add PACKAGE_NAME
# apk del PACKAGE_NAME

To start gui xfce
```
# startx
```

terminal gui system monitor
https://phoenixnap.com/kb/linux-commands-check-memory-usage 
```
# top
# htop
# doas nethogs
```

mini system monitor, how much memory being used
```
# free -h
```

To shut down / reboot as root
```
# poweroff
# reboot
```

To shut down / reboot as user
```
# doas poweroff
# doas reboot
```

logout (root or user)
```
# exit
```


To change brightness in terminal:
change int number in this file (smaller number, less bright)
```
# nano /sys/class/backlight/intel_backlight/brightness
```

spaCy NLP
The step of downloading the model is strangely missing from most instruction sets.
```
$ python -m spacy download en_core_web_sm
$ python -m spacy download en_core_web_md
$ python -m spacy download en_core_web_lg
```

installing alpine linux
https://alpinelinux.org/

Great Step by Step video
https://www.youtube.com/watch?v=8WYgynP8VJ8 
or
~ https://tilde.town/~kzimmermann/articles/alpine_linux_desktop.html 


Steps:
1. download iso
2. burn to usb
3. boot iso usb
4. login: enter -> root
5. enter -> setup-alpine
6. keyboard, enter -> us
6.2 again: enter -> us
7. hostname, name of machine, type in your choice
8. "which one do you want to initialize" select [wlan0] wifi, type in wifi name
9. password/key, type in password
10. "Ip address for wlan0", use default dhcp, hit enter
11. manual network config, default no, hit enter
12. change root password, enter new password 
13. re-enter root password
14. timzone, pick whatever enter "?" to see options
15. proxy, default none, hit enter
15. time thing, chronyd? -> chrony
16. select mirror, fastest -> f (or just pick one) [if no list...maybe network issue]
17. option to add user (you can do this later)
17. ssh server, default or none, whatever
18. select hard drive disk to install to, enter your disk name (watch out for l vs 1)
19. how would you like to use the disk? (type of install) 
sys: traditional
crypt: encrypted (recommended)
enter -> crypt
20: "How would you like to use it?" enter -> sys
21: erase drive -> y
22. encryption password, enter your choice
23. re-enter your encryption password (lock)
24. "unlock" re-re-re-enter your encryption password a third (and final) time
[main install happens here]
25. enter -> reboot
26. login, enter -> root
27. enter your password
28. check memory being used, enter -> free -h
29. add new user (recommended) -> adduser -g "WHOLE NAME" YOURSHORTNAME
30. enter password
31. re-enter password
31. enable priviledges for user (optional) -> adduser YOURSHORTNAME wheel
32. doas is lighter than sudo (recommended, standard on BSD) 
->  # apk add doas tmux nano

33. likely nothing to do in this step:
you may need to use cd and ls to navigate to find files
(this is different from video)
modify file, enter text -> # nano /etc/doas.d/doas.conf
type in: "permit persist :wheel"
save: ctrl s
exit: ctrl x
(note: file may already contain "permit persist :wheel")

34. add community package repositories
modify file -> # nano /etc/apk/repositories

35. remove the "#" from the community line (likely line 2)
save: ctrl s
exit: ctrl x
36. refresh, enter text -> # apk update

[next fews step for gui (optional)]
37. -> # setup-xorg-base
38. -> # apk add xfce4 xfce4-terminal dbus
[note, if you don't want to use the greeter, just type in "startx" from command line]
39. more configuration
-> # rc-update add dbus
-> # apk add htop 
-> # apk add top 

?-> # apk add elogind polkit-elogind
https://wiki.alpinelinux.org/wiki/Elogind 

39. -> startx
https://wiki.alpinelinux.org/wiki/Xfce#Startup



Others:
? # apk add neofetch
# apk add git
# apk add automake
# apk add rust cargo


[browser]
# apk add firefox
# apk add lynx

[python3]
# apk add --update python3
# apk add --update py3-pip


C
# apk add build-base
https://wiki.alpinelinux.org/wiki/GCC








LLVM
https://www.ranvir.tech/llvm-clang-on-alpine-linux/  
# apk add clang 
# apk add lld
# apk add musl-dev
# apk add compiler-rt compiler-rt-static

compile example:
# clang -fuse-ld=lld --rtlib=compiler-rt hello.c



Golang
https://www.ranvir.tech/go-lang-on-alpine/ 



linux anti-malware:
https://www.hiroom2.com/2017/12/02/fedora-27-clamav-en/

https://www.clamav.net/downloads 
	1. download
	2. install from downloaded file with dnf


$ mkdir ~/virus
$ clamscan -r -i --move=$HOME/virus .

$ sudo dnf install -y clamav-update
$ sudo freshclam

$ sudo dnf install -y clamtk
$ clamtk
use GUI to scan



# Rust / Rustacian / Rust Lang
https://www.udemy.com/course/ultimate-rust-crash-course/


Fedora Install:
https://developer.fedoraproject.org/tech/languages/rust/rust-installation.html 
$ sudo dnf install rust cargo

(Alpine linux says now has native support...what exactly does that mean?)

$ cargo new YOUR_PROJECTS_NAME

$ RUST_BACKTRACE=full cargo run




TF Tensorflow
Tensorflow appears to work on Fedora 37 using the docker-method that is recommended on the TF(TensorFlow) website Home Page, though this may assume the CUDA is installed and that you have an NVIDA (or other supported?) GPU:
- Home Page -> https://www.tensorflow.org/install 
- GPU
- CUDA

https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Fedora&target_version=37&target_type=rpm_local 

e.g.

$ wget https://developer.download.nvidia.com/compute/cuda/12.0.1/local_installers/cuda-repo-fedora37-12-0-local-12.0.1_525.85.12-1.x86_64.rpm

$ sudo rpm -i cuda-repo-fedora37-12-0-local-12.0.1_525.85.12-1.x86_64.rpm

$ sudo dnf clean all

$ sudo dnf -y module install nvidia-driver:latest-dkms 

$ sudo dnf -y install cuda


Fedora:
$ podman pull tensorflow/tensorflow:latest  # Download latest stable image

$ podman run -it -p 8888:8888 tensorflow/tensorflow:latest-jupyter  # Start Jupyter server


..








# Kill Process

## Kill PID
- https://github.com/lineality/find_pid_listening_at_port

###  list what processes are listening at port (user your port number below)
```bash
$ sudo lsof -n -i :8080 | grep LISTEN
$ kill -9 <PID #####>
```

To see what process is active [bash]
```bash
$ sudo nethogs
$ top
```

End process by <processID>(PID) with:
```bash
$ kill -9 <processID>(PID)

Or

$ kill -SIGKILL <processID>(PID)
```



#### end_sigkill_process_bash_cheatsheet

# Kill Process

## To see what process is active [bash]
```bash
$ sudo nethogs
$ top
```
In Top:
- type 'h'
- Kill process: Scroll with arrows until your target process is at the top of the list. Type 'k'. 

## End process by <processID>(PID) with:
- https://github.com/lineality/find_pid_listening_at_port

### List what processes are listening at port (user your port number below)
```bash
$ sudo lsof -n -i :8080 | grep LISTEN
```
#### Example output: In this example '12345' is the process-ID (PID)
```
python3 12345 username    4u  IPv4 645737      0t0  TCP 127.0.0.1:rfe (LISTEN)
```


## End process by <processID>(PID) with:
```bash
$ kill -9 <processID>(PID)
```
or
```bash
$ kill -SIGKILL <processID>(PID)
```
#### For Example:
```bash
$ kill -SIGKILL 12345
```





May you, may we, may ___{noun}, become proficient
in the sustainable cultivation
of value function and meaning
via a local implementation
of generalized system best practice
with local customs and insights.

..
Topic is often coding in Rust Language or Python
- lightweight, efficient, slim, vanilla, no extra packages unless absolutely needed.
- No bloated packages with not-needed features.

- for Rust programming: never use unwrap. NO UNSAFE CODE EVER! 

- assume all tasks require full code ready for production. 

- If you have a question, ASK; never assume.

Coding is communication: keep and add to, do not remove, comments and print statements. 

Function and variable names must be clear and must NOT COLLIDE (e.g. make_step() + make_steps() IS NOT OK)

Only use terms that have clear meaning. Specifically:
Only use the words 'complex' or 'complexity' if they are jargon such as Big-O 'computational complexity' or dynamical systems maths.


