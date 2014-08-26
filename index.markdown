---
layout: default
---
<br/>
<h1 style="text-align:center">Billie HomePage</h1>
<br />

<p>
  Welcome, I am Billie Zhang, an open source enthusiast and a RoR fan.
</p>

<p><br /><b>My Blog:</b></p>
  <ul class="posts">
    {% for post in site.posts %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>

<p><br /><b>My Project</b></p>
<ul>
  <li><a href="https://github.com/billie66">Github</a></li>
  <li><a href="http://billie66.github.com/TLCL/index.html">Book</a></li>
</ul>

<p><br /><b>Contact Information:</b></p>
<blockquote>
  <p>billiecoder at gmail.com</p>
</blockquote>


