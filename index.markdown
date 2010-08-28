---
layout: default
---
<br/>
<h1 style="text-align:center">Billie HomePage</h1>

<br />

<p>
Welcome, I am Billie Zhang, a open source enthusiast. 
</p>


<p><br /><b>My Blog:</b></p>
  <ul class="posts">
    {% for post in site.posts %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>

<p><br /><b>Contact Information:</b></p>

<blockquote>
<p>
billie.jean.zhang at gmail.com
</p>
</blockquote>


