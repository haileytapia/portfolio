---
layout: default
title: Investigate an incident in Splunk Mission Control
parent: Splunk Mission Control
grand_parent: Software
nav_order: 1
---

# Investigate an incident in Splunk Mission Control

July 28, 2023 ∙ [Splunk Documentation](https://docs.splunk.com/Documentation/MC/Current/Detect/Investigate)
{: .fs-5 : .fw-300 }

{:  .about }
> Threat Intelligence Management in Splunk Mission Control correlates your internal event data with intelligence sources to help you detect, contextualize, and respond to security threats.

After you triage an incident on the **Incident** review page of Splunk Mission Control, select either the incident or **Preview** then **View details** to start investigating it. The summary fields and custom fields are listed in the **Overview** tab, while the incident fields are listed in the side panel.

{:  .note }
> To investigate a specific incident, search for it on the **Incident review** page using the incident ID with the `MC-XXXXX` syntax.

## Edit field values for an incident
When investigating an incident in Splunk Mission Control, you can edit and automatically save changes to the following incident fields in the **Info** section of the side panel:

*   Owner
*   Status
*   Urgency
*   Sensitivity
*   Incident type
*   Disposition

In the **Overview** tab, you can edit the summary field values, including any values for custom fields you created, by selecting the edit icon ( ![edit icon](https://docs.splunk.com/images/5/52/PencilEdit.png) ). After you edit the field values, select **Save**.

## View incident information

To view details and dates associated with an incident, see the **Info** section of the side panel. The details reveal field-value pairs that are valuable to your [investigation](https://docs.splunk.com/Splexicon:Investigation). For example, you can find the source and destination of a malware infection in an endpoint incident, as well as the incident's reference ID, which is its globally unique identifier.

Follow the steps in this table to view other types of incident information:

| Information | Description |
| --- | --- |
| Recent activity for a notable event | If an incident was ingested from Splunk Enterprise Security (ES), you can select **View all recent activity for this Notable Event**. You are taken to the search page where you can see the activity of the incident for the time period you select. |
| Contributing events | You can further investigate an incident by opening a contributing search. A contributing search identifies which events contributed to the generation of the incident. Select **View contributing events** to open the search. To learn more about events, see [Add events to an incident in Splunk Mission Control](http://docs.splunk.com/Documentation/MC/Current/Detect/Events). |
| SOAR container | Each incident in Splunk Mission Control is associated with a container in Splunk SOAR. Select **View container** to open Splunk SOAR and see the container associated with the incident. |
| ES notable | Some incidents in Splunk Mission Control are associated with a notable event in ES. If applicable, select **View notable event** to open ES and see the notable event from which the incident originated. |

## View risk-based alerting scores for artifacts

You can view the risk-based alerting (RBA) scores for certain [artifacts](https://docs.splunk.com/Splexicon:Artifact) in the **Overview** tab. This information can help you understand the likelihood of the artifact being a potential threat. The RBA score and color are ingested from Splunk Enterprise Security and are represented by the following badge colors and number ranges:

*   Yellow: 0-25
*   Orange: 26-50
*   Light red: 51-75
*   Dark red: 76 and higher

To learn more about risk-based alerting, see [How risk scores work in Splunk Enterprise Security](http://docs.splunk.com/Documentation/ES/7.2.0/RBA/Analyzerisk) in the _Use Splunk Enterprise Security Risk-based Alerting_ manual.

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
