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

<div class="content-tab-container content-tab-container--top-level" data-tab-group="knowledge-base-language">
  <div class="content-tab-header" role="group" aria-label="Code language">
    <button type="button" class="content-tab-btn active" data-target="csharp" aria-pressed="true">C#</button>
    <button type="button" class="content-tab-btn" data-target="python" aria-pressed="false">Python</button>
    <button type="button" class="content-tab-btn" data-target="rest" aria-pressed="false">REST API</button>
  </div>

  <div class="content-tab-pane active" data-content="csharp" markdown="1">
In Azure AI Search, a *knowledge base* is a top-level object that orchestrates [agentic retrieval](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview) and establishes default parameters for query execution. A knowledge base configuration includes:

+ Knowledge sources that point to searchable content.
+ An optional LLM for query planning, answer synthesis, or web content summarization.
+ Custom properties that control cross-source routing, selection criteria, and object encryption.

## Prerequisites

+ An Azure AI Search service with one or more [knowledge sources](https://learn.microsoft.com/en-us/azure/search/agentic-knowledge-source-overview#supported-knowledge-sources).

+ (Conditional) A Microsoft Foundry resource with a [supported LLM](#supported-models) deployment. An LLM is required for web knowledge sources. For other knowledge sources, an LLM is optional in the `2026-08-01-preview` API version and unsupported in the `2026-04-01` API version.

+ Permission to create knowledge bases. Configure [keyless authentication](https://learn.microsoft.com/en-us/azure/search/search-get-started-rbac) with the **Search Service Contributor** role assigned to your user account (recommended) or use an [admin API key](https://learn.microsoft.com/en-us/azure/search/search-security-api-keys).

+ (Conditional) If your knowledge base specifies an LLM, enable a [managed identity](https://learn.microsoft.com/en-us/azure/search/search-how-to-managed-identities) for your search service, and then assign the **Cognitive Services User** role to your search service's managed identity on the Foundry resource.

+ [.NET 8](https://dotnet.microsoft.com/download/dotnet/8.0) or later.

+ Required [`Azure.Search.Documents`](https://www.nuget.org/packages/Azure.Search.Documents) package:

  + For `2026-08-01-preview` features, the latest preview package: `dotnet add package Azure.Search.Documents --prerelease`

  + For `2026-04-01` features, the latest stable package: `dotnet add package Azure.Search.Documents`

+ For keyless authentication, the [`Azure.Identity`](https://www.nuget.org/packages/Azure.Identity) package: `dotnet add package Azure.Identity`

### Supported models

Use one of the following LLMs from Azure OpenAI in Foundry Models:

+ `gpt-4o` (deprecated)
+ `gpt-4o-mini` (deprecated)
+ `gpt-4.1` (deprecated)
+ `gpt-4.1-mini` (deprecated)
+ `gpt-4.1-nano` (deprecated)
+ `gpt-5`
+ `gpt-5-mini`
+ `gpt-5-nano`
+ `gpt-5.1`
+ `gpt-5.2`
+ `gpt-5.4`
+ `gpt-5.4-mini`
+ `gpt-5.4-nano`
+ `gpt-5.5`
+ `gpt-5.6-sol`
+ `gpt-5.6-terra`
+ `gpt-5.6-luna`

Azure OpenAI determines regional availability for the deployment you select. For deployment instructions, see [Deploy Microsoft Foundry Models in the Foundry portal](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/deploy-models-openai).

## Check for existing knowledge bases

A knowledge base is a top-level, reusable object. Knowing about existing knowledge bases is helpful for either reuse or naming new objects.

Run the following code to list existing knowledge bases by name.

```csharp
// List knowledge bases by name
using Azure.Search.Documents.Indexes;

var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential);
var knowledgeBases = indexClient.GetKnowledgeBasesAsync();

Console.WriteLine("Knowledge Bases:");

await foreach (var kb in knowledgeBases)
{
    Console.WriteLine($"  - {kb.Name}");
}
```

**Reference:** [SearchIndexClient](https://learn.microsoft.com/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient)

You can also return a single knowledge base by name to review its JSON definition.

```csharp
using Azure.Search.Documents.Indexes;
using System.Text.Json;

var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential);

// Specify the knowledge base name to retrieve
string kbNameToGet = "earth-knowledge-base";

// Get a specific knowledge base definition
var knowledgeBaseResponse = await indexClient.GetKnowledgeBaseAsync(kbNameToGet);
var kb = knowledgeBaseResponse.Value;

// Serialize to JSON for display
string json = JsonSerializer.Serialize(kb, new JsonSerializerOptions { WriteIndented = true });
Console.WriteLine(json);
```

**Reference:** [SearchIndexClient](https://learn.microsoft.com/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient)

The following JSON is an example response for a knowledge base.

```json
{
  "name": "my-kb",
  "description": "A sample knowledge base.",
  "retrievalInstructions": null,
  "answerInstructions": null,
  "outputMode": null,
  "knowledgeSources": [
    {
      "name": "my-blob-ks"
    }
  ],
  "models": [],
  "encryptionKey": null,
  "retrievalReasoningEffort": {
    "kind": "low"
  }
}
```

## Create a knowledge base

Run the following code to create a knowledge base. To choose the right API version for your agentic retrieval scenario, see [Feature availability](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview?tabs=quickstarts#feature-availability).

<div class="content-tab-container content-tab-container--inline">
  <div class="content-tab-header">
    <button class="content-tab-btn active" data-target="2026-08-01-preview">2026-08-01-preview</button>
    <button class="content-tab-btn" data-target="2026-04-01">2026-04-01</button>
  </div>

<div class="content-tab-pane active" data-content="2026-08-01-preview" markdown="1">

```csharp
// Create a knowledge base
using Azure.Search.Documents.Indexes;
using Azure.Search.Documents.Indexes.Models;
using Azure.Search.Documents.KnowledgeBases.Models;
using Azure.Identity;

var indexClient = new SearchIndexClient(new Uri(searchEndpoint), new DefaultAzureCredential());

var aoaiParams = new AzureOpenAIVectorizerParameters
{
    ResourceUri = new Uri(aoaiEndpoint),
    DeploymentName = aoaiGptDeployment,
    ModelName = aoaiGptModel,
};

var knowledgeBase = new KnowledgeBase(
    name: "my-kb",
    knowledgeSources: new KnowledgeSourceReference[]
    {
        new KnowledgeSourceReference("hotels-ks"),
        new KnowledgeSourceReference("earth-at-night-ks")
    }
)
{
    Description = "This knowledge base handles questions directed at two unrelated sample indexes.",
    RetrievalInstructions = "Use the hotels knowledge source for queries about where to stay, otherwise use the earth at night knowledge source.",
    AnswerInstructions = "Answer in two concise sentences.",
    OutputMode = KnowledgeRetrievalOutputMode.AnswerSynthesis,
    Models = { new KnowledgeBaseAzureOpenAIModel(azureOpenAIParameters: aoaiParams) },
    RetrievalReasoningEffort = new KnowledgeRetrievalAutoReasoningEffort()
};

await indexClient.CreateOrUpdateKnowledgeBaseAsync(knowledgeBase);
Console.WriteLine($"Knowledge base '{knowledgeBase.Name}' created or updated successfully.");
```

**Reference:** [SearchIndexClient](https://learn.microsoft.com/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient?view=azure-dotnet-preview&preserve-view=true), [KnowledgeBase](https://learn.microsoft.com/en-us/dotnet/api/azure.search.documents.indexes.models.knowledgebase?view=azure-dotnet-preview&preserve-view=true)

</div>

<div class="content-tab-pane" data-content="2026-04-01" markdown="1">

```csharp
// Create a knowledge base
using Azure.Search.Documents.Indexes;
using Azure.Search.Documents.Indexes.Models;
using Azure.Identity;

var indexClient = new SearchIndexClient(new Uri(searchEndpoint), new DefaultAzureCredential());

var knowledgeBase = new KnowledgeBase(
    name: "my-kb",
    knowledgeSources: new KnowledgeSourceReference[]
    {
        new KnowledgeSourceReference("hotels-ks"),
        new KnowledgeSourceReference("earth-at-night-ks")
    }
)
{
    Description = "This knowledge base handles questions directed at two unrelated sample indexes."
};

await indexClient.CreateOrUpdateKnowledgeBaseAsync(knowledgeBase);
Console.WriteLine($"Knowledge base '{knowledgeBase.Name}' created or updated successfully.");
```

**Reference:** [SearchIndexClient](https://learn.microsoft.com/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient?view=azure-dotnet&preserve-view=true), [KnowledgeBase](https://learn.microsoft.com/en-us/dotnet/api/azure.search.documents.indexes.models.knowledgebase?view=azure-dotnet&preserve-view=true)

</div>

</div>

After you create a knowledge base, you can update its properties at any time. If the knowledge base is in use, updates take effect on the subsequent retrieval call.

### Configure CORS for browser-based retrieval (preview)

{: .important }
> Cross-origin resource sharing (CORS) allows browser-based applications to request data directly from the service. Depending on your CORS configuration, external web pages might access or invoke the service and its data by using the user's browser context. This access can create security threats. Enabling CORS is at your own risk.

To allow browser-based applications to call the retrieve action directly from the client side, configure `corsOptions` on your knowledge base. This policy specifies which allowed origins can send cross-origin requests.

The following example restricts retrieval calls to a single trusted frontend origin.

```csharp
using Azure.Identity;
using Azure.Search.Documents.Indexes;
using Azure.Search.Documents.Indexes.Models;

var indexClient = new SearchIndexClient(new Uri(searchEndpoint), new DefaultAzureCredential());

var knowledgeBase = new KnowledgeBase(
    name: "browser-chat-kb",
    knowledgeSources: new[] { new KnowledgeSourceReference("product-docs-ks") }
)
{
    Description = "A knowledge base that allows one browser app origin.",
    CorsOptions = new CorsOptions(new[] { "https://myapp.example.com" })
    {
        MaxAgeInSeconds = 300
    }
};

await indexClient.CreateOrUpdateKnowledgeBaseAsync(knowledgeBase);
```

**Reference:** [CorsOptions](https://learn.microsoft.com/en-us/dotnet/api/azure.search.documents.indexes.models.corsoptions?view=azure-dotnet-preview&preserve-view=true), [KnowledgeBase](https://learn.microsoft.com/en-us/dotnet/api/azure.search.documents.indexes.models.knowledgebase?view=azure-dotnet-preview&preserve-view=true)

If you omit `corsOptions`, the knowledge base blocks cross-origin browser requests by default.

## Query a knowledge base

After you create a knowledge base, call the [retrieve action or MCP endpoint](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-retrieve) to query it.

## Delete a knowledge base

If you no longer need the knowledge base or need to rebuild it on your search service, run the following code to delete the object.

```csharp
// Delete a knowledge base
using Azure.Search.Documents.Indexes;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential);

await indexClient.DeleteKnowledgeBaseAsync(knowledgeBaseName);
System.Console.WriteLine($"Knowledge base '{knowledgeBaseName}' deleted successfully.");
```

**Reference:** [SearchIndexClient](https://learn.microsoft.com/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient?view=azure-dotnet-preview&preserve-view=true)

## Related content

+ [Agentic retrieval in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview)
+ [Query a knowledge base](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-retrieve)
+ [Migrate agentic retrieval code](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-migrate)  </div>

  <div class="content-tab-pane" data-content="python" markdown="1">
In Azure AI Search, a *knowledge base* is a top-level object that orchestrates [agentic retrieval](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview) and establishes default parameters for query execution. A knowledge base configuration includes:

+ Knowledge sources that point to searchable content.
+ An optional LLM for query planning, answer synthesis, or web content summarization.
+ Custom properties that control cross-source routing, selection criteria, and object encryption.

## Prerequisites

+ An Azure AI Search service with one or more [knowledge sources](https://learn.microsoft.com/en-us/azure/search/agentic-knowledge-source-overview#supported-knowledge-sources).

+ (Conditional) A Microsoft Foundry resource with a [supported LLM](#supported-models) deployment. An LLM is required for web knowledge sources. For other knowledge sources, an LLM is optional in the `2026-08-01-preview` API version and unsupported in the `2026-04-01` API version.

+ Permission to create knowledge bases. Configure [keyless authentication](https://learn.microsoft.com/en-us/azure/search/search-get-started-rbac) with the **Search Service Contributor** role assigned to your user account (recommended) or use an [admin API key](https://learn.microsoft.com/en-us/azure/search/search-security-api-keys).

+ (Conditional) If your knowledge base specifies an LLM, enable a [managed identity](https://learn.microsoft.com/en-us/azure/search/search-how-to-managed-identities) for your search service, and then assign the **Cognitive Services User** role to your search service's managed identity on the Foundry resource.

+ [Python 3.8](https://www.python.org/downloads/) or later.

+ Required [`azure-search-documents`](https://pypi.org/project/azure-search-documents/#history) package:

  + For `2026-08-01-preview` features, the latest preview package: `pip install --pre azure-search-documents`

  + For `2026-04-01` features, the latest stable package: `pip install azure-search-documents`

+ For keyless authentication, the [`azure-identity`](https://pypi.org/project/azure-identity/) package: `pip install azure-identity`

### Supported models

Use one of the following LLMs from Azure OpenAI in Foundry Models:

+ `gpt-4o` (deprecated)
+ `gpt-4o-mini` (deprecated)
+ `gpt-4.1` (deprecated)
+ `gpt-4.1-mini` (deprecated)
+ `gpt-4.1-nano` (deprecated)
+ `gpt-5`
+ `gpt-5-mini`
+ `gpt-5-nano`
+ `gpt-5.1`
+ `gpt-5.2`
+ `gpt-5.4`
+ `gpt-5.4-mini`
+ `gpt-5.4-nano`
+ `gpt-5.5`
+ `gpt-5.6-sol`
+ `gpt-5.6-terra`
+ `gpt-5.6-luna`

Azure OpenAI determines regional availability for the deployment you select. For deployment instructions, see [Deploy Microsoft Foundry Models in the Foundry portal](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/deploy-models-openai).

## Check for existing knowledge bases

A knowledge base is a top-level, reusable object. Knowing about existing knowledge bases is helpful for either reuse or naming new objects.

Run the following code to list existing knowledge bases by name.

```python
# List knowledge bases by name
from azure.identity import DefaultAzureCredential
from azure.search.documents.indexes import SearchIndexClient

index_client = SearchIndexClient(endpoint = "<search-endpoint>", credential = DefaultAzureCredential())

for kb in index_client.list_knowledge_bases():
    print(f"  - {kb.name}")
```

**Reference:** [SearchIndexClient](https://learn.microsoft.com/en-us/python/api/azure-search-documents/azure.search.documents.indexes.searchindexclient)

You can also return a single knowledge base by name to review its JSON definition.

```python
# Get a knowledge base definition
from azure.identity import DefaultAzureCredential
from azure.search.documents.indexes import SearchIndexClient
import json

index_client = SearchIndexClient(endpoint = "<search-endpoint>", credential = DefaultAzureCredential())

kb = index_client.get_knowledge_base("<knowledge-base-name>")
print(json.dumps(kb.as_dict(), indent = 2))
```

**Reference:** [SearchIndexClient](https://learn.microsoft.com/en-us/python/api/azure-search-documents/azure.search.documents.indexes.searchindexclient)

The following JSON is an example response for a knowledge base.

```json
{
  "name": "my-kb",
  "description": "A sample knowledge base.",
  "retrievalInstructions": null,
  "answerInstructions": null,
  "outputMode": null,
  "knowledgeSources": [
    {
      "name": "my-blob-ks"
    }
  ],
  "models": [],
  "encryptionKey": null,
  "retrievalReasoningEffort": {
    "kind": "low"
  }
}
```

## Create a knowledge base

Run the following code to create a knowledge base. To choose the right API version for your agentic retrieval scenario, see [Feature availability](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview?tabs=quickstarts#feature-availability).

<div class="content-tab-container content-tab-container--inline">
  <div class="content-tab-header">
    <button class="content-tab-btn active" data-target="2026-08-01-preview">2026-08-01-preview</button>
    <button class="content-tab-btn" data-target="2026-04-01">2026-04-01</button>
  </div>

<div class="content-tab-pane active" data-content="2026-08-01-preview" markdown="1">

```python
# Create a knowledge base
from azure.identity import DefaultAzureCredential
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import (
    AzureOpenAIVectorizerParameters,
    KnowledgeBase,
    KnowledgeBaseAzureOpenAIModel,
    KnowledgeSourceReference,
)
from azure.search.documents.knowledgebases.models import (
    KnowledgeRetrievalAutoReasoningEffort,
    KnowledgeRetrievalOutputMode,
)

index_client = SearchIndexClient(endpoint = "<search-endpoint>", credential = DefaultAzureCredential())

aoai_params = AzureOpenAIVectorizerParameters(
    resource_url = "<aoai-endpoint>",
    deployment_name = "<aoai-gpt-deployment>",
    model_name = "<aoai-gpt-model>",
)

knowledge_base = KnowledgeBase(
    name = "my-kb",
    description = "This knowledge base handles questions directed at two unrelated sample indexes.",
    retrieval_instructions = "Use the hotels knowledge source for queries about where to stay, otherwise use the earth at night knowledge source.",
    answer_instructions = "Answer in two concise sentences.",
    output_mode = KnowledgeRetrievalOutputMode.ANSWER_SYNTHESIS,
    knowledge_sources = [
        KnowledgeSourceReference(name = "hotels-ks"),
        KnowledgeSourceReference(name = "earth-at-night-ks"),
    ],
    models = [KnowledgeBaseAzureOpenAIModel(azure_open_ai_parameters = aoai_params)],
    encryption_key = None,
    retrieval_reasoning_effort = KnowledgeRetrievalAutoReasoningEffort(),
)

index_client.create_or_update_knowledge_base(knowledge_base)
print(f"Knowledge base '{knowledge_base.name}' created or updated successfully.")
```

**Reference:** [SearchIndexClient](https://learn.microsoft.com/en-us/python/api/azure-search-documents/azure.search.documents.indexes.searchindexclient), [KnowledgeBase](https://learn.microsoft.com/en-us/python/api/azure-search-documents/azure.search.documents.indexes.models.knowledgebase)

</div>

<div class="content-tab-pane" data-content="2026-04-01" markdown="1">

```python
# Create a knowledge base
from azure.identity import DefaultAzureCredential
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import KnowledgeBase, KnowledgeSourceReference

index_client = SearchIndexClient(endpoint = "<search-endpoint>", credential = DefaultAzureCredential())

knowledge_base = KnowledgeBase(
    name = "my-kb",
    description = "This knowledge base handles questions directed at two unrelated sample indexes.",
    knowledge_sources = [
        KnowledgeSourceReference(name = "hotels-ks"),
        KnowledgeSourceReference(name = "earth-at-night-ks"),
    ],
    encryption_key = None,
)

index_client.create_or_update_knowledge_base(knowledge_base)
print(f"Knowledge base '{knowledge_base.name}' created or updated successfully.")
```

**Reference:** [SearchIndexClient](https://learn.microsoft.com/en-us/python/api/azure-search-documents/azure.search.documents.indexes.searchindexclient), [KnowledgeBase](https://learn.microsoft.com/en-us/python/api/azure-search-documents/azure.search.documents.indexes.models.knowledgebase)

</div>

</div>

After you create a knowledge base, you can update its properties at any time. If the knowledge base is in use, updates take effect on the subsequent retrieval call.

### Configure CORS for browser-based retrieval (preview)

{: .important }
> Cross-origin resource sharing (CORS) allows browser-based applications to request data directly from the service. Depending on your CORS configuration, external web pages might access or invoke the service and its data by using the user's browser context. This access can create security threats. Enabling CORS is at your own risk.

To allow browser-based applications to call the retrieve action directly from the client side, configure `corsOptions` on your knowledge base. This policy specifies which allowed origins can send cross-origin requests.

The following example restricts retrieval calls to a single trusted frontend origin.

```python
from azure.identity import DefaultAzureCredential
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import (
    CorsOptions,
    KnowledgeBase,
    KnowledgeSourceReference,
)

index_client = SearchIndexClient(endpoint="<search-endpoint>", credential=DefaultAzureCredential())

knowledge_base = KnowledgeBase(
    name="browser-chat-kb",
    description="A knowledge base that allows one browser app origin.",
    knowledge_sources=[KnowledgeSourceReference(name="product-docs-ks")],
    cors_options=CorsOptions(
        allowed_origins=["https://myapp.example.com"],
        max_age_in_seconds=300,
    ),
)

index_client.create_or_update_knowledge_base(knowledge_base)
```

**Reference:** [CorsOptions](https://learn.microsoft.com/en-us/python/api/azure-search-documents/azure.search.documents.indexes.models.corsoptions), [KnowledgeBase](https://learn.microsoft.com/en-us/python/api/azure-search-documents/azure.search.documents.indexes.models.knowledgebase)

If you omit `corsOptions`, the knowledge base blocks cross-origin browser requests by default.

## Query a knowledge base

After you create a knowledge base, call the [retrieve action or MCP endpoint](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-retrieve) to query it.

## Delete a knowledge base

If you no longer need the knowledge base or need to rebuild it on your search service, run the following code to delete the object.

```python
# Delete a knowledge base
from azure.identity import DefaultAzureCredential
from azure.search.documents.indexes import SearchIndexClient

index_client = SearchIndexClient(endpoint = "<search-endpoint>", credential = DefaultAzureCredential())
index_client.delete_knowledge_base("<knowledge-base-name>")
print(f"Knowledge base deleted successfully.")
```

**Reference:** [SearchIndexClient](https://learn.microsoft.com/en-us/python/api/azure-search-documents/azure.search.documents.indexes.searchindexclient)

## Related content

+ [Agentic retrieval in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview)
+ [Query a knowledge base](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-retrieve)
+ [Migrate agentic retrieval code](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-migrate)  </div>

  <div class="content-tab-pane" data-content="rest" markdown="1">
In Azure AI Search, a *knowledge base* is a top-level object that orchestrates [agentic retrieval](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview) and establishes default parameters for query execution. A knowledge base configuration includes:

+ Knowledge sources that point to searchable content.
+ An optional LLM for query planning, answer synthesis, or web content summarization.
+ Custom properties that control cross-source routing, selection criteria, and object encryption.

## Prerequisites

+ An Azure AI Search service with one or more [knowledge sources](https://learn.microsoft.com/en-us/azure/search/agentic-knowledge-source-overview#supported-knowledge-sources).

+ (Conditional) A Microsoft Foundry resource with a [supported LLM](#supported-models) deployment. An LLM is required for web knowledge sources. For other knowledge sources, an LLM is optional in the `2026-08-01-preview` API version and unsupported in the `2026-04-01` API version.

+ Permission to create knowledge bases. Configure [keyless authentication](https://learn.microsoft.com/en-us/azure/search/search-get-started-rbac) with the **Search Service Contributor** role assigned to your user account (recommended) or use an [admin API key](https://learn.microsoft.com/en-us/azure/search/search-security-api-keys).

+ (Conditional) If your knowledge base specifies an LLM, enable a [managed identity](https://learn.microsoft.com/en-us/azure/search/search-how-to-managed-identities) for your search service, and then assign the **Cognitive Services User** role to your search service's managed identity on the Foundry resource.

+ Required Search Service REST API version:

  + For preview features: [2026-08-01-preview](/rest/api/searchservice/operation-groups?view=rest-searchservice-2026-08-01-preview&preserve-view=true)

  + For generally available features: [2026-04-01](/rest/api/searchservice/operation-groups?view=rest-searchservice-2026-04-01&preserve-view=true)

+ For keyless authentication, include a [Microsoft Entra ID token](search-get-started-rbac.md?pivots=rest#get-token) in the `Authorization` header of each HTTP request.

### Supported models

Use one of the following LLMs from Azure OpenAI in Foundry Models:

+ `gpt-4o` (deprecated)
+ `gpt-4o-mini` (deprecated)
+ `gpt-4.1` (deprecated)
+ `gpt-4.1-mini` (deprecated)
+ `gpt-4.1-nano` (deprecated)
+ `gpt-5`
+ `gpt-5-mini`
+ `gpt-5-nano`
+ `gpt-5.1`
+ `gpt-5.2`
+ `gpt-5.4`
+ `gpt-5.4-mini`
+ `gpt-5.4-nano`
+ `gpt-5.5`
+ `gpt-5.6-sol`
+ `gpt-5.6-terra`
+ `gpt-5.6-luna`

Azure OpenAI determines regional availability for the deployment you select. For deployment instructions, see [Deploy Microsoft Foundry Models in the Foundry portal](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/deploy-models-openai).

## Check for existing knowledge bases

A knowledge base is a top-level, reusable object. Knowing about existing knowledge bases is helpful for either reuse or naming new objects.

Run the following code to list existing knowledge bases by name.

```http
# List knowledge bases
GET {{search-endpoint}}/knowledgebases?api-version={{api-version}}&$select=name
Content-Type: application/json
Authorization: Bearer {{search-access-token}}
```

**Reference:** [Knowledge Bases - List](/rest/api/searchservice/knowledge-bases/list)

You can also return a single knowledge base by name to review its JSON definition.

```http
# Get knowledge base
GET {{search-endpoint}}/knowledgebases/{{knowledge-base-name}}?api-version={{api-version}}
Content-Type: application/json
Authorization: Bearer {{search-access-token}}
```

**Reference:** [Knowledge Bases - Get](/rest/api/searchservice/knowledge-bases/get)

The following JSON is an example response for a knowledge base.

```json
{
  "name": "my-kb",
  "description": "A sample knowledge base.",
  "retrievalInstructions": null,
  "answerInstructions": null,
  "outputMode": null,
  "knowledgeSources": [
    {
      "name": "my-blob-ks"
    }
  ],
  "models": [],
  "encryptionKey": null,
  "retrievalReasoningEffort": {
    "kind": "low"
  }
}
```

## Create a knowledge base

Run the following code to create a knowledge base. To choose the right API version for your agentic retrieval scenario, see [Feature availability](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview?tabs=quickstarts#feature-availability).

<div class="content-tab-container content-tab-container--inline">
  <div class="content-tab-header">
    <button class="content-tab-btn active" data-target="2026-08-01-preview">2026-08-01-preview</button>
    <button class="content-tab-btn" data-target="2026-04-01">2026-04-01</button>
  </div>

<div class="content-tab-pane active" data-content="2026-08-01-preview" markdown="1">

```http
# Create a knowledge base
PUT {{search-endpoint}}/knowledgebases/my-kb?api-version=2026-08-01-preview
Content-Type: application/json
Authorization: Bearer {{search-access-token}}

{
    "name" : "my-kb",
    "description": "This knowledge base handles questions directed at two unrelated sample indexes.",
    "retrievalInstructions": "Use the hotels knowledge source for queries about where to stay, otherwise use the earth at night knowledge source.",
    "answerInstructions": "Answer in two concise sentences.",
    "outputMode": "answerSynthesis",
    "knowledgeSources": [
        {
            "name": "hotels-ks"
        },
        {
            "name": "earth-at-night-ks"
        }
    ],
    "models" : [
        {
            "kind": "azureOpenAI",
            "azureOpenAIParameters": {
                "resourceUri": "{{aoai-endpoint}}",
                "deploymentId": "gpt-5.4-mini",
                "modelName": "gpt-5.4-mini"
            }
        }
    ],
    "encryptionKey": null,
    "retrievalReasoningEffort": {
        "kind": "auto"
    }
}
```

**Reference:** [Knowledge Bases - Create or Update](/rest/api/searchservice/knowledge-bases/create-or-update?view=rest-searchservice-2026-08-01-preview&preserve-view=true)

</div>

<div class="content-tab-pane" data-content="2026-04-01" markdown="1">

```http
# Create a knowledge base
PUT {{search-endpoint}}/knowledgebases/my-kb?api-version=2026-04-01
Content-Type: application/json
Authorization: Bearer {{search-access-token}}

{
    "name" : "my-kb",
    "description": "This knowledge base handles questions directed at two unrelated sample indexes.",
    "knowledgeSources": [
        {
            "name": "hotels-ks"
        },
        {
            "name": "earth-at-night-ks"
        }
    ],
    "encryptionKey": null
}
```

**Reference:** [Knowledge Bases - Create or Update](/rest/api/searchservice/knowledge-bases/create-or-update?view=rest-searchservice-2026-04-01&preserve-view=true)

</div>

</div>

After you create a knowledge base, you can update its properties at any time. If the knowledge base is in use, updates take effect on the subsequent retrieval call.

### Configure CORS for browser-based retrieval (preview)

{: .important }
> Cross-origin resource sharing (CORS) allows browser-based applications to request data directly from the service. Depending on your CORS configuration, external web pages might access or invoke the service and its data by using the user's browser context. This access can create security threats. Enabling CORS is at your own risk.

To allow browser-based applications to call the retrieve action directly from the client side, configure `corsOptions` on your knowledge base. This policy specifies which allowed origins can send cross-origin requests.

The following example restricts retrieval calls to a single trusted frontend origin.

```http
PUT {{search-endpoint}}/knowledgebases/browser-chat-kb?api-version=2026-08-01-preview
Content-Type: application/json
Authorization: Bearer {{search-access-token}}

{
  "name": "browser-chat-kb",
  "description": "A knowledge base that allows one browser app origin.",
  "knowledgeSources": [
    {
      "name": "product-docs-ks"
    }
  ],
  "corsOptions": {
    "allowedOrigins": [
      "https://myapp.example.com"
    ],
    "maxAgeInSeconds": 300
  }
}
```

**Reference**: [Knowledge Bases - Create or Update](/rest/api/searchservice/knowledge-bases/create-or-update?view=rest-searchservice-2026-08-01-preview&preserve-view=true)

If you omit `corsOptions`, the knowledge base blocks cross-origin browser requests by default.

## Query a knowledge base

After you create a knowledge base, call the [retrieve action or MCP endpoint](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-retrieve) to query it.

## Delete a knowledge base

If you no longer need the knowledge base or need to rebuild it on your search service, run the following code to delete the object.

```http
# Delete a knowledge base
DELETE {{search-endpoint}}/knowledgebases/{{knowledge-base-name}}?api-version={{api-version}}
Authorization: Bearer {{search-access-token}}
```

**Reference:** [Knowledge Bases - Delete](/rest/api/searchservice/knowledge-bases/delete?view=rest-searchservice-2026-04-01&preserve-view=true)

## Related content

+ [Agentic retrieval in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview)
+ [Query a knowledge base](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-retrieve)
+ [Migrate agentic retrieval code](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-migrate)
  </div>
</div>

---

[Back to top](#top)

Thanks for visiting my portfolio! If you have any questions or feedback, please feel free to reach out.