---
layout: portfolio
title: Create and manage a knowledge base
parent: Azure AI Search
grand_parent: Microsoft
nav_order: 4
permalink: /microsoft/azure-ai-search/create-manage-knowledge-base
---

# Create and manage a knowledge base for agentic retrieval
{: .no_toc }

{% capture csharp_content %}
{% include how-tos/knowledge-base-csharp.md %}
{% endcapture %}

{% capture python_content %}
{% include how-tos/knowledge-base-python.md %}
{% endcapture %}

{% capture rest_content %}
{% include how-tos/knowledge-base-rest.md %}
{% endcapture %}

<div class="content-tab-container content-tab-container--top-level" data-tab-group="knowledge-base-language">
  <div class="content-tab-header">
    <button type="button" class="content-tab-btn active" data-target="csharp">C#</button>
    <button type="button" class="content-tab-btn" data-target="python">Python</button>
    <button type="button" class="content-tab-btn" data-target="rest">REST API</button>
  </div>
  <div class="content-tab-pane active" data-content="csharp">
    {{ csharp_content | markdownify }}
  </div>
  <div class="content-tab-pane" data-content="python">
    {{ python_content | markdownify }}
  </div>
  <div class="content-tab-pane" data-content="rest">
    {{ rest_content | markdownify }}
  </div>
</div>

---

[Back to top](#top)

Thanks for visiting my portfolio! If you have any questions or feedback, please feel free to reach out.
