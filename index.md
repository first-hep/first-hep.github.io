---
#
# You don't need to edit this file, it's empty on purpose.
# Edit sleeks's default layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
#
layout: mainpage
title: FIRST-HEP
---

{% comment %}
Go through the list and produce a list of upcoming events as well as a
list of events in the past 90 days. Treat 6 days ago as "now" so that
ongoing events don't get prematurely flagged as recent.
{% endcomment %}
{% assign currentdatecmp = 'now' | date: "%s" %}
{% assign sixdaysago = 'now' | date: "%s" | minus: 518400 | date: "%b %d, %Y %I:%M %p -0500" | uri_encode | replace: "+","%20" | date: "%s"%}
{% assign ninetydaysago = 'now' | date: "%s" | minus: 7776000| date: "%b %d, %Y %I:%M %p -0500" | uri_encode | replace: "+","%20" | date: "%s"%}


{% assign selected_events = "" | split: ',' %}
<h4>Upcoming Events:</h4>
IRIS-HEP team members are involved in organizing the following events:
{% for event_hash in site.data.events %}
  {% assign event = event_hash[1] %}
  {% assign startdatecmp = event.startdate | date: "%s" %}
  {% if startdatecmp >= sixdaysago %}
     {% assign selected_events = selected_events | push: event %}
  {% endif %}
{% endfor %}

<ul>
{% assign selected_events = selected_events | sort: 'startdate' %}
{% for event in selected_events %}
  {% assign startdatecmp = event.startdate | date: "%s" %}
  <li> {{TXT}}{{event.startdate | date: "%-d %b" }}{{event.enddate | date: " - %-d %b" }}, {{event.startdate | date: "%Y" }} - <a href="{{event.meetingurl}}">{{event.name}}</a> (<i>{{event.location}}</i>)</li>
{% endfor %}
</ul>


{% assign selected_events = "" | split: ',' %}
<h4>Recent Events:</h4>
{% for event_hash in site.data.events  %}
  {% assign event = event_hash[1] %}
  {% assign startdatecmp = event.startdate | date: "%s" %}
  {% if startdatecmp < sixdaysago and startdatecmp > ninetydaysago %}
     {% assign selected_events = selected_events | push: event %}
  {% endif %}
{% endfor %}

<ul>
{% assign selected_events = selected_events | sort: 'startdate' | reverse %}
{% for event in selected_events  %}
  {% assign startdatecmp = event.startdate | date: "%s" %}
  {% if startdatecmp < sixdaysago and startdatecmp > ninetydaysago %}
  <li> {{TXT}}{{event.startdate | date: "%-d %b" }}{{event.enddate | date: " - %-d %b" }}, {{event.startdate | date: "%Y" }} - <a href="{{event.meetingurl}}">{{event.name}}</a> (<i>{{event.location}}</i>)</li>
  {% endif %}
{% endfor %}
</ul>

<h1>New Content</h1>

 <section class="blog">
   <h2> News Items 2 </h2>
   <div class="container">
     <div class="post-list" itemscope="" itemtype="http://schema.org/Blog">

       {% for post in site.posts %}
         {% include card.html %}
       {% endfor %}

       <!-- {% include pagination.html %} -->
     </div>
   </div>
 </section>



