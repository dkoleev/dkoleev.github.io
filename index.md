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

# My own projects:
* **[Survival Island](https://play.google.com/store/apps/details?id=com.airbit.outcast)** Mobile survival game set in an open 3D world with more than 1 million downloads.
* **[UniGSC](https://github.com/dkoleev/UniGSC)** Plugin for flexible use of Google Sheets as game configs.


# Team projects:
* **[Florescence](https://play.google.com/store/apps/details?id=com.gamegarden.florescence&hl=en)** AFK Arena for women

---


## My Articles

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}
    </li>
  {% endfor %}
</ul>
