---
layout: page
title: domains
titleheader: Application Domains
permalink: /domains/
nav: true
description: Metapages collecting information on topics of interest in the lab. 
showtitle: true
---

<div class="projects grid">
  {% assign sorted_items = site.domains | sort: "title" %}
  {% for item in sorted_items %}
      {% if item.publish %}
          <div class="grid-item">
              {% if item.redirect %}
                  <a href="{{ item.redirect }}" target="_blank">
              {% else %}
                  <a href="{{ item.url | relative_url }}">
              {% endif %}
              <div class="card hoverable">
                {% if item.img %}
                <img src="{{ item.img | relative_url }}" alt="item thumbnail">
                {% endif %}
                <div class="card-body">
                  <h2 class="card-title">{{ item.title }}</h2>
                  <p class="card-text">{{ item.description }}</p>
                </div>
              </div>
            </a>
          </div>
      {% endif %}
{% endfor %}
</div>