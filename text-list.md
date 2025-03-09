---
layout: minimal
title: Search
---


{% assign workshops = site.data.workshop_list_scratch | sort_natural: "Title" %}
{% assign seriesList = site.data.workshop_list_scratch | map: "Series" | uniq | sort_natural %}

{% for series in seriesList %}
  <h1 class="text-list-h1">{{ site.data.workshop_series[series] | default: series }}</h1>
  <ul>
  {% for page in workshops %}
    {% if page["Series"] == series %}
      <li> <a href="{{ page["URL"] }}" class="text-list-result"> {{ page["Title"] }} </a> </li>
    {% endif %}
  {% endfor %}
  </ul>
{% endfor %}