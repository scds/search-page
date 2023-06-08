---
layout: default
title: Search
nav_order: 2
---

<!-- https://jekyllrb.com/tutorials/csv-to-table/ -->
<!-- https://github.com/christian-fei/Simple-Jekyll-Search -->

{% assign workshops = site.data.workshop_list 
    | sort: "title" 
%}

# Online Learning

New skills are just a click away. These workshop recordings and online modules will teach you about data analysis, digital scholarship, innovative software, and more.

<div id="search-container">

<input type="text" id="search-inputt" placeholder="search...">

<div style="display:flex">

<div style="width: 70%; padding-right: 1em">
<ul id="results-container">

{% for row in workshops %}
<li>
<p><a href="{{row["url"]}}">{{row["title"]}}</a><br>{{row["description"]}}</p>
</li>
{% endfor %}

</ul>
</div>

<div style="width: 30%; font-size: small">
<fieldset>

<b>Year</b><br>
<input type="checkbox" id="vehicle1" name="vehicle1" value="Bike">
<label for="vehicle1">2023</label><br>

<input type="checkbox" id="vehicle1" name="vehicle1" value="Bike">
<label for="vehicle1">2022</label><br>

<input type="checkbox" id="vehicle1" name="vehicle1" value="Bike">
<label for="vehicle1">2021</label><br>

<b>Series</b><br>
<input type="checkbox" id="vehicle1" name="vehicle1" value="Bike">
<label for="vehicle1">DMDS - Do More with Digital Scholarship</label><br>

<input type="checkbox" id="vehicle1" name="vehicle1" value="Bike">
<label for="vehicle1">DASH - Data Analysis Support Hub</label><br>


</fieldset>
</div>

</div>

</div>

<!-- Script pointing to search-script.js -->
<script src="/assets/js/search-script.js" type="text/javascript"></script>

<!-- Configuration -->
<script>


var sjs = SimpleJekyllSearch({
  searchInput: document.getElementById('search-inputt'),
  resultsContainer: document.getElementById('results-container'),
  json: '/search.json',
  noResultsText: 'No result found!',
  searchResultTemplate: '
  <li>
    <p>
      <a href="{url}">{title}</a>
      <br>
      {tags}
    </p>
  </li>
  ',
  templateMiddleware: function(prop, value, template) {
    if (prop === 'tags') {
      var strr = "";
      function createHTMLTag(tag) { return `<p class="label">${tag}</p>`;}
      function createTag(tag) { strr = strr.concat(" ", createHTMLTag(tag));  }
      value.forEach(createTag);
      console.log(strr);
      return strr;
    }
  }
})
</script>