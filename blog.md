---
layout: default
title: Blog
permalink: /blog/
---

## Blog

<div style="margin-top: 24px;">
  {% for post in site.posts %}
  <div style="
    border-left: 4px solid #2c2c2c;
    padding: 14px 20px;
    margin-bottom: 24px;
    background-color: #f8f8f8;
    border-radius: 0 6px 6px 0;
  ">
    <h3 style="margin: 0 0 6px 0;">
      <a href="{{ post.url | relative_url }}" style="text-decoration: none; color: #2c2c2c;">
        {{ post.title }}
      </a>
    </h3>
    <p style="margin: 0; font-size: 0.85em; color: #888;">
      {{ post.date | date: "%B %d, %Y" }}
    </p>
    {% if post.description %}
    <p style="margin: 8px 0 0 0; font-size: 0.95em; color: #444;">
      {{ post.description }}
    </p>
    {% endif %}
  </div>
  {% else %}
  <p>No posts yet.</p>
  {% endfor %}
</div>