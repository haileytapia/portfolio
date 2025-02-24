---
layout: default
title: Create a search service in the Azure portal
parent: Azure AI Search
grand_parent: Microsoft
nav_order: 1
permalink: /microsoft/azure-ai-search/create-search-service-portal
---

# Create an Azure AI Search service in the Azure portal
{: .no_toc }

February 21, 2025 ∙ [Original article](https://learn.microsoft.com/en-us/azure/search/search-create-service-portal)
{: .fs-5 : .fw-300 }

Azure AI Search is an information retrieval platform for the enterprise. It supports traditional search and conversational, AI-driven search for "chat with your data" experiences across proprietary content.

The easiest way to create a search service is through the Azure portal, which is covered in this article. You can also use:

+ [Azure PowerShell](https://learn.microsoft.com/en-us/azure/search/search-manage-powershell#create-or-delete-a-service)
+ [Azure CLI](https://learn.microsoft.com/en-us/azure/search/search-manage-azure-cli#create-or-delete-a-service)
+ [Management REST API](https://learn.microsoft.com/en-us/azure/search/search-manage-rest#create-or-update-a-service)
+ [Azure Resource Manager template](https://learn.microsoft.com/en-us/azure/search/search-get-started-arm)
+ [Bicep](https://learn.microsoft.com/en-us/azure/search/search-get-started-bicep)
+ [Terraform](https://learn.microsoft.com/en-us/azure/search/search-get-started-terraform)

## Before you start

### Choose a name, region, and tier

Some properties are fixed for the lifetime of the search service. Before creating your service, decide on the following properties:

| Property | Description |
|--|--|
| [Name](#name-your-service) | Becomes part of the URL endpoint. The name must be unique and follow naming rules. |
| [Region](https://learn.microsoft.com/en-us/azure/search/search-region-support) | Determines data residency and availability of certain features. For example, semantic ranker and Azure AI integration have region requirements. Choose a region that supports the features you need. |
| [Tier](https://learn.microsoft.com/en-us/azure/search/search-sku-tier) | Determines infrastructure, service limits, and billing. Some features aren't available on lower or specialized tiers. |

### Subscribe to Azure

Azure AI Search requires a free or pay-as-you-go Azure subscription.

To try Azure AI Search for free, [start a trial subscription](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and then [create your search service on the Free tier](#choose-a-tier). Each Azure subscription can have one free search service, which is intended for short-term, non-production evaluation of the product. You can complete all of our quickstarts and most of our tutorials on the Free tier. For more information, see [Try Azure AI Search for free](https://learn.microsoft.com/en-us/azure/search/search-try-for-free).

{: .important }
> To make room for other services, Microsoft might delete free services that are inactive for an extended period of time.

## Find the Azure AI Search offering

1. Sign in to the [Azure portal](https://portal.azure.com/).

1. In the upper-left corner of your dashboard, select **Create a resource**.

   ![Screenshot of the Create a Resource button in the Azure portal.](/portfolio/media/create-search-service/create-resource.png)

1. Use the search box to find **Azure AI Search**.

   ![Screenshot of the Azure AI Search tile in the Azure portal.](/portfolio/media/create-search-service/search-tile.png)

## Choose a subscription

If you have multiple Azure subscriptions, choose one for your search service.

If you're implementing [customer-managed encryption](https://learn.microsoft.com/en-us/azure/search/search-security-manage-encryption-keys) or using features that rely on managed service identities for [external data access](https://learn.microsoft.com/en-us/azure/search/search-indexer-securing-resources), choose the subscription you use for those services, such as Azure Key Vault.

## Set a resource group

A resource group is a container of related resources for an Azure solution. Use it to consolidate same-solution resources, monitor costs, and check the creation date of your search service.

![Screenshot of the Create a Resource Group dialog on the Create a Search Service page.](/portfolio/media/create-search-service/create-resource-group.png)

Over time, you can track current and projected costs for individual resources and for the overall resource group. The following screenshot shows the cost information that's available when you combine multiple resources into one group:

![Screenshot of the Cost Management page in the Azure portal.](/portfolio/media/create-search-service/manage-costs.png)

## Name your service

Enter a name for your search service. The name is part of the endpoint against which API calls are issued: `https://your-service-name.search.windows.net`. For example, if you enter `myservice`, the endpoint becomes `https://myservice.search.windows.net`.

When naming your service, follow these rules:

+ Use a name that's unique within the `search.windows.net` namespace.
+ Use between 2 and 60 characters.
+ Use only lowercase letters, digits, and dashes (-).
+ Don't use dashes as the first two characters or the last character.
+ Don't use consecutive dashes.

{: .tip }
> If you have multiple search services, it's helpful to include the region in the service name. For example, when deciding how to combine or attach resources, the name `myservice-westus` might save you a trip to the Properties page.

## Choose a region

{: .important }
> Due to high demand, Azure AI Search is currently unavailable for new instances in some regions.

If you use multiple Azure services, putting all of them in the same region minimizes or voids bandwidth charges. There are no charges for data egress among same-region services.

In most cases, choose a region near you, unless any of the following apply:

+ Your nearest region is [at capacity](https://learn.microsoft.com/en-us/azure/search/search-sku-tier#region-availability-by-tier). The Azure portal has the advantage of hiding unavailable regions and tiers during resource setup.

+ You want to use integrated data chunking and vectorization or built-in skills for AI enrichment. Integrated operations have region requirements.

+ You want to use Azure Storage for indexer-based indexing, or you want to store application data that isn't in an index. Debug session state, enrichment caches, and knowledge stores are Azure AI Search features that depend on Azure Storage. The region you choose for Azure Storage has implications for network security. If you're setting up a firewall, you should place the resources in separate regions. For more information, see [Outbound connections from Azure AI Search to Azure Storage](https://learn.microsoft.com/en-us/azure/search/search-indexer-securing-resources).

### Checklist for choosing a region

1. Is Azure AI Search available in a nearby region? Check the [list of supported regions](https://learn.microsoft.com/en-us/azure/search/search-region-support).

1. Do you have a specific tier in mind? Check [region availability by tier](https://learn.microsoft.com/en-us/azure/search/search-sku-tier#region-availability-by-tier).

1. Do you have business continuity and disaster recovery (BCDR) requirements? Create two or more search services in [regional pairs](/azure/reliability/cross-region-replication-azure#azure-paired-regions) within [availability zones](https://learn.microsoft.com/en-us/azure/search/search-reliability#availability-zones). For example, if you're operating in North America, you might choose East US and West US for each search service.

1. Do you need [AI enrichment](https://learn.microsoft.com/en-us/azure/search/cognitive-search-concept-intro), [integrated data chunking and vectorization](https://learn.microsoft.com/en-us/azure/search/vector-search-integrated-vectorization), or [multimodal image search](https://learn.microsoft.com/en-us/azure/search/search-get-started-portal-image-search)? Azure AI Search, Azure OpenAI, and Azure AI multiservice must coexist in the same region.

   + Start with [Azure OpenAI regions](/azure/ai-services/openai/concepts/models#model-summary-table-and-region-availability) because they have the most variability. Azure OpenAI provides embedding models and chat models for RAG and integrated vectorization.

   + Check [Azure AI Search regions](search-region-support.md#azure-public-regions) for a match to your Azure OpenAI region. If you're using OCR, entity recognition, or other skills backed by Azure AI, the `AI service integration` column indicates whether Azure AI multiservice and Azure AI Search are in the same region.

   + Check [multimodal embedding regions](/azure/ai-services/computer-vision/overview-image-analysis#region-availability) for multimodal APIs and image search. This API is accessed through an Azure AI multiservice account, but in general, it's available in fewer regions than Azure AI multiservice.

### Regions with the most overlap

The following regions offer cross-regional availability for Azure AI Search, Azure OpenAI, and Azure AI Vision multimodal:

+ Americas: West US, East US
+ Europe: Switzerland North, Sweden Central

This list isn't definitive, and depending on your tier, you might have more choices. Region status can also change quickly, so confirm your region choice before creating your search service.

## Choose a tier

Azure AI Search is offered in multiple [pricing tiers](https://azure.microsoft.com/pricing/details/search/):

+ Free
+ Basic
+ Standard
+ Storage Optimized

Each tier has its own [capacity and limits](https://learn.microsoft.com/en-us/azure/search/search-limits-quotas-capacity), and some features are tier dependent. For information about computing characteristics, feature availability, and region availability, see [Choose a service tier for Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-sku-tier).

The Basic and Standard tiers are the most common for production workloads, but many customers start with the Free tier. The billable tiers differ primarily in partition size, partition speed, and limits on the number of objects you can create.

![Screenshot of the Select Pricing Tier page in the Azure portal.](/portfolio/media/create-search-service/select-tier.png)

{: .note }
> Search services created after April 3, 2024 have larger partitions and higher vector quotas at every billable tier.

## Create your service

After providing the necessary inputs, create your search service.

![Screenshot of the Review and Create button on the Create a Search Service page.](/portfolio/media/create-search-service/create-service.png)

Your service is deployed within minutes, and you can monitor its progress with Azure notifications. Consider pinning the service to your dashboard for quick access in the future.

![Screenshot of the Notifications tab in the Azure portal.](/portfolio/media/create-search-service/notifications-tab.png)

## Configure authentication

When you create a search service, key-based authentication is the default, but it's not the most secure option. We recommend that you replace it with role-based access.

To enable role-based access for your service:

1. Go to your search service in the [Azure portal](https://portal.azure.com/).

1. From the left pane, select **Settings** > **Keys**. You can connect to your service using [API keys](https://learn.microsoft.com/en-us/azure/search/search-security-api-keys), [Azure roles](https://learn.microsoft.com/en-us/azure/search/search-security-rbac), or both. Select **Both** until you assign roles, after which you can select **Role-based access control**.

   ![Screenshot of the Keys tab with authentication options.](/portfolio/media/create-search-service/authentication-options.png)

## Scale your service

After deploying your search service, you can [scale it to your workload](https://learn.microsoft.com/en-us/azure/search/search-limits-quotas-capacity). Azure AI Search offers two scaling dimensions: *replicas* and *partitions*. Replicas allow your service to handle a higher load of search queries, while partitions allow your service to store and search through more documents.

Scaling is available only on billable tiers. On the Free tier, you can't scale your service or configure replicas and partitions.

Adding resources will increase your monthly bill. Use the [pricing calculator](https://azure.microsoft.com/pricing/calculator/) to understand the billing implications. You can adjust resources based on load, such as increasing resources for initial indexing and decreasing them later for incremental indexing.

To scale your service:

1. Go to your search service in the [Azure portal](https://portal.azure.com/).

1. From the left pane, select **Settings** > **Scale**.

   ![Screenshot of the Scale tab with sliders for adding replicas and partitions.](/portfolio/media/create-search-service/scale-options.png)

1. Use the sliders to add replicas and partitions.

## When to add a second service

Most customers use a single search service at a tier sufficient for the [expected load](https://learn.microsoft.com/en-us/azure/search/search-capacity-planning). One service can host multiple indexes, each isolated from the others, within the [maximum limits of your chosen tier](https://learn.microsoft.com/en-us/azure/search/search-limits-quotas-capacity#index-limits). In Azure AI Search, you can direct requests to only one index, reducing the chance of retrieving data from other indexes in the same service.

However, you might need a second service for the following operational requirements:

+ [BCDR](https://learn.microsoft.com/en-us/azure/reliability/regions-paired). If there's an outage, Azure AI Search won't provide instant failover.
+ [Multitenant architectures](https://learn.microsoft.com/en-us/azure/search/search-modeling-multitenant-saas-applications) that require two or more services.
+ Globally deployed applications that require services in each geography to minimize latency.

{: .note }
> In Azure AI Search, you can't separate indexing and querying operations, so don't create multiple services for separate workloads. An index is always queried on the service in which it was created, and you can't copy an index to another service.

A second service isn't required for high availability. You achieve high availability for queries by using two or more replicas in the same service. Because the replicas are updated sequentially, at least one is operational when a service update is rolled out. For more information about uptime, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

## Add more services to your subscription

Azure AI Search limits the [number of search services](https://learn.microsoft.com/en-us/azure/search/search-limits-quotas-capacity#subscription-limits) you can initially create in a subscription. If you reach your limit, you can request more quotas.

You must have Owner or Contributor permissions for the subscription to request quotas. Depending on your region and data center capacity, you might be able to request quotas automatically. If the request fails, reduce the number or submit a support ticket. Expect a one-month turnaround for a large quota increase, such as more than 30 services.

To request more subscription quotas:

1. Go to your dashboard in the [Azure portal](https://portal.azure.com/).

1. Use the search box to find the **Quotas** service.

   ![Screenshot of the Quota search term and the Quotas service in the results.](/portfolio/media/create-search-service/quota-search.png)

1. On the **Overview** tab, select the **Search** tile.

   ![Screenshot of the Search tile on the Overview page.](/portfolio/media/create-search-service/search-tile-overview.png)

1. Set filters to review the existing quota for search services in your current subscription. We recommend filtering by usage.

   ![Screenshot of the Usage filter for search services in your current subscription.](/portfolio/media/create-search-service/usage-filter.png)

1. Next to the tier and region that need more quotas, select **Request adjustment** <img src="/portfolio/media/create-search-service/request-adjustment.png" alt="Screenshot of the Request Adjustment icon, which is the outline of a pencil." width="14">.

1. In **New Quota Request**, enter a new limit for your subscription quota. The new limit must be greater than your current limit. If regional capacity is constrained, your request won't be automatically approved, and an incident report will be generated for investigation and resolution.

1. Submit your request.

1. Check notifications in the Azure portal for updates on the new limit. Most requests are approved within 24 hours.

## Related content

+ [Quickstart: Create an Azure AI Search index in the Azure portal](https://learn.microsoft.com/en-us/azure/search/search-get-started-portal)
+ [Quickstart: Start using Cost analysis](https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn)

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
