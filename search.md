---
layout: minimal
title: Search
nav_order: 2
---

<!-- https://jekyllrb.com/tutorials/csv-to-table/ -->
<!-- https://github.com/christian-fei/Simple-Jekyll-Search -->

<div id="search-container">

<input type="text" id="search-inputt" placeholder="search...">

<div style="display:flex">

<div style="width: 70%; padding-right: 1em">
<ul id="results-container">
Search!
</ul>
</div>


<div style="width: 30%; font-size: small">
<fieldset>

<div id="yearsFilters">

<b>Year</b><br>

</div>

<div id="seriesFilters">

<b>Series</b><br>

</div>


</fieldset>
</div>

</div>

</div>

<!-- Script pointing to search-script.js -->
<script src="{{site.github_repo_url}}assets/javascript/search-script.js" type="text/javascript"></script>
<script src="{{site.github_repo_url}}assets/javascript/jquery.js"></script>

<script>
var json = "";
$.getJSON('data.json', function(obj) {
    json = obj;
});

var search = "";
$.getJSON('search.json', function(obj) {
    search = obj;
});

function getProperty(title, prop) {
  return json[title][prop];    
}

var title = "";

var sjs = SimpleJekyllSearch({
  searchInput: document.getElementById('search-inputt'),
  resultsContainer: document.getElementById('results-container'),
  json: "search.json",
  noResultsText: 'No result found!',
  limit: 100,
  fuzzy: true,
  searchResultTemplate: '
  <li> <!-- {title} -->
    <p>
      <a href="{url}" target="_top">{title}</a>
    </p>
  </li>
  ',
  templateMiddleware: function(prop, value, template) {
    if (prop === 'title') {
      title = value;
    }

    if (prop === 'tags') {
      var strr = "";
      function createHTMLTag(tag) { return `<p class="label">${tag}</p>`;}
      function createTag(tag) { strr = strr.concat(" ", createHTMLTag(tag));  }
      value = value.split(", ");
      value.forEach(createTag);
      const regex = /\*/i;
      return strr;
    }

    if (prop === 'url' || prop === 'description') {
      return getProperty(title, prop);
    }
  }
})
</script>
