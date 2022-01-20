# What is this?

A tutorial for writing GBA homebrew software in the modern age.

<ol>
  <li>
    <a>Introduction</a>
    <ol>
      {% assign sorted = site.introduction | sort: 'ordering' %}
      {% for post in sorted %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </li>
      {% endfor %}
    </ol>
  </li>

  <li>
    <a>Test A</a>
    <ol>
      {% assign sorted = site.testA | sort: 'ordering' %}
      {% for post in sorted %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </li>
      {% endfor %}
    </ol>
  </li>

  <li>
    <a>Test B</a>
    <ol>
      {% assign sorted = site.testB | sort: 'ordering' %}
      {% for post in sorted %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </li>
      {% endfor %}
    </ol>
  </li>
</ol>
