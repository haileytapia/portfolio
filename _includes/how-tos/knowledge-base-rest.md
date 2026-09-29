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

### `2026-08-01-preview`

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

### `2026-04-01`

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
