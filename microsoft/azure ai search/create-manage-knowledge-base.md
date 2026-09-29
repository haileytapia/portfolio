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

August 12, 2026 ∙ [Original article](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-create-knowledge-base)
{: .fs-5 : .fw-300 }

<div class="kb-tab-container">
  <div class="kb-tab-header">
    <button type="button" class="kb-tab-btn active" onclick="switchKbTab(event, 'csharp')">C#</button>
    <button type="button" class="kb-tab-btn" onclick="switchKbTab(event, 'python')">Python</button>
    <button type="button" class="kb-tab-btn" onclick="switchKbTab(event, 'rest')">REST API</button>
  </div>

  <div id="kb-pane-csharp" class="kb-tab-pane active" markdown="1">
    {% include how-tos/knowledge-base-csharp.md %}
  </div>

  <div id="kb-pane-python" class="kb-tab-pane" markdown="1">
    {% include how-tos/knowledge-base-python.md %}
  </div>

  <div id="kb-pane-rest" class="kb-tab-pane" markdown="1">
    {% include how-tos/knowledge-base-rest.md %}
  </div>
</div>

<style>
  .kb-tab-container {
    margin: 1.5rem 0;
    border: 1px solid #e2e8f0;
    border-radius: 8px;
    background: #ffffff;
    overflow: hidden;
  }
  .kb-tab-header {
    display: flex;
    background: #f8fafc;
    border-bottom: 1px solid #e2e8f0;
    padding: 0 1rem;
    gap: 0.5rem;
  }
  .kb-tab-btn {
    background: transparent;
    border: none;
    padding: 0.75rem 1rem;
    font-size: 0.875rem;
    font-weight: 500;
    cursor: pointer;
    color: #64748b;
    border-bottom: 2px solid transparent;
    margin-bottom: -1px;
  }
  .kb-tab-btn:hover {
    color: #0f172a;
  }
  .kb-tab-btn.active {
    color: #7c3aed;
    font-weight: 600;
    border-bottom-color: #7c3aed;
    background: #ffffff;
  }
  .kb-tab-pane {
    display: none;
    padding: 1.5rem;
  }
  .kb-tab-pane.active {
    display: block;
  }
</style>

<script>
  function switchKbTab(evt, lang) {
    const container = evt.target.closest('.kb-tab-container');
    
    container.querySelectorAll('.kb-tab-btn').forEach(b => b.classList.remove('active'));
    container.querySelectorAll('.kb-tab-pane').forEach(p => p.classList.remove('active'));
    
    evt.currentTarget.classList.add('active');
    document.getElementById('kb-pane-' + lang).classList.add('active');
  }
</script>

---

[Back to top](#top)

Thanks for visiting my portfolio! If you have any questions or feedback, please feel free to reach out.