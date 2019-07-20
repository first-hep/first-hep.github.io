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

<h1>New Content 2</h1>

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



