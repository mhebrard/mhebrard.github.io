---
layout: default
---

# Setup Workspace
Setup your machine to work with version control system.

## Version Control System
[Git](https://git-scm.com/downloads) is a version control system. It allows to keep track of any modifictation of files and facilitate code sharing.

### [Windows]
* Download Git for Windows
* Install Git

### [Linux / MacOS]
* check that Git is already installed
```
git --version
```

## Code Repository
[GitHub](https://github.com/) or [GitLab](https://gitlab.com/) are online repositories that comes with handy tools for project management and especially version control.
* Create an account on [GitHub](https://github.com/) or [GitLab](https://gitlab.com/)
* Create a new repository from the Git* website

## Text Editor
[Visual Studio Code](https://code.visualstudio.com/) is a text editor that become handy to develop modern applications
* Download vsCode
* Install vsCode
* Open vsCode
* Install extensions
    * In the left menu, click on the 5th icon `Extentions` or in the top menu select `View / Extensions`
    * Search for `Material Icon Theme` and click `install`.
    * Click on `reload` button in the extension lists, then `activate` in the popup.
    * Search for `Git Graph` and click `install`

## Create SSH Key
GitHub and GitLab provide two type of connections. by HTTP, you will need to enter your credentials at each action. By SSH you can create a key pair that will be use by the Git* provider to identify your machine automatically.

* Create a new key
```
ssh-keygen -t rsa -b 4096
```
* Name the key file

The command above will ask to name the key file. I usually rename the key according to the Git* provider `gitlab_rsa` or `github_rsa`. Please take care to save the key in the default folder

> [Windows] `C:\Users\{Username}\.ssh\github_rsa`

> [Linux] `/home/{Username}/.ssh/gitlab_rsa`

* Enter a Passphrase

The command will then ask for a passphrase. Note that if you enter a passphrase, you will need it for every git action (similar as HTTP credentials). I suggest to not enter passphrase.

[Windows]

At this point Windows required some more configuration (Window 10)

* ssh key config
    * create `config` file
    ```
    touch C:\Users\{Username}\.ssh\config
    ```
    * edit `config` file
    ```
    Host gitlab.com
	    IdentityFile ~/.ssh/gitlab_rsa
    Host github.com
	    IdentityFile ~/.ssh/github_rsa
    ```
* ssh agent config
    * Open the Task Manager
    * Select the tab `Services`
    * Click on `Open services`
    * Search for `OpenSSH Authentification Agent`
    * Right click and select `Properties`
    * Set the Startup type to `Automatic`
    * Click on `Start`
    * Click on `OK`

## Register SSH Key
You need to register the SSH key to the Git* provider. 

### [Github]
* Login on GitHub
* On the top right corner, click on your avatar and select `Settings`
* Select `SSH and GPG keys`
* Click on `New SSH Key`
* Enter a Title
* Copy / Paste the content of `~/.ssh/github_rsa.pub`
* Click `Add SSH key`

### [Gitlab]
* Login on GitLAb
* On the top right corner, click on your avatar and select `Settings`
* Select `SSH keys`
* Click on `New SSH Key`
* Copy / Paste the content of `~/.ssh/gitlab_rsa.pub`
* Enter a Title
* Click `Add key`

## END
You are all set. Next, you can learn how to use Git in the [next tutorial](tutorials/git.md)