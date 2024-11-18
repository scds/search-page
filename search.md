---
layout: minimal
title: Search
nav_order: 2
---

<!-- https://jekyllrb.com/tutorials/csv-to-table/ -->
<!-- https://github.com/christian-fei/Simple-Jekyll-Search -->

<div style="height:800px; overflow-y: clip">
  <div id="search-container" style="height:100%">
    <div style="display:flex; height: 100%">
      <div style="width: 70%; height: 100%; padding-right: 1em">
        <input style="width: 100%; height: 40px; border-radius: 10px; border: solid 1px gray; margin-bottom: 1em; padding-left: 1em; padding-right: 1em" type="text" id="search-inputt" placeholder="Search...">
        <div style="display:grid; grid-template-columns: 1fr 1fr 1fr; overflow-y:scroll; height: 740px" id="results-container">
          <!-- This is where results are automatically filled -->
        </div>
      </div>
      <!-- Filters -->
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
</div>

<!-- Script pointing to search-script.js -->
<script src="assets/javascript/jquery.js"></script>
<script src="assets/javascript/search-script.js" type="text/javascript"></script>

<script>
function getProperty(title, prop) {
  try {
    return json[title][prop]; 
  } catch(e) {
    console.log("json not initialized");
  }
}

var title = "";
var json = "";
var search = "";
$.getJSON('data.json', function(obj) {
  json = obj;
  $.getJSON('search.json', function(obj) {
    search = obj;

    var sjs = SimpleJekyllSearch({
      searchInput: document.getElementById('search-inputt'),
      resultsContainer: document.getElementById('results-container'),
      json: "search.json",
      noResultsText: 'No result found!',
      limit: 30,
      fuzzy: true,
      searchResultTemplate: '<!--{title}-->
      <div style="background-color: #ABBAEA; padding: 10px; border-radius: 10px; margin: 5px; height: auto">
        <img src="https://learn.scds.ca/dmds22-23/assets/img/3DPPoster.png">
        <a target="_parent" href="{url}" style="margin-top: 5px; font-family: Arial; font-size: 18px !important; line-height: 1.25; display:block">{title}</a>
        <p style="margin: 0px; font-family: Arial; font-size: 13px"> {series} - {year} </p>
      </div>
      ',
      templateMiddleware: function(prop, value, template) {
        if(prop === 'title') {
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

        if (prop === 'url' || prop === 'description' || prop === 'year' || prop === 'series') {
          return getProperty(title, prop);
        }
      }
    })
  });
})




</script>
