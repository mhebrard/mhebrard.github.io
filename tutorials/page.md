---
layout: main
title: GitHub Pages (2019-08-21)
description: Personal web page
---

Setup personal GitHub page. It is free and easy to setup a CV or portfolio online.

## Create the repository

* Login on GitHub
* In the top-left menu, click on `+` icon and select `New repository`
* Name the repository `{username}.github.io`. This naming convention is required by GitHub page in order to work properly.
* From the repo page, click on `Settings`
* Scroll down to the `GitHub Pages` section
* Click on `Change theme`
* After choosing your theme, click on `Select theme`
(I use `Cayman` theme for the next tutorials)

## Jekyll

GitHub pages uses [Jekyll](https://jekyllrb.com/) under the hood. Jekyll is a static site generator. We can write content using [Markdown](https://www.markdownguide.org/) and Jekyll will transform it to html files. Jekyll also accept HTML and CSS files directly and can compile [SASS](https://sass-lang.com/). With GitHub pages, everytime we push content on the master branch, the web site is build using Jekyll and published.

From here, we could directly edit the pages on GitHub and commit/push the modification using the web editor. Another option would be to clone the repo (see [tutorial](tutorials/git.html#clone-a-repo)), edit the pages on our machine and push on origin to see the changes. But if we want to preview our changes on our machine and push on origin only a satisfying version of our website, that we need to install jekyll and build the website on our machine.

* Install Ruby

  [Linux/MacOS] see jekyll installation steps [there](https://jekyllrb.com/docs/installation/)

  [Windows]

  > * Download [Ruby](https://rubyinstaller.org/) for Windows. I recommand the latest `Ruby+Devkit {version} (x64)`
  > * Install Ruby
  > * Choose `Run uidk install` at the end of the installation wizard
  > * In the RubyInstaller2 window, choose option `1 - MSYS2 base installation`
  > * At the end of the installation, press `Enter`

* Install Jekyll
  * Close vsCode and open vsCode again (to update the environment variables)
  * In vsCode, open the `Terminal`
  * Run the command

  ```sh
  gem install jekyll bundler
  ```

* Install Cayman theme
  * create a new file `Gemfile` with the content as follow

  ```sh
  source 'https://rubygems.org'
  gem 'github-pages', group: :jekyll_plugins
  gem 'wdm', '>= 0.1.0' if Gem.win_platform?
  ```

  * In the Terminal run the command

  ```sh
  bundle install
  ```

* Configure Cayman theme
  * Edit `_config.yml`
  
  ```yml
  theme: jekyll-theme-cayman # Jekyll default theme
  title: Maxime HEBRARD # Website title
  description: Bio-Informatician # Website description
  show_downloads: false # Theme header button
  github: [metadata] # auto fetch github info
  ```

* Start local server
  * In the Terminal run the command

  ```sh
  bundle exec jekyll serve
  ```

* Preview the web site
  * In a web browser, visit `http://127.0.0.1:4000`

Everytime we modify and save a page, the server update the website. If we refresh the webpage (In the browser, press `F5`), we can preview the changes.

* Stop the server
  * In vsCode, click on Terminal view
  * Press `Ctrl+C`

To preview the website locally, we create few files that do not need to be present on origin. We can notify Git to not push those files

* Create a new file `.gitignore` and edit

```git
# VS Code
.vscode/
# Jekyll
Gemfile*
_site/
```

## END

Now we can edit our website, preview the changes on our machine, push the code on the web and publish it !
