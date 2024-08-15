---
layout: default
title: Wei creates an intelligence workflow to enrich data
parent: Mission Control
grand_parent: Splunk
nav_order: 1
permalink: /splunk/mission-control/enrich-data
---

# Scenario: Wei creates an intelligence workflow in Splunk Mission Control to enrich data

July 13, 2023 ∙ [Original document](https://docs.splunk.com/Documentation/MC/Current/Detect/TIMEnrichData)
{: .fs-5 : .fw-300 }

{:  .about }
> Threat Intelligence Management in Splunk Mission Control correlates your internal event data with intelligence sources to help you detect, contextualize, and respond to threats.

The following scenario features Buttercup Games, a fictitious game company.

Buttercup Games recently released the latest version of its artificial intelligence gaming software. Wei, a security operations center (SOC) administrator at Buttercup Games, uses Threat Intelligence Management in Splunk Mission Control to detect and enrich security threats.

Since the release, several employees have received malicious emails. To contextualize each email with additional information, such as whether the email contains malware, Wei decides to use an intelligence workflow in Splunk Mission Control. Only company administrators can create and manage intelligence workflows, and because Wei is a SOC administrator at Buttercup Games, they can configure the workflow.

In this scenario, Wei uses Threat Intelligence Management in Splunk Mission Control to create an intelligence workflow that enriches data from malicious emails.

## Wei creates an intelligence workflow

From the **Workflows** page of their Splunk Cloud Console, Wei follows these four steps to configure a new workflow.

### Wei provides details for the workflow

Wei names the workflow **Medium and High Email Addresses** and, to filter their internal event data by priority, selects **Indicator prioritization** for the workflow type.

Indicators are pieces of data that provide additional information about unusual, suspicious, or malicious cyber activity. In Wei's case, indicators include threat actors and malware associated with a malicious email.

![Wei names the workflow Medium and High Email Addresses and selects Indicator prioritization for the workflow type.](https://github.com/haileytapia/portfolio/assets/78626762/77b5cd7b-0536-4931-a06c-77a381df54b9)

### Wei selects intelligence sources for indicator prioritization

In Splunk Mission Control, intelligence sources are feeds that enrich your internal event data with threat intelligence. Intelligence sources can be internal or external.

Wei uses Threat Intelligence Management to normalize, score, and prioritize data from their desired intelligence sources by following these steps:

1. Wei sends Buttercup Games' internal event data to Threat Intelligence Management.
2. To normalize the data, Wei selects two external sources: **Digital Shadows** and **VirusTotal**.
3. The weight of an intelligence source represents the source's influence in the final indicator scoring. Because Wei wants to prioritize VirusTotal over Digital Shadows in the scoring, they set the weight of Digital Shadows to **1** and the weight of VirusTotal to **3**. This means 25% of the score comes from Digital Shadows and 75% from VirusTotal.

![Wei selects Digital Shadows and VirusTotal as intelligence sources to normalize and prioritize the internal event data. They also give VirusTotal more weight in indicator prioritization.](https://github.com/haileytapia/portfolio/assets/78626762/8abfbde2-6669-4eac-ab7f-82d504cd0859)

### Wei filters the prioritized indicators

To identify only malicious emails, Wei filters the prioritized indicators from Digital Shadows and VirusTotal for **EMAIL_ADDRESS** indicators with **Medium** and **High** scores.

![Wei filters the prioritized indicators from the intelligence sources for only email addresses with Medium and High threat scores.](https://github.com/haileytapia/portfolio/assets/78626762/31447deb-c208-4734-bcb6-dca8e406a37e)

### Wei sends the filtered indicators to Splunk Mission Control

Now that Wei has created a list of prioritized indicators for email addresses, they select **Splunk Mission Control** as the destination for the resulting dataset and save the workflow.

![Wei sends the prioritized indicators to Splunk Mission Control and creates the workflow.](https://github.com/haileytapia/portfolio/assets/78626762/078b0e1f-d021-48c4-ba6a-ee3fd5083ffe)

The workflow now appears in Wei's list of intelligence workflows, and the workflow stages are visualized in a diagram.

![Wei's new intelligence workflow for malicious email addresses appears in their list of workflows.](https://github.com/haileytapia/portfolio/assets/78626762/fa55fda1-3e9b-45c7-a407-c8aa7c8e3583)

Every few minutes, Threat Intelligence Management runs a data processing pipeline that applies the preferences specified in the workflow to Wei's entire intelligence library and sends the resulting records to Splunk Mission Control.

## Wei activates the intelligence workflow for data processing

After navigating to the **Intelligence Management** page in Splunk Mission Control, Wei activates the intelligence workflow they created and begins to investigate incidents involving malicious email addresses.

![Wei activates the workflow they created to periodically process intelligence from Digital Shadows and VirusTotal, filter internal event data for malicious email addresses, and return the results to Splunk Mission Control.](https://github.com/haileytapia/portfolio/assets/78626762/15ff25b0-4fbf-43b3-be13-e1f97c4b4f13)

## Summary

In this scenario, Wei used Splunk Mission Control to enrich data from malicious emails by creating a workflow that periodically normalizes data against intelligence sources, passes the data through filters specified in the workflow, and transforms the results into a destination enclave.

## Learn more

To learn more about Threat Intelligence Management in Splunk Mission Control, see:

* [Assess threats using intelligence data in Splunk Mission Control](http://docs.splunk.com/Documentation/MC/Current/Detect/Intelligence)
* [Configure intelligence workflows for Splunk Mission Control to automate processing indicators](http://docs.splunk.com/Documentation/MC/Current/Detect/IntelligenceWorkflows)
* [Enrich incidents in Splunk Mission Control with threat intelligence sources](http://docs.splunk.com/Documentation/MC/Current/Detect/IntelligenceSources)

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
