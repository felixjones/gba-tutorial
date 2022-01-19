# What is this?

A tutorial for writing GBA homebrew software in the modern age.

<ol>
{% for p in site.introduction %}
  <h2>
    <a href="{{ p.url }}">
      {{ p.title }}
    </a>
  </h2>
  <p>{{ p.content | markdownify }}</p>
{% endfor %}
</ol>
