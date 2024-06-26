---
layout: default
title: Search
nav_order: 2
---

<!-- https://jekyllrb.com/tutorials/csv-to-table/ -->
<!-- https://github.com/christian-fei/Simple-Jekyll-Search -->

# Online Learning

New skills are just a click away. These workshop recordings and online modules will teach you about data analysis, digital scholarship, innovative software, and more.

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
<script src="../assets/javascript/search-script.js" type="text/javascript"></script>
<script src="../assets/javascript/jquery.js" type="text/javascript"></script>

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

function getOGImageFromURL(urlInput) {
  $.ajax({
      url: urlInput,
			error: function() {
				  return "https://t3.ftcdn.net/jpg/03/35/13/14/360_F_335131435_DrHIQjlOKlu3GCXtpFkIG1v0cGgM9vJC.jpg";
			}, 
      success: function(response){
          return "https://t3.ftcdn.net/jpg/03/35/13/14/360_F_335131435_DrHIQjlOKlu3GCXtpFkIG1v0cGgM9vJC.jpg";
      },
      complete: function(){
          return "https://t3.ftcdn.net/jpg/03/35/13/14/360_F_335131435_DrHIQjlOKlu3GCXtpFkIG1v0cGgM9vJC.jpg";
      }
  });
}

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
      <a href="{url}">
        {title}
        <img src="{getOGImageFromURL}" width="100%" style="border: 1px solid #000;">
      </a>
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

    if (prop === 'getOGImageFromURL') {
      return getOGImageFromURL(getProperty(title, prop));
    }
  }
})
</script>