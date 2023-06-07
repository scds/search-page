---
layout: default
title: Home
nav_order: 1
---

<!-- https://jekyllrb.com/tutorials/csv-to-table/ -->

{% assign workshops = site.data.workshop_list 
    | sort: "title" 
%}

{% assign dmds_workshops = workshops
    | where_exp: "item", "item.tags contains 'DMDS'"
%}

{% assign dash_workshops = workshops
    | where_exp: "item", "item.tags contains 'DASH'"
%}

# Online Learning

New skills are just a click away. These workshop recordings and online modules will teach you about data analysis, digital scholarship, innovative software, and more.

## Do More with Digital Scholarship

<p markdown="1">
{% for row in dmds_workshops %}
[{{ row["title"] }}]({{ row["url"] }})  
{% endfor %}
</p>

## DASH (Data Analysis Support Hub)

<p markdown="1">
{% for row in dash_workshops %}
[{{ row["title"] }}]({{ row["url"] }})  
{% endfor %}
</p>

