---
layout: default
title: Investigate an incident
parent: Splunk
nav_order: 3
---

# Investigate an incident

June 28, 2023 ∙ [Original document](https://docs.splunk.com/Documentation/MC/Current/Detect/Investigate)
{: .fs-5 : .fw-300 }

After you triage an incident on the **Incident review** page of Splunk Mission Control, select either the incident or **Preview** then **View details** to start investigating it. You can view incident fields in the side panel, and you can view summary fields and custom fields in the **Overview** tab.

{:  .note }
> To investigate a specific incident, search for it on the **Incident review** page using the incident ID with the `MC-XXXXX` syntax.

## Create a summary field for an incident

Use summary fields to document metadata that isn't automatically provided for an incident. Unlike custom fields, summary fields apply only to the incidents for which you create them. See [Create a custom field](http://docs.splunk.com/Documentation/MC/Current/Detect/IncidentSettings#Create_a_custom_field) for more information about custom fields.

When you create a summary field, you must specify its name and one or more values. For example, if you want to document the IP address associated with a particular incident, you can create a summary field named `IP` with a value of `20.20.20.20`. You can view and edit summary field values for an incident in the **Overview** tab.

To create a summary field for an incident:

1. Select an incident from the **Incident review** page of Splunk Mission Control.
2. In the **Summary** section of the **Overview** tab, select **+**.
3. Enter a name and value for the summary field.
    1. (Optional) To add a value to your summary field, select **+** next to the field.
    2. (Optional) To delete a value from your summary field, select **×** next to the value.
    3. (Optional) To delete your summary field entirely, select **×** next to the field. Your field must have only one value for you to delete it.
4. (Optional) To create an additional field, select **+ Summary field**, then follow the instructions in the previous step.
5. Select **Submit**.

## Edit field values for an incident

When investigating an incident, you can edit and automatically save changes to the following incident field values in the **Info** section of the side panel:

*   Owner
*   Status
*   Urgency
*   Sensitivity
*   Incident type
*   Disposition

In the **Overview** tab, you can edit summary and custom field values by selecting the edit icon ( ![edit icon](https://docs.splunk.com/images/5/52/PencilEdit.png) ). After you edit the field values, select **Save**.

## View incident information

To view details and dates associated with an incident, see the **Info** section of the side panel. The details reveal field-value pairs that are valuable to your [investigation](https://docs.splunk.com/Splexicon:Investigation). For example, you can find the source and destination of a malware infection in an endpoint incident.

Follow the steps in this table to view other types of incident information:

| Information | Description |
| --- | --- |
| Recent activity for a notable event | If the incident was ingested from Splunk Enterprise Security (ES), select **View all recent activity for this notable event** to view incident activity over a specified time period. |
| Contributing events | Select **View contributing events** to open a contributing search, which identifies the events that generated the incident. To learn more about events, see [Add events to an incident in Splunk Mission Control](http://docs.splunk.com/Documentation/MC/Current/Detect/Events). |
| SOAR container | Each incident in Splunk Mission Control is associated with a container in Splunk SOAR. Select **View container** to open Splunk SOAR and see the container associated with the incident. |
| ES notable | Some incidents in Splunk Mission Control are associated with a notable event in ES. If applicable, select **View notable event** to open ES and see the notable event from which the incident originated. |

## View risk-based alerting scores for artifacts

You can view the risk-based alerting (RBA) scores for specific [artifacts](https://docs.splunk.com/Splexicon:Artifact) in the **Overview** tab. This information can help you determine the likelihood that an artifact is a potential threat. The RBA score and color are ingested from Splunk Enterprise Security and are represented by the following badge colors and number ranges:

*   Yellow: 0 to 25
*   Orange: 26 to 50
*   Light red: 51 to 75
*   Dark red: 76 and higher

To learn more about RBA, see [How risk scores work in Splunk Enterprise Security](http://docs.splunk.com/Documentation/ES/7.2.0/RBA/Analyzerisk) in the _Use Splunk Enterprise Security Risk-based Alerting_ manual.

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
