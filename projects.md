---
layout: page
title: Projects
dek: Every build, from single-evening mini projects to a semester-long industry-mentored system. Ordered newest first.
permalink: /projects/
---

<div class="grid" style="margin-top: 10px;">
{% for post in site.posts %}
  <article class="card">
    <div class="card-top">
      <span class="status-tag">
        {% if post.status == "completed" %}
          <span class="led led--green"></span> Completed
        {% else %}
          <span class="led led--amber"></span> {{ post.status | default: "In progress" }}
        {% endif %}
      </span>
      <span class="meta-row">{{ post.date | date: "%b %Y" }}</span>
    </div>
    <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
    <p class="summary">{{ post.dek | default: post.excerpt | strip_html | truncate: 150 }}</p>
    <div class="tags">
      {% for t in post.tags %}<span class="tag">{{ t }}</span>{% endfor %}
    </div>
  </article>
{% endfor %}
</div>
