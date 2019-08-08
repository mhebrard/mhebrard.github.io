---
layout: default
---

# Git (2019-08-08)
Git is a version control system. It allows to keep track of any modifictation of files and facilitate code sharing.

## Introduction
### Branching Model
Git can be confusing at first. You need to understand some basics and keep your repo organized to work efficiently. One great resource is [This post](https://nvie.com/posts/a-successful-git-branching-model/) Where Vincent Driessen introduce a model now known as `GitFlow`.

### Origin vs Local
Previously, we create a repo on the cloud. This code is the `Origin of truth`, we call this repo `origin`. Later we will copy this code on our local machine and work on it. Note that the local version and the origin are not automatically synchronized ! Here we are using Git, not a cloud service. We have full control of what is synch. That also means we need to be more careful.

### Pull, Commit, Push
Because the local repo and origin are not authomatically synchronise, we first need to `Pull` the code from origin and copy it on our local machine. Then we can modify the files. Once our code is satifying, we can `Commit` the changes. That create a entry in git history and save all the files. Note that we can do multiple commit on our local machine. Once the code is ready, we need to `Push` the code on origin, that will copy our local files (and all the commit history) to the cloud.

### Branches and merge
Git also allows to create multiples `Branches` that represent multiple history lines. By convention, the main branch is called `master`. From master, we can create a new branch `develop`, then `checkout` on develop. Checkout indicate git that we move to the develop branch history. When we commit changes, they will be created on the develop branch. Note that if we checkout on master branch, git will automatically change the content of the working directory to reflect the last commit made on the master branch. Later we can `merge` develop into master. That will create a new commit and merge the files from both branches.

### GitFlow
GitFlow define some best practice in term of branching.

* The branch `master` represent the production version of the code.
  * `master` is always present
* The branch `develop` represent the development version of the code.
  * `develop` is branched from `master`
  * `develop` is merged into `master`
  * `develop` is always present
* A branch `feature` is created for each new feature development. Note that multiples branch feature can live at the same time (featureA, featureB...) depending of the needs.
  * `feature` is branched from `develop`
  * `feature` is merged into `develop`
  * `feature` is deleted after merged

## Usage
First you need to [Setup Workspace](tutorials/setup.html).

### Clone a repo
* Login on Git* website,
* Navigate to your repository.
* Click on `Clone`
* Copy the SSH address (`git@git....com:{Username}/{Repo}.git`)
* In vsCode, open the Command Palette (`Ctrl + Shift + P`)
* Enter `>Git:Clone`
* Paste the SSH address
* Select the directory where the repo will be created (vsCode will create a new folder with the name of the repo in this directory).
* Open the repo folder with vsCode

### Create feature branch
* Checkout on develop
  * In vsCode, in the left menu, click on the 3rd icon `Source Control`
  * In the left-top menu, click on the 3rd icon `View Git Graph`
  * In Git Graph view, double-click on develop
* Pull origin/develop
  * If there is new commit on origin/develop, in the bottom menu, click on the second button `Synchronize Changes`
* Create feature branch
  * In Git Graph view, right-click on the last commit, and select `Create Branch...`
  * Name the branch (`f-{myfeature}`)
* Checkout on feature branch
  * In Git Graph view, double-click on the feature branch

### Commit changes
* Change the files
  * In vsCode, in the left menu, click on the 1st icon `Explorer`
  * Click on a file name to open it in the main view
  * Edit the files
  * Save the changes
* Review the changes
  * In vsCode, ub the left menu, click on the 3rd icon `Source Control`
  * Click on a file name to open a diff view. The previous and current version are displayed, with the changes highlighted.
* Stage the changes
  * In the left menu, beside the file name, click on the 3rd icon `Stage changes`
* Commit
  * In the left-top menu, enter a commit message
  * Click on the 1st icon `Commit`

### Merge branch
* Checkout on develop
  * In vsCode, in the left menu, click on the 3rd icon `Source Control`
  * In the left-top menu, click on the 3rd icon `View Git Graph`
  * In Git Graph view, double-click on develop
* Pull origin/develop
  * If there is new commit on origin/develop, in the bottom menu, click on the second button `Synchronize Changes`
* Merge feature into develop
  * In Git Graph view, right-click on feature and select `Merge into current branch...`
  * Check `Create a new commit even if fast-forward is possible`
  * Click on `Yes, merge`

### Push
* In vsCode, in the left menu, click on the 3rd icon `Source Control`
* In the left-top menu, click on the 3rd icon `View Git Graph`
* Check that your branch is upward origin
* In the bottom menu, click on the second button `Synchronize Changes`

## END
Now you are a git-pro !!
