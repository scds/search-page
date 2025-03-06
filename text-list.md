---
layout: minimal
title: Search
---

<link rel="stylesheet" href="./assets/css/search-tool.css">

<div id="text-results-container">
  <!-- This is where results are automatically filled -->
  {{ site.data.workshop_list_scratch }}
</div>


<!-- <script src="assets/javascript/jquery.js"></script>
<script>
var title = "";
var json = "";
var search = "";
$.getJSON('data.json', function(obj) {
  json = obj;
  let results = document.getElementById('text-results-container');
  let categories = {};

  for (const [key, value] of Object.entries(json)) {
    if(value.series in categories) {
      categories[value.series].push(value);
    } else {
      categories[value.series] = [value];
    }
  }

  for (const [key, value] of Object.entries(categories).sort()) {
    results.innerHTML += `<h1>${key}</h1>`;
    value.sort((a, b) => a.title.localeCompare(b.title));
    
    let listToAdd = "<ul>\n";
    for (const workshop of value) {
      listToAdd += `<li><a href="${workshop.url}" class="text-list-result">${workshop.title}</a></li>\n`;
    }
    results.innerHTML += listToAdd + "</ul>\n";
  }
})
</script> -->