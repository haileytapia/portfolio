---
layout: portfolio
title: Azure AI Search agent skill
parent: Documentation strategy and initiatives
grand_parent: Microsoft
nav_order: 4
permalink: /microsoft/strategy-and-initiatives/search-agent-skill
---

# Azure AI Search agent skill
{: .no_toc }

My team used an internal AI toolset called DocAssist (fictitious name), a collection of specialized agents and skills that supported all stages of content development: planning, research, authoring, review, and evaluation. PMs also increasingly used DocAssist to generate PRs.

DocAssist was broadly useful, but it lacked the Azure AI Search-specific decisions I had to make when developing and maintaining our documentation. I identified the recurring gaps in its output and encoded those decisions in an agent skill.

## Where DocAssist fell short

Whether I used DocAssist myself or reviewed DocAssist-generated PRs from PMs, I repeatedly found myself making the same product-specific corrections before the content was ready to publish. DocAssist's shortcomings included:

### Code and SDK conventions

+ DocAssist wasn't configured with the Azure AI Search SDK packages, so I had to explicitly prompt it to validate code snippets against the appropriate SDK.

+ DocAssist could add unnecessary scaffolding to focused code snippets or make them inconsistent with adjacent snippets, such as using different placeholder names and different levels of detail.

### Documentation strategy and structure

+ DocAssist had difficulty determining how a change should be documented: as a new article, an extension to an existing article, or a "What's New" announcement. It often favored extending existing articles, even when new functionality introduced a distinct customer scenario or enough conceptual and procedural novelty to warrant a separate article.

+ DocAssist could overload focused articles with peripheral references and new subsections, creating laundry lists of related content instead of preserving a clear happy path through the core task.

+ Many Azure AI Search articles used side-by-side tabs to demonstrate preview and GA behavior. DocAssist didn't consistently account for this structure and could add content in ways that disrupted the conventions established within those tabs.

+ DocAssist often used alert boxes where ordinary prose would've been more appropriate, adding unnecessary visual emphasis to otherwise straightforward information.

+ DocAssist didn't apply [preview disclosure model](preview-disclosure-model.md) I developed separately, which called for `(preview)` labels and the reusable article-level preview notice.

### Product, repository, and editorial conventions

+ Our documentation defaulted to the latest Azure AI Search API version. Older versions were preserved when historical accuracy required them. DocAssist often added new API-version content alongside existing guidance without integrating it into the surrounding content.

+ Even though our global DocFX configuration already designated me as the default author for Azure AI Search documentation, DocAssist always manually assigned me as the author of every article.

+ DocAssist favored its built-in conventions over the standards defined in our in-house contributor and style guides. For example, one of its skills evaluated whether content was written appropriately for developers. I found that its output often referred to "the developer" rather than addressing the audience directly as "you," which conflicted with our established style.

## New Azure AI Search agent skill

For the Microsoft Global Hackathon 2026, I created an agent skill with more than 20 Azure AI Search-specific documentation rules and decision points. The skill was designed to work alongside, rather than replace, DocAssist.

I researched effective skill design, including attending a workshop on skill development. I then translated the corrections I repeatedly made into explicit guidance that DocAssist could apply during content development. Whenever a prompt to any DocAssist agent mentioned Azure AI Search, the skill was automatically triggered and applied the relevant guidance.

## Guiding principle: Start with the customer

I designed the skill around a simple principle: start with what the customer is trying to accomplish.

Instead of letting a one-pager or spec dictate the content structure, the skill used the customer's goal to guide subsequent decisions. This helped DocAssist distinguish between changes that needed new guidance, changes that belonged in existing content, and changes that only needed a concise update.

The same principle shaped decisions about structure and reuse. The goal wasn't simply to generate technically correct content, but to organize that content around the customer's path through our documentation.

## Impact

The skill turned Azure AI Search-specific documentation expertise from individual writer judgment into an explicit, reusable layer of AI-assisted authoring. Instead of relying on a writer to catch the same product-specific issues after generation, DocAssist could apply those requirements during content development.

This work also changed my role in AI-assisted documentation. I started as a user of the existing tooling and became an active contributor to how it behaved, testing the skill against real authoring scenarios, identifying where its outputs still fell short, and refining the rules and decision points.

---

[Back to top](#top)

Thanks for visiting my portfolio! If you have any questions or feedback, please feel free to reach out.
