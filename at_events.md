---

copyright:
  years: 2016, 2019
lastupdated: "2019-04-23"

keywords: annotator clinical data, clinical data, annotation

subcollection: wh-acd
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:table: .aria-labeledby="caption"}

<!-- Name your file `at-events.md` and include it in the Reference nav group in your toc file. -->

# {{site.data.keyword.cloudaccesstrailshort}} events
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the _YourServiceName_ service in {{site.data.keyword.Bluemix}}.
{: shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in {{site.data.keyword.Bluemix_notm}}. For more information, see the [{{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla).

<!-- You can create different sections to group events by area. -->

## List of events
{: #events}

<!-- Make sure you introduce the table with a detailed description that immediately precedes it. For example, see https://cloud.ibm.com/docs/services/cloud-activity-tracker/services?topic=cloud-activity-tracker-cf. -->
Whan profiles or flows are modified, cartridges are created, or tennant data is deleted, an event is generated. The following table is a list of actions that generate events.

| Action | Description |
|:-----------------|:-----------------|
| wh-acd.profile.create | Create a profile. |
| wh-acd.profile.update | Update a profile. |
| wh-acd.profile.delete | Delete a profile. |
| wh-acd.flow.create | Create a flow. |
| wh-acd.flow.update | Update a flow. |
| wh-acd.flow.delete | Delete a flow. |
| wh-acd.cartridge.deploy | Deploy a cartridge. |
| wh-acd.alluserdata.delete | Delete a tenant's data. |
{: caption="Table 1. Actions that generate events" caption-side="top"}

## Where to view the events
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.Bluemix_notm}} region where the events are generated.
