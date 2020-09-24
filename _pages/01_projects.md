---
layout: project
title: Projects
permalink: /projects/
---

# Projects

{% for projects in site.projects %}


{% if projects.category == "project" %}

<div class="pubitem">
  <div class="pubteaser">
    <a href="{{site.url  | append: site.baseurl | append: projects.permalink}}">
      <img src="../{{ projects.image }}" alt="{{projects.image}} project teaser"/>
    </a>
  </div>
   <h3><a href="{{site.url  | append: site.baseurl | append: projects.permalink}}">{{ projects.title }}</a></h3>
  <p>{{ projects.description }}</p>
</div>

<br>

{% if forloop.last == false %}
<hr>
{% endif %}

<!-- <div class="publication"> 
<table>
    <td width="40%" valign="center"><img src="../{{ projects.image }}" alt="{{projects.image}} publication teaser" width="200" height="50" style="border-style: none">
    <td width="60%" valign="top">
        <h3><a href="">{{projects.title}}</a></h3>
        <br>
        <p>{{ projects.description }}</p>
    </td> 
    </td>
</table>
</div>
<br>


<div class="publication"> 
<table>
    <td  valign="center"><img src="../{{ projects.image }}" alt="{{projects.image}} publication teaser" style="border-style: none">
    <td width="60%" valign="top">
        <h3><a href="">{{projects.title}}</a></h3>
        <br>
        <p>{{ projects.description }}</p>
    </td> 
    </td>
</table>
</div>
<br> -->

{% endif %}

{% endfor %} 
