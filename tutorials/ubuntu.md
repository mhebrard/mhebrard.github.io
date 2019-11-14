---
layout: main
title: Ubuntu on Windows (2019-11-14)
description: Install ubuntu as a "Win10 app"
---

## Activate Windows subsystem for Linux

Windows 10 allows to install Linux as an application. Here we will activate Windows Subsystem for Linux (WSL) then install Ubuntu from the Microsoft Store. This application take the form of a terminal and come with a full Ubuntu distribution. Note that we will not have any Graphic User Interface with this application, but we have access to all the command line tools. It is also good to know that Windows file system is automaticaly mount inside the linux file system so we can access our data seamlessly.

* Click on `windows icon` or press `windows key`
* Type `Control Panel`
* Open `Control Panel`
* Click on `Programs`
* Click on `Turn Windows features on or off`
* Check `Windows Subsystem for Linux`
* Click on `Ok`
* Click on `Restart now`
* Open `Microsoft Store`
* Search `Ubuntu`
* Select `Ubuntu`
* Click on `Get`
* Click on `Launch`
* Enter a username
* Enter a password
* Re-enter the password

> Now we can enjoy Linux directly within Windows ! We can find Ubuntu listed in our applications.

## Custom shell

WSL come with a minimal terminal. In this section, we will configure the terminal to add some features and style using [Oh My ZSH!](https://ohmyz.sh/). We can find dozens of [themes](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes) available for Oh My Zsh, here we will install [Powerlevel10k](https://github.com/romkatv/powerlevel10k). Thanks to Deepu K Sasidharan
 for [his guide](https://deepu.tech/configure-a-beautiful-terminal-on-unix/).

* Open `Ubuntu`
* Install `zsh`

  `sudo apt install zsh -y`

* Install `Oh My Zsh!`

  `sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`

* Set zsh as default shell

  `chsh -s $(which zsh)`

* Close `Ubuntu`

  `exit`

* Open `Ubuntu`
* Setup zsh config file

  `0`

* Install `Oh My Zsh!`

  `sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`

* Install plugins
  * `zsh-autosuggestions` provides autocompletion based on our previous commands
  
    `git clone --depth=1 https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions`
  
  * `zsh-syntax-highlighting` provides syntax highlighting.
  
    `git clone --depth=1 https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting`
  
  * `autojump` provides a smarter directory navigation system.
  
    Folow the installation instructions for your OS from [here](https://github.com/wting/autojump#automatic)

* Setup `ZSH`: edit `~/.zshrc` as follow

  ```sh
  # Specify full color mode
  export TERM="xterm-256color"

  # Add exports from your profile
  source ~/.profile

  # Path to your oh-my-zsh installation.
  export ZSH="/home/hebrardms/.oh-my-zsh"

  # ZSH Settings
  # Fix pasting URLs and other text messed up.
  DISABLE_MAGIC_FUNCTIONS=true
  # Disable colors in ls.
  DISABLE_LS_COLORS="true"
  # Enable command auto-correction.
  ENABLE_CORRECTION="true"
  # Display red dots whilst waiting for completion.
  COMPLETION_WAITING_DOTS="true"
  # Disable marking untracked files under VCS as dirty. (much faster)
  DISABLE_UNTRACKED_FILES_DIRTY="true"
  ```

  ```sh
  # Which plugins would you like to load?
  # Standard plugins can be found in ~/.oh-my-zsh/plugins/*
  # Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/
  # Example format: plugins=(rails git textmate ruby lighthouse)
  # Add wisely, as too many plugins slow down shell startup.
  plugins=(git zsh-autosuggestions zsh-syntax-highlighting)

  source $ZSH/oh-my-zsh.sh
  ```

* Install fonts

  ZSH and Powerlevel10K theme that we will installed later show their potential when used with fonts that contain extended icon sets known as [Powerline fonts](https://github.com/powerline/fonts) and [nerd fonts](https://github.com/ryanoasis/nerd-fonts). There is multiple fonts available, but I had some issues finding one compatible for windows.

  `MesloLGS` is the font recommanded by Powerlevel10K and work great with WSL. We can download the file from [here](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Regular.ttf)

  Sadly VsCode do not like this font so I choose `RobotoMono` from [here](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/RobotoMono/Regular/complete/Roboto%20Mono%20Nerd%20Font%20Complete%20Mono.ttf) as alternative.

  * Download the 2 font files
  * Open each file and click on `Install`

* Setup `WSL` to use `MesloLGS` font
  * Right click on the `Ubuntu icon` at the left top corner of Ubuntu terminal
  * Click on `Properties`
  * In the tab `Font`, select size: `18` and Font: `MesloLGS NF`
  * Click on `OK`

* Install `Powerlevel10k` Theme

  `git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k`

* Enable `Powerlevel10k` Theme: edit `~/.zshrc` as follow

  ```sh
  ZSH_THEME=powerlevel10k/powerlevel10k
  ```

* Configure `Powerlevel10k`

  Powerlevel10K come with an easy configuration wizard, answer the questions as we see fit and it generate a config file for us. Ig the configuration is not triggered automatically, we can initiate it by

  `p10k configure`

  At the end of the dialogue it will generate a file `~/.p10k.zsh` that we can manually edit if needed. We can for example look at `POWERLEVEL9K_LEFT_PROMPT_ELEMENTS` and `POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS` to choose which item to display.

> Close and re-open Ubuntu and w have a beautiful Prompt !

## END
