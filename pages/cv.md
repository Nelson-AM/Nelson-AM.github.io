---
layout: page
title: CV
permalink: /cv/
---

A selection of my professional career.

## Work Experience

{% for job in site.data.work %}
<p>
<b>{{ job.function }}</b> at {{ job.company }}, {{ job.location }}<br />
<span class="post-meta">{{ job.dates.start }} -- {{ job.dates.end }}</span><br />
Tools of the trade: {{ job.tools }}
</p>
{% endfor %}

## Education

{% for study in site.data.education %}
<p>
<b>{{ study.name }}</b> at {{ study.alma-mater }}<br />
<span class="post-meta">{{ study.dates.start }} -- {{ study.dates.end }}</span><br />
{% if study.major %}Major: {{ study.major }}<br />{% endif %}
{% if study.minor %}Minor: {{ study.minor }}<br />{% endif %}
</p>
{% endfor %}
