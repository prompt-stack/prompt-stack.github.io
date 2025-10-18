---
layout: page
title: Guides
permalink: /guides/
---

# Technical Guides

Deep-dives into AI-assisted development, Claude tools, and modern engineering practices.

---

{% for guide in site.guides %}
## [{{ guide.title }}]({{ guide.url }})

{{ guide.summary }}

**Tags:** {{ guide.tags | join: ", " }}
**Date:** {{ guide.date | date: "%B %d, %Y" }}

[Read more →]({{ guide.url }})

---
{% endfor %}
