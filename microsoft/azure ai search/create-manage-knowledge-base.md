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

<div class="test-tab-container">
  <div class="test-tab-header">
    <button type="button" class="test-tab-btn active" onclick="switchTestTab(event, 'pane-csharp')">C#</button>
    <button type="button" class="test-tab-btn" onclick="switchTestTab(event, 'pane-python')">Python</button>
    <button type="button" class="test-tab-btn" onclick="switchTestTab(event, 'pane-rest')">REST API</button>
  </div>

  <div id="pane-csharp" class="test-tab-pane active">
    <h3>C# Content Works!</h3>
    <p>This is the C# tab text.</p>
  </div>

  <div id="pane-python" class="test-tab-pane">
    <h3>Python Content Works!</h3>
    <p>This is the Python tab text.</p>
  </div>

  <div id="pane-rest" class="test-tab-pane">
    <h3>REST Content Works!</h3>
    <p>This is the REST API tab text.</p>
  </div>
</div>

<style>
  .test-tab-container {
    margin: 1.5rem 0;
    border: 1px solid #e2e8f0;
    border-radius: 8px;
    background: #ffffff;
    overflow: hidden;
  }
  .test-tab-header {
    display: flex;
    background: #f8fafc;
    border-bottom: 1px solid #e2e8f0;
    padding: 0 1rem;
    gap: 0.5rem;
  }
  .test-tab-btn {
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
  .test-tab-btn:hover {
    color: #0f172a;
  }
  .test-tab-btn.active {
    color: #7c3aed;
    font-weight: 600;
    border-bottom-color: #7c3aed;
    background: #ffffff;
  }
  .test-tab-pane {
    display: none;
    padding: 1.5rem;
  }
  .test-tab-pane.active {
    display: block;
  }
</style>

<script>
  function switchTestTab(evt, paneId) {
    const container = evt.target.closest('.test-tab-container');
    container.querySelectorAll('.test-tab-btn').forEach(b => b.classList.remove('active'));
    container.querySelectorAll('.test-tab-pane').forEach(p => p.classList.remove('active'));
    evt.currentTarget.classList.add('active');
    document.getElementById(paneId).classList.add('active');
  }
</script>