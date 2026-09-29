In Azure AI Search, a *knowledge base* is a top-level object that orchestrates [agentic retrieval](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview) and establishes default parameters for query execution. A knowledge base configuration includes:

+ Knowledge sources that point to searchable content.

+ An optional LLM for query planning, answer synthesis, or web content summarization. Supported tasks vary by API version and knowledge source type.

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

Run the following code to create a knowledge base.

{: .important }
> The `2026-04-01` API version only accepts generally available knowledge source types and supports minimal, extractive retrieval. It doesn't support preview-only capabilities, such as LLM-based query planning, answer synthesis, and configurable reasoning effort. For full functionality, use the `2026-08-01-preview` API version.

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

<div class="content-tab-pane active" data-content="2026-04-01" markdown="1">

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

After you create a knowledge base, you can update its properties at any time. If the knowledge base is in use, updates take effect on the next retrieval.

### Configure CORS for browser-based retrieve calls (preview)

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
+ [Migrate agentic retrieval code](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-migrate)