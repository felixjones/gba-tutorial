# What is this?

A tutorial for writing GBA homebrew software in the modern age.

```
<ul>
  {% for category in site.categories %}
    <h3>{{ category[0] }}</h3>
    <ul>
      {% for post in category[1] %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endfor %}
    </ul>
  {% endfor %}
</ul>
```
