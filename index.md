# What is this?

A tutorial for writing GBA homebrew software in the modern age.

<ol>
  {% for post in site.introduction %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ol>
