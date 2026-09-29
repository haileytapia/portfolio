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

In Azure AI Search, a *knowledge base* is a top-level object that orchestrates [agentic retrieval](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview) and establishes default parameters for query execution. A knowledge base configuration includes:

+ Knowledge sources that point to searchable content.
+ An optional LLM for query planning, answer synthesis, or web content summarization.
+ Custom properties that control cross-source routing, selection criteria, and object encryption.


<style>
  /* Outer Language Switcher Styles */
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

  /* Inner API Version Switcher Styles */
  .kb-version-container {
    margin: 1rem 0;
    border: 1px solid #e2e8f0;
    border-radius: 6px;
    background: #fafafa;
    overflow: hidden;
  }
  .kb-version-header {
    display: flex;
    background: #f1f5f9;
    border-bottom: 1px solid #e2e8f0;
    padding: 0 0.75rem;
    gap: 0.5rem;
  }
  .kb-version-btn {
    background: transparent;
    border: none;
    padding: 0.5rem 0.75rem;
    font-size: 0.75rem;
    font-weight: 500;
    cursor: pointer;
    color: #475569;
    border-bottom: 2px solid transparent;
    margin-bottom: -1px;
  }
  .kb-version-btn.active {
    color: #2563eb;
    font-weight: 600;
    border-bottom-color: #2563eb;
    background: #fafafa;
  }
  .kb-version-pane {
    display: none;
    padding: 1rem;
    background-color: #ffffff;
  }
  .kb-version-pane.active {
    display: block;
  }
</style>

<div class="kb-lang-container">
  <div class="kb-lang-header">
    <button type="button" class="kb-lang-btn active" data-target="lang-csharp">C#</button>
    <button type="button" class="kb-lang-btn" data-target="lang-python">Python</button>
    <button type="button" class="kb-lang-btn" data-target="lang-rest">REST API</button>
  </div>

  <div class="kb-lang-pane active" data-content="lang-csharp" markdown="1">
    {% include how-tos/knowledge-base-csharp.md %}
  </div>

  <div class="kb-lang-pane" data-content="lang-python" markdown="1">
    {% include how-tos/knowledge-base-python.md %}
  </div>

  <div class="kb-lang-pane" data-content="lang-rest" markdown="1">
    {% include how-tos/knowledge-base-rest.md %}
  </div>
</div>

<script>
  (function() {
    document.addEventListener("click", function (event) {
      // Handle Outer Language Tabs
      const langBtn = event.target.closest(".kb-lang-btn");
      if (langBtn) {
        const target = langBtn.getAttribute("data-target");
        const container = langBtn.closest(".kb-lang-container");
        if (container && target) {
          container.querySelectorAll(".kb-lang-btn").forEach(b => b.classList.toggle("active", b === langBtn));
          container.querySelectorAll(".kb-lang-pane").forEach(p => p.classList.toggle("active", p.getAttribute("data-content") === target));
        }
        return;
      }

      // Handle Inner API Version Tabs
      const verBtn = event.target.closest(".kb-version-btn");
      if (verBtn) {
        const target = verBtn.getAttribute("data-target");
        const container = verBtn.closest(".kb-version-container");
        if (container && target) {
          container.querySelectorAll(".kb-version-btn").forEach(b => b.classList.toggle("active", b === verBtn));
          container.querySelectorAll(".kb-version-pane").forEach(p => p.classList.toggle("active", p.getAttribute("data-content") === target));
        }
      }
    });
  })();
</script>

---

[Back to top](#top)

Thanks for visiting my portfolio! If you have any questions or feedback, please feel free to reach out.