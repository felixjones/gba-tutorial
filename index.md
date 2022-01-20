# What is this?

A tutorial for writing GBA homebrew software in the modern age.

<ol>
{% assign sorted = site.collections | where_exp: "item", "item.label != 'posts'" %}
{% for collection in sorted %}
  <li>
    <a>{{ collection.title }}</a>
    <ol>
    {% for item in site[collection.label] %}
      <li><a href="{{ item.url }}">{{ item.title }}</a></li>
    {% endfor %}
    </ol>
  </li>
{% endfor %}
</ol>
