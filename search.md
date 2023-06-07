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

<div style="border-style: solid; width: 80%">
<ul id="results-container">

{% for row in workshops %}
<li>
<p><a href="{{row["url"]}}">{{row["title"]}}</a><br>{{row["description"]}}</p>
</li>
{% endfor %}

</ul>
</div>

<div style="border-style: solid; width: 20%">
test
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
  searchResultTemplate: '<li><p><a href="{url}">{title}</a><br>{description}</p></li>'
})
</script>