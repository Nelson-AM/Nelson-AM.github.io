---
layout: page
title: CV
permalink: /CV/
---

A selection of my professional career.

## Work Experience

{% for job in site.data.work %}
<b>{{ job.function }}</b> at {{ job.company }}, {{ job.location }}

<span class="post-meta">{{ job.dates.start }} -- {{ job.dates.end }}</span>

Tools of the trade: {{ job.tools }}
{% endfor %}

## Education

{% for study in site.data.education %}
<b>{{ study.name }}</b> at {{ study.alma-mater }}

<span class="post-meta">{{ study.dates.start }} -- {{ study.dates.end }}<span>
{% endfor %}
