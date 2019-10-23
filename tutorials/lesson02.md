---
layout: main
title: Lesson 02 (2019-10-23)
description: Parse and format a list of articles.
---

In this lesson, we will read a list of articles information (title, authors...), parse the different type of data and format it according to our wish.

## Source file

For this example, we will start from a table (excel file) that contains the title, authors, journal, date, issue and PubMedID information for a list of articles.

| Title | Authors | Journal | Date | Issue | PMID |
|-------|---------|---------|------|-------|------|
|Functional analysis of Plasmodium falciparum subpopulations associated with artemisinin resistance in Cambodia. | Dwivedi A, Reynes C, Kuehn A, Roche DB, Khim N, Hebrard M, Milanesi S, Rivals E, Frutos R, Menard D, Mamoun CB, Colinge J, Cornillot E. | Malar J. |2017 Dec 19 | 16(1):493 | 29258508 |
| Transcriptomic study of Salmonella enterica subspecies enterica serovar Typhi biofilm. | Chin KCJ, Taylor TD, Hebrard M, Anbalagan K, Dashti MG, Phua KK. | BMC Genomics. | 2017 Oct 31 | 18(1):836 | 29089020 |
| Population genomics of picophytoplankton unveils novel chromosome hypervariability. | Blanc-Mathieu R, Krasovec M, Hebrard M, Yau S, Desgranges E, Martin J, Schackwitz W, Kuo A, Salin G, Donnadieu C, Desdevises Y, Sanchez-Ferandin S, Moreau H, Rivals E, Grigoriev IV, Grimsley N, Eyre-Walker A, Piganeau G. | Sci Adv. | 2017 Jul 5 | 3(7):e1700239 | 28695208
MetaTreeMap: An Alternative Visualization Method for Displaying Metagenomic Phylogenic Trees. | Hebrard M, Taylor TD. | PLoS One. | 2016 Jun 23 | 11(6):e0158261 | 27336370
Recessive Mutations in RTN4IP1 Cause Isolated and Syndromic Optic Neuropathies. | Angebault C, Guichet PO, Talmat-Amar Y, Charif M, Gerber S, Fares-Taie L, Gueguen N, Halloy F, Moore D, Amati-Bonneau P, Manes G, Hebrard M, Bocquet B, Quiles M, Piro-Mégy C, Teigell M, Delettre C, Rossel M, Meunier I, Preising M, Lorenz B, Carelli V, Chinnery PF, Yu-Wai-Man P, Kaplan J, Roubertie A, Barakat A, Bonneau D, Reynier P, Rozet JM, Bomont P, Hamel CP, Lenaers G. | Am J Hum Genet. | 2015 Nov 5 | 97(5):754-60 | 26593267

Our goal is to display this list of article using a format following the pattern below:

> Title. First Author *et al*. *Journal* **issue** (year)

## Input

First we need to input the data in our code. We can edit `basics/index.html` from lesson 01 or create a new html page `basics/lesson02.html`
as below:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Basics - 02</title>
  </head>
  <body>
    <div>HTML say "Hello Word"</div>
    <div id="trace"><!-- Content from javascript--></div>
    <script>
      // Function genereting content
      function trace() {
        // Copy data from the table and paste it between the `...`
        var input = ``;
        // Output content in console log
        console.log('input:', input);
        // Output content in HTML element
        document.getElementById('trace').innerHTML = input;
      }
      // Call Javascript function
      trace();
    </script>
  </body>
</html>
```

At this point we can open the table that contains the list of articles, copy the data and paste the data input variable. To prove that we get the data inside our variable we can print it.

## Parsing

The `input` variable contains one string will all our data. if we want to manipulate the information we need to parse this string, cut the text in pieces.

First we need to recover the lines. To do so we can cut the string each time we encounter `\n` that represent the special character `new line`. We can use the generic function `split` that take 2 arguments: The string we want to cut and a pattern we will use to cut the string. The split function return an array of strings, result of the cut.

```js
/* Algo:
lines=split(input, '\n')
*/

// Split input string into an array of lines
var lines = input.split('\n');
```

Notice that in our case, the first line is the header of the table. We will keep this first line aside in another variable for further use. We also need to recover the label of each column. To do so, we can cut the header line each time we encounter `\t` that represent the special character `tabulation`.

```js
/* Algo:
header=lines[0]
header=split(header, '\t')
*/

// Split the first line in an array of headers
var headers = lines[0].split('\t');
```

Now we can delete the first line from the list of articles.

```js
/* Algo:
articles=lines[1..n]
*/

// Delete first line from the array of articles
var articles = lines.slice(1);
```

Then for each article we need to recover each cell by cutting the line at each tabulation. Next, we will create a hash per article and store the content of each cell indexed by corresponding column header. For convenience, we want to store the parsed articles in a array.

```js
/* Algo:
parsed=array()
foreach article in articles: {
  cells=split(article, '\t')
  hash={}
  for index=1; index<=cells.length; i++: {  
    hash[headers[i]]=cell[index]
  }
  parsed.push(hash)
}
*/

// Create array of parsed articles
var parsed = [];
// Foreach article
articles.forEach(article => {
  // Split article in an array of cells
  var cells = article.split('\t');
  // Create a hash for current article
  var hash = {};
  // Foreach cell
  cells.forEach((cell, index) => {
    // Store the cell value in the hash, using the header at the same index as key
    hash[headers[index]] = cell;
  });
  // Store the hash in parsed array
  parsed.push(hash);
});
```

Note that we can use some tricks specific to javascript language to shorten the code

```js
// articles is an array
// map function execute a function for each item of an array and return an array of same length containing the results
var reduced = articles.map(article => {
  // article is a sting
  // split function return an array
  // reduce function execute a function for each item of an array and return an object
  return article.split('\t').reduce((hash, cell, index) => {
    hash[headers[index]] = cell;
    // In our case, reduce function return an hash
    return hash;
  }, {});
});
```

After parsing the input, we have a array of hash with each information indexed using the column label from our original table.

## Formating

Now we wish to output the data in specific format:

> Title. First Author *et al*. *Journal* **issue** (year)

## TO BE CONTINUED
