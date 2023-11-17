---
layout: default
title: Scenario: Wei creates an intelligence workflow to reduce false positives
parent: Splunk
nav_order: 2
---

# Scenario: Wei creates an intelligence workflow to reduce false positives

July 13, 2023 ∙ [Original document](https://docs.splunk.com/Documentation/MC/Current/Detect/TIMFalsePositives)
{: .fs-5 : .fw-300 }

{:  .about }
> Threat Intelligence Management in Splunk Mission Control correlates your internal event data with intelligence sources to help you detect, contextualize, and respond to security threats.

The following scenario features Buttercup Games, a fictitious game company.

Buttercup Games recently released the latest version of its artificial intelligence gaming software. Wei, a security operations center (SOC) administrator at Buttercup Games, uses Threat Intelligence Management in Splunk Mission Control to detect and enrich security threats.

While monitoring the Buttercup Games software, Wei faces a high volume of false positives for IP addresses. False positives are security alerts that incorrectly indicate the presence of threats. To make more accurate detections, Wei decides to use an intelligence workflow in Splunk Mission Control to prioritize IP addresses by threat. Only company administrators can create and manage intelligence workflows, and because Wei is a SOC administrator at Buttercup Games, they can configure the workflow.

In this scenario, Wei uses Threat Intelligence Management in Splunk Mission Control to create an intelligence workflow that rules out false positives for IP addresses.

## Wei creates an intelligence workflow

From the **Workflows** page of their Splunk Cloud Console, Wei follows these four steps to configure a new workflow.

### Wei provides details for the workflow

Wei names the workflow **Medium and High IP Addresses** and, to filter their internal event data by priority, selects **Indicator prioritization** for the workflow type.

Indicators are pieces of data that provide additional information about unusual, suspicious, or malicious cyber activity. In Wei's case, indicators include threat actors and malware associated with a malicious IP address.

![Wei names the workflow Medium and High IP Addresses and selects Indicator prioritization for the workflow type.](https://github.com/haileytapia/portfolio/assets/78626762/287be924-7569-497a-af7e-f8793ae2056a)

### Wei selects intelligence sources for indicator prioritization

In Splunk Mission Control, intelligence sources are feeds that enrich your internal event data with threat intelligence. Intelligence sources can be internal or external.

Wei uses Threat Intelligence Management to normalize, score, and prioritize data from their desired intelligence sources by following these steps:

1. Wei sends Buttercup Games' internal event data to Threat Intelligence Management.
2. To normalize the data, Wei selects two external sources: **Digital Shadows** and **VirusTotal**.
3. The weight of an intelligence source represents the source's influence in the final indicator scoring. Because Wei wants to prioritize VirusTotal over Digital Shadows in the scoring, they set the weight of Digital Shadows to **1** and the weight of VirusTotal to **3**. This means 25% of the score comes from Digital Shadows and 75% from VirusTotal.

![Wei selects Digital Shadows and VirusTotal as intelligence sources to normalize and prioritize the internal event data. They also give VirusTotal more weight in indicator prioritization.](https://github.com/haileytapia/portfolio/assets/78626762/d6d5eeb3-4456-4c76-a5e1-4b1d7577a01f)

### Wei filters the prioritized indicators

To identify only malicious IP addresses, Wei filters the prioritized indicators from Digital Shadows and VirusTotal for **IP4** and **IP6** indicators with **Medium** and **High** scores.

![Wei filters the prioritized indicators from the intelligence sources for only IP addresses with Medium and High threat scores.](https://github.com/haileytapia/portfolio/assets/78626762/8d02e567-dfdc-4285-b154-c8fd44e9b3f4)

### Wei sends the filtered indicators to Splunk Mission Control

Now that Wei has created a list of prioritized indicators for IP addresses, they select **Splunk Mission Control** as the destination for the resulting dataset and save the workflow.

![Wei sends the prioritized indicators to Splunk Mission Control and creates the workflow.](https://github.com/haileytapia/portfolio/assets/78626762/c16cd66f-9279-4cfe-a8d6-11829a88163d)

The workflow now appears in Wei's list of intelligence workflows, and the workflow stages are visualized in a diagram.

![Wei's new intelligence workflow for malicious IP addresses appears in their list of workflows.](https://github.com/haileytapia/portfolio/assets/78626762/17a91593-d095-4e18-be62-714f57ff4da1)

Every few minutes, Threat Intelligence Management runs a data processing pipeline that applies the preferences specified in the workflow to Wei's entire intelligence library and sends the resulting records to Splunk Mission Control.

## Wei activates the intelligence workflow for data processing

After navigating to the **Intelligence Management** page in Splunk Mission Control, Wei activates the intelligence workflow they created and begins to investigate incidents involving malicious IP addresses.

![Wei activates the workflow they created to periodically process intelligence from Digital Shadows and VirusTotal, filter internal event data for malicious IP addresses, and return the results to Splunk Mission Control.](https://github.com/haileytapia/portfolio/assets/78626762/aafe5e85-7c95-488d-bc48-afb9e84c4a6d)

## Summary

In this scenario, Wei used Splunk Mission Control to reduce false positives for IP addresses by creating a workflow that periodically normalizes data against intelligence sources, passes the data through filters specified in the workflow, and transforms the results into a destination enclave.

## Learn more

To learn more about Threat Intelligence Management in Splunk Mission Control, see:

* [Assess threats using intelligence data in Splunk Mission Control](http://docs.splunk.com/Documentation/MC/Current/Detect/Intelligence)
* [Configure intelligence workflows for Splunk Mission Control to automate processing indicators](http://docs.splunk.com/Documentation/MC/Current/Detect/IntelligenceWorkflows)
* [Enrich incidents in Splunk Mission Control with threat intelligence sources](http://docs.splunk.com/Documentation/MC/Current/Detect/IntelligenceSources)

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
