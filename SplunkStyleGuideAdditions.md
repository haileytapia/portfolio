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

This document contains the sections of the _Splunk Style Guide_ to which I contributed:

- TOC
{:toc}

## Numbers

This section contains guidelines for using numbers in text. During my internship, Splunk decided to phase out the tech industry practice of spelling out numbers under 10 and instead use numerals for most numbers, with a few exceptions. I informed the company's decision with research and, in collaboration with three technical editors, wrote the following content for the company's new guidance on numbers in documentation:

### [Using numerals](https://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Numbersornumerals#Using_numerals)

In general, use numerals for numbers in text, even for numbers less than 10. This includes numbers associated with counts, dates, decimals, fractions, measurements, percentages, ranges, time, versions, weight, and other data for comparison or analysis.

Review the following table for examples of when to use numerals in text:

<table>
    <tbody>
        <tr>
            <td style="background-color:rgb(204, 204, 255) !important;border-bottom:1px solid rgb(204, 204, 255);border-top:1px solid rgb(204, 204, 255);padding:8px;vertical-align:top;">
                <strong>Use numerals for</strong>
            </td>
            <td style="background-color:rgb(204, 204, 255) !important;border-bottom:1px solid rgb(204, 204, 255);border-top:1px solid rgb(204, 204, 255);padding:8px;vertical-align:top;">
                <strong>Example</strong>
            </td>
            <td style="background-color:rgb(204, 204, 255) !important;border-bottom:1px solid rgb(204, 204, 255);border-top:1px solid rgb(204, 204, 255);padding:8px;vertical-align:top;">
                <strong>For more information</strong>
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Counts
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                2 forwarders, 3 unique values
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                &nbsp;
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Dates
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                April 22, 2019
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                See <a href="http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Dates">Dates</a>.
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Decimals
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                3.14
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                See <a href="http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Decimals">Commas and decimals</a>.
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Dimensions
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                1280 x 1024
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                &nbsp;
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Distance
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                4 feet
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                &nbsp;
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Duration of time
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                2 minutes
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                See <a href="http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Time">Time</a>.
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Fractions
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                1/4
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                See <a href="http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Fractions">Fractions</a>.
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Measurements
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                8 CPU, 1,045 MB
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                See <a href="http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Measurements">Measurements</a>.
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Numerical user input
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                In the <strong>Number</strong> field, enter <strong>5</strong>.
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                &nbsp;
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Percentages
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                25%
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                &nbsp;
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Phone numbers
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                +1-888-555-1212
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                See <a href="http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Phonenumbers">Phone numbers</a>.
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Pixels
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                450 px, 1920 x 1080 pixels
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                &nbsp;
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Ranges
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                50 to 60 GB
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                See <a href="http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Ranges">Ranges</a>.
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Time of day
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                2:30 PM to 5 PM
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                See <a href="http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Time">Time</a>.
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Versions
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Splunk Enterprise 7.x
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                See <a href="http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Versions">Versions</a>.
            </td>
        </tr>
        <tr>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                Weight
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                40 lbs
            </td>
            <td style="border-bottom:1px solid rgb(221, 221, 221);border-top:1px solid rgb(221, 221, 221);padding:8px;vertical-align:top;">
                &nbsp;
            </td>
        </tr>
    </tbody>
</table>


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

> Use to denote a chronological sequence of events that doesn't rely on cause and effect. Don't use to mean "when". See also [when](#when).
> 
> **Correct**
> 
> After you install the update, save your changes.
> 
> **Incorrect**
> 
> After a user logs in to your organization, a SessionLog event is created.

### [if](https://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Usagedictionary#I)

> Use to indicate a hypothetical situation, a possibility, or a condition that must be met for a particular action, behavior, or event to occur. See also [when](#when).
> 
> **Correct**
> 
> If the search returns too many results, try refining your search.
> 
> **Incorrect**
> 
> When the search returns too many results, try refining your search.

### [when](http://docs.splunk.com/Documentation/StyleGuide/current/StyleGuide/Usagedictionary#W)

> Use to indicate an action, behavior, or event that is expected or certain to occur. This term implies a cause-and-effect relationship. See also [after](#after) and [if](#if).
> 
> **Correct**
> 
> When a signal crosses the static threshold, an alert is triggered.
> 
> **Incorrect**
> 
> After a signal crosses the static threshold, an alert is triggered.
> 
> If a signal crosses the static threshold, an alert is triggered.

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
