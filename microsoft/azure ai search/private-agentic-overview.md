---
layout: portfolio
title: Overview
parent: "Tutorial: Private agentic retrieval"
grand_parent: Azure AI Search
nav_order: 1
permalink: /microsoft/azure-ai-search/private-agentic-retrieval-overview
---

# Tutorial: Deploy private agentic retrieval
{: .no_toc }

July 13, 2026 ∙ [Original article](https://learn.microsoft.com/en-us/azure/foundry/agents/how-to/foundry-iq-tutorial-private-overview)
{: .fs-5 : .fw-300 }

This three-part tutorial series describes how to deploy an end-to-end private agentic retrieval architecture by using Microsoft Foundry and Azure AI Search. It explains how inbound connectivity, outbound dependencies, and retrieval runtime fit together across the deployment.

In this tutorial, you:

- [x] Establish inbound private connectivity between Foundry and Azure AI Search.
- [x] Configure outbound private dependencies from Azure AI Search.
- [x] Validate end-to-end retrieval with a knowledge source, knowledge base, project connection, and agent.

## What is private agentic retrieval?

Private agentic retrieval is a pattern where an agent retrieves knowledge over private network paths instead of public endpoints. In this tutorial, the agent-to-Search path and the Search-to-Storage path stay on private endpoints, shared private links, and private DNS zones. The Search-to-Foundry embedding dependency is also configured for private outbound access, but the ingestion-time embedding call currently still relies on the Foundry trusted-service bypass.

{: .tip }
> This tutorial is the private network version of [Tutorial: Build an end-to-end agentic retrieval solution using Azure AI Search](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-create-pipeline). Both tutorials use managed identities and role-based access, but this version emphasizes private connectivity and adds inbound and outbound validation at each step.

## Services in this tutorial

The deployment provisions the following services. You interact with each service differently throughout this tutorial.

| Service | Role |
| --- | --- |
| Foundry (resource and project) | Orchestrates the agent runtime and hosts the project connection, the agent, and a GPT-5 family model that powers the agent. In part three, you also deploy the `text-embedding-3-large` embedding model that Azure AI Search uses to vectorize content. |
| Azure AI Search | Ingests and vectorizes your private blob content into a knowledge source, and then serves agentic retrieval through a knowledge base and its MCP endpoint. Makes a private outbound call to Azure Blob Storage for content access. For the Foundry embedding dependency, this tutorial uses the `openai_account` shared private link for the target resource, and the ingestion-time embedding call currently also relies on the trusted-service bypass. |
| Azure Blob Storage | Stores the source documents that the knowledge source ingests and indexes for agentic retrieval. |
| Azure Cosmos DB | Stores agent state for the standard agent setup, including messages, conversation history, and agent metadata. The deployment provisions it automatically, and you don't configure or use it directly. |

## Parts in this tutorial

The following table shows what you accomplish in each part, the components involved, and how to confirm success before moving to the next part.

| Part | Outcome | Components | Success criteria |
| --- | --- | --- | --- |
| 1 - Inbound | A private request path from Foundry to Azure AI Search. | <ul><li>Virtual network and subnets</li><li>Private endpoints</li><li>Private DNS zones</li><li>Foundry and Azure AI Search private access settings</li></ul> | From your in-VNet client, the Foundry and Azure AI Search endpoints resolve to private IP addresses and accept connections on TCP 443. |
| 2 - Outbound | Private dependency paths from Azure AI Search to Azure Blob Storage and Foundry. | <ul><li>Shared private links</li><li>Target-side approvals</li><li>Managed identities</li><li>Dependency RBAC for Azure Blob Storage and Foundry</li></ul> | The Azure Blob Storage and Foundry shared private links report an `Approved` state, and the Azure AI Search managed identity holds its assigned blob and model roles. |
| 3 - Retrieval validation | An agent that returns grounded answers over the private retrieval path. | <ul><li>Knowledge source</li><li>Knowledge base</li><li>Project connection</li><li>Agent configuration</li></ul> | The validation prompt returns an answer grounded in your blob content, with citations to the source documents. |

## Next step

[Set up private inbound connectivity](/portfolio/microsoft/azure-ai-search/private-agentic-retrieval-inbound){: .btn .btn-purple }