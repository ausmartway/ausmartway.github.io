---
layout: page
title: Projects
permalink: /projects/
---

A collection of my work in DevSecOps, Infrastructure as Code, and cloud security.

## Infrastructure as Code

{% for project in site.projects %}
  {% if project.category == "Infrastructure as Code" %}
### [{{ project.title }}]({{ project.url | relative_url }})
{{ project.description }}

[View on GitHub](https://github.com/ausmartway/{{ project.title | slugify }})
  {% endif %}
{% endfor %}

## Security

{% for project in site.projects %}
  {% if project.category == "Security" %}
### [{{ project.title }}]({{ project.url | relative_url }})
{{ project.description }}

[View on GitHub](https://github.com/ausmartway/{{ project.title | slugify }})
  {% endif %}
{% endfor %}

## Cloud Security

{% for project in site.projects %}
  {% if project.category == "Cloud Security" %}
### [{{ project.title }}]({{ project.url | relative_url }})
{{ project.description }}

[View on GitHub](https://github.com/ausmartway/{{ project.title | slugify }})
  {% endif %}
{% endfor %}