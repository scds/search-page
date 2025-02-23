---
layout: minimal
title: Search
---

<link rel="stylesheet" href="./assets/css/search-tool.css">


<div id="text-results-container">
  <!-- This is where results are automatically filled -->
</div>


<script src="assets/javascript/jquery.js"></script>
<script>
var title = "";
var json = "";
var search = "";
$.getJSON('data.json', function(obj) {
  json = obj;
  console.log(json);
  let results = document.getElementById('text-results-container');
  let categories = {};

  for (const [key, value] of Object.entries(json)) {
    if(value.series in categories) {
      categories[value.series].push(value);
    } else {
      categories[value.series] = [value];
    }
  }

  console.log(categories);

  for (const [key, value] of Object.entries(categories).sort()) {
    results.innerHTML += `<h1>${key}</h1>`;
    value.sort((a, b) => a.title.localeCompare(b.title));

    for (const workshop of value) {
      results.innerHTML += `<p>${workshop.title}</p>`;
    }
  }
})
</script>