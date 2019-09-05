---
layout: main
title: Material Design Bootstrap (2019-08-19)
description: Style and features
primary: 
  900: '#55006b'
  800: '#710078'
  700: '#800080' # primary-color
  600: '#910887'
  500: '#9D0D8C'
  400: '#AD399C'
  300: '#BC5DAC'
  200: '#D08CC4'
  100: '#E3BADB'
  50: '#FAE3F0'
secondary:
 900: '#EE7D1A' # secondary-color
 800: '#F3A528'
 700: '#F5BD30'
 600: '#F8D438'
 500: '#F6E43A'
 400: '#F9E958'
 300: '#FBEE76'
 200: '#FCF39D'
 100: '#FDF8C4'
 50: '#FEFCE7'
selected:
  primary: 700
  secondary: 900
---

Follow: [FontAwesome](https://fontawesome.com), [Material Design](https://material.io/) and [Boostrap](https://getbootstrap.com/) framework

## Installation

* Download FontAwesome from [here](https://fontawesome.com/how-to-use/on-the-web/setup/hosting-font-awesome-yourself)
* Extract the archive
* Copy ```/js/all.min.js``` to ```assets/js/fontawesome.min.js```
* Download the free version of MDB from [here](https://mdbootstrap.com/docs/jquery/getting-started/download/)
* Extract the archive
* Copy ```/css/bootstrap.min.css``` to ```assets/css/bootstrap.min.css```
* Copy the folder ```/scss/``` to ```_sass/mdb/```
* Copy ```/js/jquery-3.4.1.min.js``` to ```assets/js/jquery-3.4.1.min.js``
* Copy ```/js/popper.min.js``` to ```assets/js/popper.min.js```
* Copy ```/js/bootstrap.min.js``` to ```assets/js/bootstrap.min.js```
* Copy ```/js/mdb.min.js``` to ```assets/js/mdb.min.js```
* Copy the folder ```/font/``` to ```assets/font/```
* Edit ```/_includes/header.html```

{% raw %}

```html
<!-- Bootstrap core CSS -->
<link rel="stylesheet" href="/assets/css/bootstrap.min.css" >
<!-- Main Style -->
<link rel="stylesheet" href="{{ '/assets/css/style.css?v=' | append: site.github.build_revision | relative_url }}">
```

{% endraw %}

* Edit ```/_includes/footer.html```

{% raw %}

```html
</footer>

  <!-- SCRIPTS -->
  <!-- Font Awesome -->
  <script type="text/javascript" src="/assets/js/fontawesome.min.js"></script>
  <!-- JQuery -->
  <script type="text/javascript" src="/assets/js/jquery-3.4.1.min.js"></script>
  <!-- Bootstrap tooltips -->
  <script type="text/javascript" src="/assets/js/popper.min.js"></script>
  <!-- Bootstrap core JavaScript -->
  <script type="text/javascript" src="/assets/js/bootstrap.min.js"></script>
  <!-- MDB core JavaScript -->
  <script type="text/javascript" src="/assets/js/mdb.min.js"></script>
```

{% endraw %}

* Create and edit ```/assets/css/style.scss```

```scss
---
---

@charset "utf-8";

// Import Cayman theme
@import "{{ site.theme }}";
// Import MDB theme
@import "mdb/mdb";
```

## Colors

Material Design is based on 2 colors palette. We can take a look [here](https://material.io/design/color/the-color-system.html#tools-for-picking-colors) and pickup our colors.

<div class="palette primary">
  {% for c in page.primary %}
    <div class="box">
      {% if page.selected.primary == c[0] %}
      <div class="color selected" style="background-color:{{c[1]}}" data-toggle="tooltip" title="{{c[1]}}">P</div>
      {% else %}
      <div class="color" style="background-color:{{c[1]}}" data-toggle="tooltip" title="{{c[1]}}"></div>
      {% endif %}
    <div>{{ c[0] }}</div>
  </div>
  {% endfor %}
</div>

<div class="palette secondary">
  {% for c in page.secondary %}
    <div class="box">
      {% if page.selected.secondary == c[0] %}
      <div class="color selected" style="background-color:{{c[1]}}" data-toggle="tooltip" title="{{c[1]}}">S</div>
      {% else %}
      <div class="color" style="background-color:{{c[1]}}" data-toggle="tooltip" title="{{c[1]}}"></div>
      {% endif %}
    <div>{{ c[0] }}</div>
  </div>
  {% endfor %}
</div>

* Edit ```/assets/css/style.scss```

```scss
@charset "utf-8";

// Variables Overwrite
$primary-color: #800080;
$secondary-color: #EE7D1A;

// Import Cayman theme
@import "{{ site.theme }}";
// Import MDB theme
@import "mdb/mdb";
```

## Components

### Navbar

<!--Navbar -->
<nav class="navbar navbar-expand-lg navbar-dark primary-color mb-1">
  <!-- Brand -->
  <a class="navbar-brand" href="#">Brand</a>
  <!-- Toggler -->
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navCollapsible">
    <span class="navbar-toggler-icon"></span>
  </button>
  <!-- Collapsible content -->
  <div class="collapse navbar-collapse" id="navCollapsible">
    <!-- Links -->
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home
          <span class="sr-only">(current)</span>
        </a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link 1</a>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" id="dropdownMenu" data-toggle="dropdown">Dropdown</a>
        <div class="dropdown-menu dropdown-default">
          <a class="dropdown-item" href="#">Link A</a>
          <a class="dropdown-item" href="#">Link B</a>
        </div>
      </li>
    </ul>
    <!-- Socials -->
    <ul class="navbar-nav ml-auto nav-flex-icons">
      <li class="nav-item">
        <a class="nav-link">
          <i class="fab fa-facebook-f"></i>
        </a>
      </li>
      <li class="nav-item">
        <a class="nav-link">
          <i class="fab fa-twitter"></i>
        </a>
      </li>
      <li class="nav-item">
        <a class="nav-link">
          <i class="fab fa-linkedin-in"></i>
        </a>
      </li>
    </ul>
  </div>
</nav>
<!--/.Navbar -->

```html
<!--Navbar -->
<nav class="navbar navbar-expand-lg navbar-dark primary-color mb-1">
  <!-- Brand -->
  <a class="navbar-brand" href="#">Brand</a>
  <!-- Toggler -->
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navCollapsible">
    <span class="navbar-toggler-icon"></span>
  </button>
  <!-- Collapsible content -->
  <div class="collapse navbar-collapse" id="navCollapsible">
    <!-- Links -->
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home
          <span class="sr-only">(current)</span>
        </a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link 1</a>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" id="dropdownMenu" data-toggle="dropdown">Dropdown</a>
        <div class="dropdown-menu dropdown-default">
          <a class="dropdown-item" href="#">Link A</a>
          <a class="dropdown-item" href="#">Link B</a>
        </div>
      </li>
    </ul>
    <!-- Socials -->
    <ul class="navbar-nav ml-auto nav-flex-icons">
      <li class="nav-item">
        <a class="nav-link">
          <i class="fab fa-facebook-f"></i>
        </a>
      </li>
      <li class="nav-item">
        <a class="nav-link">
          <i class="fab fa-twitter"></i>
        </a>
      </li>
      <li class="nav-item">
        <a class="nav-link">
          <i class="fab fa-linkedin-in"></i>
        </a>
      </li>
    </ul>
  </div>
</nav>
<!--/.Navbar -->
```

* Option fixed-top
We can make the navbar always visible on the top of the page by adding the class ```fixed-top``` to the ```nav``` element. We notice that the content of the page is now under the navbar. We need to add margin on top of our content to make space for the navbar.

```html
<!-- Edit /_includes/header.html -->
<nav class="navbar navbar-expand-lg navbar-dark primary-color mb-1 fixed-top">
```

```scss
// Edit /assets/css/style.scss
.main-content {
  margin-top: 56px;
}
```

## TO BE CONTINUED
