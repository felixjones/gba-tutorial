# What is this?

A tutorial for writing GBA homebrew software in the modern age.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

<ol>
  {% for category in site.categories %}
    <h3>{{ category[0] }}</h3>
    <ol>
      {% for post in category[1] %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endfor %}
    </ol>
  {% endfor %}
</ol>
