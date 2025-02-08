---
layout: minimal
title: Search
nav_order: 2
---

<link rel="stylesheet" href="./assets/css/search-tool.css">

<!-- https://jekyllrb.com/tutorials/csv-to-table/ -->
<!-- https://github.com/christian-fei/Simple-Jekyll-Search -->

<div class="search-filter-container">
  <div class="search-container" id="search-container">
    <div class="search-container-left">
      <input class="tool-search-input" type="text" id="search-inputt" placeholder="Search...">
      <button class="filter-button" type="button">🝖</button>
      <div class="filters-container-mobile">
        <fieldset>
          <details class="yearsFilters" style="all: unset;">
            <summary style="border-bottom: none; margin-bottom: 0; padding-bottom: 0.25em;">Year</summary>
          </details>
          <details class="seriesFilters" style="all: unset;">
            <summary style="border-bottom: none; margin-bottom: 0; padding-bottom: 0.25em;">Series</summary>
          </details>
          <details class="topicsFilters" style="all: unset;">
            <summary style="border-bottom: none; margin-bottom: 0; padding-bottom: 0.25em;">Topics</summary>
          </details>
          <details class="softwareFilters" style="all: unset;">
            <summary style="border-bottom: none; margin-bottom: 0; padding-bottom: 0.25em;">Software</summary>
          </details>
        </fieldset>
      </div>
      <div class="results-container" id="results-container">
        <!-- This is where results are automatically filled -->
      </div>
    </div>
    <!-- Filters -->
    <div class="filters-container">
      <fieldset>
        <details open class="yearsFilters" style="all: unset;">
          <summary style="border-bottom: none; margin-bottom: 0; padding-bottom: 0.25em;">Year</summary>
        </details>
        <details open class="seriesFilters" style="all: unset;">
          <summary style="border-bottom: none; margin-bottom: 0; padding-bottom: 0.25em;">Series</summary>
        </details>
        <details open class="topicsFilters" style="all: unset;">
          <summary style="border-bottom: none; margin-bottom: 0; padding-bottom: 0.25em;">Topics</summary>
        </details>
        <details open class="softwareFilters" style="all: unset;">
          <summary style="border-bottom: none; margin-bottom: 0; padding-bottom: 0.25em;">Software</summary>
        </details>
      </fieldset>
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
  $.getJSON('search.json', function(objj) {
    search = objj;

    var sjs = SimpleJekyllSearch({
      searchInput: document.getElementById('search-inputt'),
      resultsContainer: document.getElementById('results-container'),
      json: search,
      noResultsText: 'No result found!',
      limit: 12,
      fuzzy: true,
      searchResultTemplate: '<!--{title}, {url}-->
      <div style="background-color: #AAD5E1; padding: 10px; border-radius: 10px; margin: 5px; height: auto;">
        <a target="_parent" href="{url}" style="font-family: Arial; font-size: 18px !important; line-height: 1.25; font-weight: bold; display:block">
        <object data="{image}" type="image/png" height="auto" width="100%" style="background-color: white;">
          <object data="assets/img/{series_image}_image.png" type="image/png" height="auto" width="100%" style="background-color: white;">
            <img src="assets/img/unknownImageLocation.png" height="100%" style="background-color: white;">
          </object>
        </object>
        <p style="margin-top: 5px; margin-bottom: 0px; font-family: Arial; font-size: 18px !important; line-height: 1.25; display:block">{title}</p>
        </a>
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
          return strr;
        }

        if (prop === 'year') {
          var strr = "";
          function createYear(year) { strr = strr.concat(year, ", ");  }
          value = value.split(";");
          value.forEach(createYear);
          return strr.slice(0, -2);
        }

        if (prop === 'url' || prop === 'year' || prop === 'series' || prop === 'image') {
          return getProperty(title, prop);
        }

        if (prop === "series_image") {
          return getProperty(title, "series").toLowerCase();
        }
      }
    })
  });
})




</script>
