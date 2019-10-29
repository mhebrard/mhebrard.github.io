---
layout: main
title: Lesson 02 (2019-10-29)
description: Parse and format a list of articles.
---

In this lesson, we will read a list of articles information (title, authors...), parse the different types of data and format them according to our wish.

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

> Title. First Author *et al*. ***Journal*** **issue** (year)

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

At this point we can open the table that contains the list of articles, copy the data and paste the data input variable. To prove that we get the data inside our variable, we print it.

## Parsing

The `input` variable contains one string with all our data. If we want to manipulate the information we need to parse this string, i.e. cut the text in pieces.

First we need to recover the lines. To do so we cut the string each time we encounter `\n` that represent the special character `new line`. We can use the generic function `split` that take 2 arguments: The string we want to cut and a pattern we will use to cut the string. The split function return an array of strings, result of the cut.

```js
/* Algo:
lines = split input at each '\n'
*/

// Split input string into an array of lines
var lines = input.split('\n');
```

Notice that in our case, the first line is the header of the table. We will keep this first line aside in another variable for further use. We also need to recover the label of each column. To do so, we can cut the header line each time we encounter `\t` that represent the special character `tabulation`.

```js
/* Algo:
header = lines[0]
header = split header at each '\t'
*/

// Split the first line in an array of headers
var headers = lines[0].split('\t');
```

Now we can delete the first line from the list of articles.

```js
/* Algo:
articles = lines[1..end]
*/

// Delete first line from the array of articles
// Slice is function specific to javascript language that help us in that case
var articles = lines.slice(1);
```

Then for each article we need to recover each cell by cutting the line at each tabulation. Next, we will create a hashmap per article and store the content of each cell indexed by corresponding the column header. For convenience, we want to store the parsed articles in a array.

```js
/* Algo:
parsed = array()
for i from 0 to end of articles: do
  article = articles[i]
  cells = split article at each '\t'
  hash = {}
  for j from 1 to end of cells: do
    hash[headers[j]]=cells[j]
  end for j
  push hash in parsed
end for i
*/

// Create array of parsed articles
var parsed = [];
// Foreach article
for (i = 0; i < articles.length; i++) {
  var article = articles[i];
  // Split article in an array of cells
  var cells = article.split('\t');
  // Create a hashmap for current article
  var hash = {};
  // Foreach cell
  for (j = 0; j < cells.length; j++) {
    // Store the cell value in the hash, using the header at the same index as key
    hash[headers[j]] = cells[j];
  };
  // Store the hash in parsed array
  parsed.push(hash);
};
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

> Title. First Author *et al*. ***Journal*** **issue** (year)

First we can format the first article. As we wish to display the text on a HTML page we need to add some HTML tags to handle the style of our text. We build a string to combine each bit of information and style that we need. As each article have multiple authors, we need to cut the author list to display only the first one. We also need to extract the year from the date of the article.

```js
/* Algo:
article = article[0]
output = ''
output = output + article[Title]
authors = split article[Authors] at each ','
output = output + authors[0] + 'et al.' in italic
output = output + article[Journal] in bold and italic
output = output + article[Issue] in bold
date = split article[Date] at each ' '
output = output + ( date[0] )
*/

// Format first article
// Get first article
var article = parsed[0];
// Create string
var output = '';
// Add title
output += article['Title'] + ' ';
// Split authors
var authors = article['Authors'].split(',');
// Add first author
output += authors[0] + ' <i> et al.</i> ';
// Add journal
output += '<b><i>' + article['Journal'] + '</i><b> ';
// Add issue
output += '<b>' + article['Issue'] + '</b> ';
// Split date
var date = article['Date'].split(' ');
// Add date
output += '(' + date[0] + ')';
```

Now that we have formatted one article, we need to do the same series of instructions for each article in our list. We also need to create a list on our HTML page. We define a function, and call this fuction for each article in our list.

If we copy the instruction from the previous section, we will encounter an error. We might not have noticed before but our list of parsed articles contains an empty item due to the last `\n` of the input. If we proceed with a for loop over each item of the array, an error raizes because the last item of the array do not have any author. To prevent the error, we need to test if the item is empty.

```js
/* Algo
output = ''
output = output + <ul>
for i from 0 to end of articles: do
  if articles[i] is not empty: do
    output = output + <li>
    output = output + format(articles[i])
    output = output + </li>
  end if
end for i
output = output + </ul>
*/

// Create function format
function format(article) {
  // Create string
  var result = '';
  // Add title
  result += article['Title'] + ' ';
  // Split authors
  var authors = article['Authors'].split(',');
  // Add first author
  result += authors[0] + ' <i> et al.</i> ';
  // Add journal
  result += '<b><i>' + article['Journal'] + '</i></b> ';
  // Add issue
  result += '<b>' + article['Issue'] + '</b> ';
  // Split date
  var date = article['Date'].split(' ');
  // Add date
  result += '(' + date[0] + ')';
  // Return string
  return result;
}

// Create HTML string
output = '';
// Open an unordered list in HTML
output += '<ul>\n'
// For each article
for (i = 0; i < parsed.length; i++) {
  // Test if article is empty
  if (parsed[i]['Title'].length > 0) {
    // Open a list item in HTML
    output += '\t<li>';
    // Format the ieme article
    output += format(parsed[i]);
    // Close a list item in HTML
    output += '</li>\n';
  }
}
// Close an unordered list in HTML
output += '</ul>\n';
```

At this point we display a list of article formatted as we wished. Well done !

That's it for today.

## END
