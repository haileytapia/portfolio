---
layout: portfolio
title: Create and manage a knowledge base
parent: Azure AI Search
grand_parent: Microsoft
nav_order: 4
permalink: /microsoft/azure-ai-search/search-knowledge-base
---

# Create and manage a knowledge base for agentic retrieval
{: .no_toc }

August 12, 2026 ∙ [Original article](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-create-knowledge-base)
{: .fs-5 : .fw-300 }

<style>
  /* Self-contained styles for the KB Language Switcher */
  .kb-lang-container {
    margin: 1.5rem 0;
    width: 100%;
    background: #ffffff;
    border: 1px solid #e2e8f0;
    border-radius: 8px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.02);
    overflow: hidden;
  }
  .kb-lang-header {
    display: flex;
    overflow-x: auto;
    background: #f8fafc;
    border-bottom: 1px solid #e2e8f0;
    padding: 0 1rem;
    gap: 0.5rem;
    white-space: nowrap;
  }
  .kb-lang-btn {
    background: transparent;
    border: none;
    padding: 0.75rem 1rem;
    font-size: 0.875rem;
    font-weight: 500;
    cursor: pointer;
    color: #64748b;
    border-bottom: 2px solid transparent;
    margin-bottom: -1px;
    transition: all 0.15s ease;
  }
  .kb-lang-btn:hover {
    color: #0f172a;
  }
  .kb-lang-btn.active {
    color: #7c3aed;
    font-weight: 600;
    border-bottom-color: #7c3aed;
    background: #ffffff;
  }
  .kb-lang-pane {
    display: none;
    padding: 1.5rem;
    background-color: #ffffff;
  }
  .kb-lang-pane.active {
    display: block;
  }
</style>

<div class="kb-lang-container">
  <div class="kb-lang-header">
    <button type="button" class="kb-lang-btn active" data-target="kb-csharp">C#</button>
    <button type="button" class="kb-lang-btn" data-target="kb-python">Python</button>
    <button type="button" class="kb-lang-btn" data-target="kb-rest">REST API</button>
  </div>

  <div class="kb-lang-pane active" data-content="kb-csharp" markdown="1">
    {% include how-tos/knowledge-base-csharp.md %}
  </div>

  <div class="kb-lang-pane" data-content="kb-python" markdown="1">
    {% include how-tos/knowledge-base-python.md %}
  </div>

  <div class="kb-lang-pane" data-content="kb-rest" markdown="1">
    {% include how-tos/knowledge-base-rest.md %}
  </div>
</div>

<script>
  (function() {
    document.addEventListener("click", function (event) {
      const button = event.target.closest(".kb-lang-btn");
      if (!button) return;

      const target = button.getAttribute("data-target");
      if (!target) return;

      const container = button.closest(".kb-lang-container");
      if (!container) return;

      const buttons = container.querySelectorAll(".kb-lang-btn");
      const panes = container.querySelectorAll(".kb-lang-pane");

      buttons.forEach(b => b.classList.toggle("active", b === button));
      panes.forEach(p => p.classList.toggle("active", p.getAttribute("data-content") === target));
    });
  })();
</script>

---

[Back to top](#top)

Thanks for visiting my portfolio! If you have any questions or feedback, please feel free to reach out.