---
layout: main
---

# Material Design Bootstrap (2019-08-19)
Style and features following [FontAwesome](https://fontawesome.com), [Material Design](https://material.io/) and [Boostrap](https://getbootstrap.com/) framework

## Installation
* Download FontAwesome from [here](https://fontawesome.com/how-to-use/on-the-web/setup/hosting-font-awesome-yourself)
* Extract the archive
* Copy ```/js/all.min.js``` to ```/js/fontawesome.min.js```
* Download the free version of MDB from [here](https://mdbootstrap.com/docs/jquery/getting-started/download/)
* Extract the archive
* Copy ```/css/bootstrap.min.css``` into the project
* Copy ```/css/mdb.min.css``` into the project
* Copy ```/js/jquery-3.4.1.min.js``` into the project
* Copy ```/js/popper.min.js``` into the project
* Copy ```/js/bootstrap.min.js``` into the project
* Copy ```/js/mdb.min.js``` into the project
* Copy the folder ```/font/``` into the project
* Edit ```/_includes/header.html```
```html
<link rel="stylesheet" href="{{ '/assets/css/style.css?v=' | append: site.github.build_revision | relative_url }}">
<!-- Font Awesome -->
<link rel="stylesheet" href="js/fontawesome.min.js">
<!-- Bootstrap core CSS -->
<link rel="stylesheet" href="css/bootstrap.min.css" >
<!-- Material Design Bootstrap -->
<link rel="stylesheet" href="css/mdb.min.css" >
```
* Edit ```/_includes/footer.html```
```html
</footer>

  <!-- SCRIPTS -->
  <!-- JQuery -->
  <script type="text/javascript" src="js/jquery-3.4.1.min.js"></script>
  <!-- Bootstrap tooltips -->
  <script type="text/javascript" src="js/popper.min.js"></script>
  <!-- Bootstrap core JavaScript -->
  <script type="text/javascript" src="js/bootstrap.min.js"></script>
  <!-- MDB core JavaScript -->
  <script type="text/javascript" src="js/mdb.min.js"></script>
```
