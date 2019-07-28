---
layout: page
title: Training Events
permalink: /events/
---

**Upcoming events:**

  * 19-21 Aug, 2019 - ATLAS Software Carpentries Training
    * Lawrence Berkeley National Laboratory
    * [Indico page](https://indico.cern.ch/event/816946/)

**Past events:**

  * 22-26 Jul, 2019 - Computational and Data Science for High Energy Physics (CoDaS-HEP) 2019 School
    * Princeton University
    * [Webpage](http://codas-hep.org/)

  * 10 Jun, 2019 - FIRST-HEP/ATLAS Software Training
    * Argonne National Laboratory
    * [Indico page](https://indico.cern.ch/event/827231/)

  * 3-4 Jun, 2019 - An introduction to programming for STEM teachers
    * University of Puerto Rico at Mayaguez
    * [Indico page](https://indico.cern.ch/event/817539/)

  * 24-26 Apr, 2019 - Machine Learning Hackathon for UPRM Students
    * University of Puerto Rico at Mayaguez
    * [Indico page](https://indico.cern.ch/event/809812/)

  * 1-2 Apr, 2019 - Software Carpentry Workshop 
    * Fermi National Accelerator Laboratory
    * [Indico page](https://indico.fnal.gov/event/20233)


**Next attempt**

{% comment %}
Go through the list and produce a breakdown of the events in reverse
chronological order, grouped by months
{% endcomment %}

{% assign yearlist = "2019, 2018, 2017, 2016" | split: ", " %}
{% assign monthlist= "12, 11, 10, 09, 08, 07, 06, 05, 04, 03, 02, 01" | split: ", " %}

{% for yearidx in yearlist %}
{% for monthidx in monthlist %}
{% assign selected_array = "" | split: ',' %}
{% for event_hash in site.data.events  %}
  {% assign event = event_hash[1] %}
  {% assign eventyear = event.startdate | date: "%Y" %}
  {% assign eventmonth = event.startdate | date: "%m" %}
  {% if eventyear == yearidx and eventmonth == monthidx %}
     {% assign selected_array = selected_array | push: event %}
  {% endif %}
{% endfor %}

{% assign selected_array = selected_array | sort: 'startdate' | reverse %}
{% assign hdrprint = true %}
<ul>
{% for event in selected_array %}
  {% if hdrprint == true %}
    <br><h5>{{event.startdate | date: "%B, %Y"}}</h5>
    {% assign hdrprint = false %}
  {% endif %}
  <li>{{event.startdate | date: "%-d %b" }}{{event.enddate | date: " - %-d %b" }}, {{event.startdate | date: "%Y" }} - <a href="{{event.meetingurl}}">{{event.name}}</a> (<i>{{event.location}}</i>)</li>
{% endfor %}
</ul>

{% endfor %}
{% endfor %}
<br>


