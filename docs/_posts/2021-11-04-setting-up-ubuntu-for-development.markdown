---
layout: post
title:  "Setting up Ubuntu for Development"
date:   2021-11-04 16:00:00 +0100
categories: ubuntu
---

# Install programming languages
I install python, java and node.js for my development needs. I plan to develop vue webapplications with a python backend.

# Install the correct IDE
I recommend using VS Code or IntelliJ Ultimate / Webstorm / PyCharm if you are a student like me.

# Install a browser and important plugins
I personally prefer Google Chrome, but Firefox is also a great choice. Since I want to develop vue applications, I install the vue-devtools plugin. There is also a great devtools plugin for React, in case you prefer React over Vue :)

# Install additional tools
I really like to work with docker, especially when developing web applications that need access to e.g. databases. Nothing is easier than to start a ready-to-use database docker like MySQL, PostgreSQL, MongoDB or even ElasticSearch.
Also, install docker-compose to manage, start and close multiple docker containers at once.

# Configure your shell
```
# Install zsh
$ sudo apt install zsh
$ chsh -s $(which zsh)

# Install tmux (for multiple sessions, split windows etc.)
$ sudo apt-get install tmux 

# Install ohmzyzsh (https://github.com/ohmyzsh/ohmyzsh)
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Designing ohmyzsh
# Install fonts
$ sudo apt-get install fonts-powerline
# Edit your ~/.zshrc and change the theme (ZSH_THEME)
# I use powerlevel10k as recommended by my colleques :) you can find more themes here (https://github.com/ohmyzsh/ohmyzsh/wiki/External-themes#powerlevel10k)
$ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
$ nano ~/.zshrc
# set ZSH_THEME="powerlevel10k/powerlevel10k"

# Plugins for omyzsh
# https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh
$ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
$ nano ~/.zshrc
# set plugins=( 
#    # other plugins...
#    zsh-autosuggestions
#)

# Configure ZSH Autosuggestions to suggest commands as you type based on history and completions
$ cd ~/.oh-my-zsh/custom/   
$ nano autosuggestions.zsh
# write: ZSH_AUTOSUGGEST_STRATEGY=(history completion)

# Install a proper text editor (neovim)
$ sudo apt install neovim

# Install NERDTree for neovim
$ mkdir -p ~/.local/share/nvim/site/pack/plugins/start
$ git clone https://github.com/preservim/nerdtree.git ~/.local/share/nvim/site/pack/plugins/start/nerdtree
```

# Configure your desktop
I really like the Mac OS Desktop style and I want a centered, bottom app bar.
```
# Install dconf editor, then apply the following settings to achieve what we want
$ sudo apt install dconf-editor
$ gsettings set org.gnome.shell.extensions.dash-to-dock extend-height false
$ gsettings set org.gnome.shell.extensions.dash-to-dock dock-position BOTTOM
$ gsettings set org.gnome.shell.extensions.dash-to-dock transparency-mode FIXED
$ gsettings set org.gnome.shell.extensions.dash-to-dock dash-max-icon-size 64
$ gsettings set org.gnome.shell.extensions.dash-to-dock unity-backlit-items true
```
I also like to use workspaces, but by default, workspaces on Ubuntu 20 LTS only work on the primary desktop. If you work with multiple desktops, consider the following steps:
```
$ sudo apt-get install gnome-tweaks 
$ gnome-tweaks
Workspaces > Check Workspaces span displays
```

# Install additional GNOME Extensions
Install the gnome chrome extension: https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep/related
Then install the chrome-gnome-shell
```
$ sudo apt-get install chrome-gnome-shell
```
I install the following extensions:
- https://extensions.gnome.org/extension/120/system-monitor/
- https://extensions.gnome.org/extension/779/clipboard-indicator/
