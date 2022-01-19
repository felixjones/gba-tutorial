# What is this?

A tutorial for writing GBA homebrew software in the modern age.

<ol>
  {% assign sorted = site.introduction | sort: 'order' %}
  {% for post in sorted %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ol>
