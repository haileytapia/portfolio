---
layout: default
title: Additions to the Splunk Style Guide
parent: Software
---

# Additions to the Splunk Style Guide
{: .no_toc }

May 17, 2023 ∙ [Splunk Style Guide](https://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Howtouse)
{: .fs-5 : .fw-300 }

{:  .about }
> As a Technical Writer Intern at Splunk, I created and revised various pieces of content for the _Splunk Style Guide_, the writing style reference for Splunk documentation and products.

This page lists the sections of the _Splunk Style Guide_ to which I contributed:

- TOC
{:toc}

## Numbers

This section contains guidelines for using numbers in Splunk documentation.

### [When to use numerals]()

### [When to use words]()

## UI text guidelines

This section contains guidelines for writing user interface (UI) text at Splunk.

See below for the content I developed and reformatted on terminal punctuation in UI text.

### [Terminal punctuation](https://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/UIGuidelines#Terminal_punctuation)

Follow these best practices for terminal punctuation:

*   Use a period at the end of complete sentences.
*   When writing single, short, descriptive phrases that are not complete sentences, don't use a period at the end.
*   If a UI element requires more than one phrase of description, write them as sentences and use a period or other appropriate punctuation to distinguish them from one another and to enhance readability.
*   If a word or phrase is meant to be read as a question, use a question mark.
*   Don't use exclamation marks.
*   If a single view, page, or dialog box contains descriptive text that uses both full sentences and fragments, try rewriting the full sentences into fragments. If it isn't possible to rewrite the full sentences into fragments, use terminal punctuation for all of the text for consistency.

For more punctuation guidelines, see [Punctuation and symbols](http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Showingsymbolsintext).

See the following examples of correct and incorrect punctuation:

| Correct | Incorrect |
| --- | --- |
| The search head removes the alias field from the event. | The search head removes the alias field from the event |
| Search results | Search results. |
| The search processed 100,000 events. This process took less than a minute. | The search processed 100,000 events, this process took less than a minute. |
| What is the average query response time? | What is the average query response time |
| The update includes enhanced security features. | The update includes enhanced security features! |

## Usage dictionary

This section outlines terms to use and avoid in Splunk documentation.

See below for my three entries in the dictionary.

### [after](https://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Usagedictionary#A)

     Use to denote a chronological sequence of events that doesn't rely on cause and effect. Don't use to mean "when". See also [when](http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Usagedictionary#W).

     **Correct**

     After you install the update, save your changes.

     **Incorrect**

     After a user logs in to your organization, a SessionLog event is created.

### [if](https://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Usagedictionary#I)

     Use to indicate a hypothetical situation, a possibility, or a condition that must be met for a particular action, behavior, or event to occur. See also [when](http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Usagedictionary#W).

 **Correct**

     If the search returns too many results, try refining your search.

 **Incorrect**

     When the search returns too many results, try refining your search.

### [when](http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Usagedictionary#W)

     Use to indicate an action, behavior, or event that is expected or certain to occur. This term implies a cause-and-effect relationship. See also [after](http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Usagedictionary#A) and [if](http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Usagedictionary#I).

 **Correct**

     When a signal crosses the static threshold, an alert is triggered.

 **Incorrect**

     After a signal crosses the static threshold, an alert is triggered.

     If a signal crosses the static threshold, an alert is triggered.
