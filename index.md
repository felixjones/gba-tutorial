# What is this?

A tutorial for writing GBA homebrew software in the modern age.

<ol>
  {% for collection in site.collections %}
  <li>
    <h2>{{collection.label}}</h2>
  </li>
  <li>
    <ol>
      {% assign sorted = site.introduction | sort: 'order' %}
      {% for post in sorted %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </li>
      {% endfor %}
    </ol>
  </li>
  {% endfor %}
</ol>
