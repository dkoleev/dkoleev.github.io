---
layout: default
title: Home
---
# Welcome to My Blog

### About Me
Hi, I'm Dmitry Koleev, a [brief description about yourself]. I write about [topics you cover in your blog]. You can follow me on [social media, GitHub link, etc.].

---

<p style="color:green;">
  This is my hacker-style themed page, powered by Jekyll and GitHub Pages.
</p>

```sh
# Displaying some hacker-style content:
- Custom Raspberry Pi projects
- Penetration testing and ethical hacking
- Open-source software enthusiast
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
