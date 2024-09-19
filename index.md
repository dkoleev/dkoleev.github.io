---
layout: default
title: Home
---
# Welcome to My Blog

### About Me
<p style="color:green;">
Hi, I'm Dmitry Koleev 👋
</p>


```sh
# Skills:
- Languages: C#, Python, Rust
- Editors: Unity Engine, Rider, VS Code, Bevy Engine, GODOT
- Custom Raspberry Pi projects
```

---


## Recent Articles

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}
    </li>
  {% endfor %}
</ul>
