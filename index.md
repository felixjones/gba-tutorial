# What is this?

A tutorial for writing GBA homebrew software in the modern age.

<ol>
  {% for collection in site.collections %}
  <li>
    <h2>{{collection.label}}</h2>
    <ol>
      {% assign posts = site[collection.label] | sort: 'ordering' %}
      {% for post in posts %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </li>
      {% endfor %}
    </ol>
  </li>
  {% endfor %}
</ol>
