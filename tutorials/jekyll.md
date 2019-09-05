---
layout: main
title: Jekyll (2019-08-19)
description: Modify Jekyll templates
---

In a previous tutorial ([here](tutorials/page.html)), we setup a GitHub page and install Jekyll on our machine to preview the pages locally. Now it is time to modify the default template of our website.

## Layouts & Includes

First we want to take a look at the default template of our theme. The code can be found on the theme repository ([here](https://github.com/pages-themes/cayman/blob/master/_layouts/default.html)).

Jekyll generate web pages using ```layouts``` and ```includes```. Layouts define the skeleton of the web pages, for now, all our pages are generated using the layout ```default.html```. Parts of the pages can be breakdown into ```includes``` that can be used in multiples ```layouts```. A good example of parts of code that can be turn to includes are the header and footer of our webpage. These parts will be defined once, and display in all our webpages.

### Header & Footer

* At the root of the project, create a new folder named ```_includes```

```sh
mkdir ./_includes
```

* Create new files for header and footer

```sh
touch ./_includes/header.html
touch ./_includes/footer.html
```

* Copy the header of ```default.html``` from the theme repository
* Paste the header in ```./_includes/header.html```
* Copy the footer of ```default.html``` from the theme repository
* Paste the footer in ```./_includes/footer.html```

### Main Layout

* At the root of the project, create a new folder named ```_layouts```

```sh
mkdir ./_layouts
```

* Create new files for the main layout

```sh
touch ./_layouts/main.html
```

* Edit ```./_layouts/main.html```

{% raw %}

```html
{% include header.html %}

<main id="content" class="main-content" role="main">
  <h1>{{page.title}}</h1>
  <p>{{page.description}}</p>
  {{ content }}
</main>

{% include footer.html %}
```

{% endraw %}

* Edit ```./index.md``` to use main.html

```md
---
layout: main
---
```

## END
