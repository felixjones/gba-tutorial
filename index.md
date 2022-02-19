# What is this?

A tutorial for writing GBA homebrew software in the modern age.

<ol>
{% assign collections = site.collections | where_exp: "item", "item.label != 'posts'" %}
{% for collection in collections %}
  <li>
    <a>{{ collection.title }}</a>
    <ol>
    {% assign posts = site[collection.label] | sort: 'ordering' %}
    {% for post in posts %}
      <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a></li>
    {% endfor %}
    </ol>
  </li>
{% endfor %}
</ol>
