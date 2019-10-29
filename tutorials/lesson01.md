---
layout: main
title: Lesson 01 (2019-10-29)
description: Introduction to programming.
---

In this lesson we will learn the basics of programming.

First let me introduce the notion of `Algorithm`. An algorithm is a sequence of instructions required to perform a computation or solve a problem. Note that the instructions are not specific to a programming language. We first write generic instructions, like a map, then we will follow the map to code the instructions in a language of our choice.

In this course, I will first write the algorithm then implement the code in `Javascript`. Javascript is a programming language wildely use to develope web site. It is particularly useful to add dynamism and event driven actions to static pages. In the good context, we can also execute Javascript code on our machine like other imperative languages.

## Hello Word

In this section, we will prepare a webpage to experiment with our code and display the result. I will not explain the code we write in this section. Please bear with me for a while, the lesson will start in the next section.

* Create a new folder for your project (we will name the folder `basics`)
* Open this folder with your favorite text editor (we recommand [Visual Studio Code](https://code.visualstudio.com/))
* In `basics` folder, create a file names `index.html`
* Edit `basics/index.html` as below

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Basics</title>
  </head>
  <body>
    <div>HTML say "Hello Word"</div>
  </body>
</html>
```

* Save the file and open it with your favorite web browser (we recommand [Chrome](https://www.google.com/chrome/))

> We can see "HTML say Hello Word" appears on the page

* Edit `basics/index.html` as below

```html
<body>
  <div>HTML says "Hello Word"</div>
  <div id="trace"><!-- Content from javascript--></div>
  <script>
    // Function genereting content
    function trace() {
      // Hello word
      var msg = 'JavaScript says "Hello Word"';
      // Output content in console log
      console.log(msg);
      // Output content in HTML element
      document.getElementById('trace').innerHTML = msg;
    }
    // Call Javascript function
    trace();
  </script>
</body>
```

* Refresh the page inside the web browser

> We can see "JavaScript says Hello Word" appears below "HTML says Hello Word"

At this point we have a web page in which we can write code and we can view the results using a web browser.

## Variables

Any data that we wish to use in our code should be store un a `variable`. A variable has a `name` amd a `value`. The name of the variable will be use along the code to refer to the data. Note that it is recommanded to give an explicite name to our variable and that this name should not start by a number. The value of a variable is the data that we wish to store. There is 4 principal types of variables:

1. `number`: can be an integer (1) or a float (1.2) a e-notation (1e-2) or an hexadecimal (0xF), positive or negative.
2. `string`: can be a character (a) or a text (hello word).
3. `array`: it is a list of variables that are indexed using numbers. Note that the first item in the array is `index` 0.
4. `hashmap`: it is a collection of variables that are indexed using strings. Note that for hash we usually do not talk about index, but about `key`.

```js
/* Algo:
number=-1.2
print number
string='some text'
print string
array=['A','B','C']
print array and array[1]
hashmap={first: 'A', second: 'B', third: 'C'}
print hash and hash[second]
*/

var number = -1.2;
console.log('number:', number);
var string = 'some text';
console.log('string:', string);
var array = ['A', 'B', 'C'];
console.log('array:', array, 'array[1]:', array[1]);
var hashmap = {first: 'A', second: 'B', third: 'C'};
console.log('hashmap:', hashmap, 'hashmap[second]:', hashmap['second']);
```

If we look back at the hello word section, we can see that we declare a variable named `msg` and store the string `JavaScript say "Hello Word"` in that variable.

## Functions

A `function` is a serie of instructions grouped together under a `name`. Similarly as a variable, we can call a function later along the code using its name. The instructions inside a function are executed only at the time when the function is called. In addition, a function can return a value that can be store in a variable. Finally, we can define function's `attributes`. Attributes are variables that are passed to the function when we call it, and they can be used by the instructions inside the function. See an example below.

```js
/* Algo:
function sum(x, y) {
  result = x + y
  print result
  return result
}
*/

// Declaration
function sum(x, y) {
  var result = x + y;
  console.log('sum of', x, '+', y, '=', result);
  return result;
}
// Call
var mySum=sum(1, 2);
```
