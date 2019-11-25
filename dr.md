---

copyright:
  years: 2019
lastupdated: "2019-06-19"

keywords: annotator clinical data, disaster recovery, disaster, recovery

subcollection: wh-acd

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# High availability and disaster recovery
(: ha-dr}
The {{site.data.keyword.wh-acd_full}} service is highly available within any IBM Cloud region.  Recovering from potential disasters that affect an entire region requires planning and preparation.

The instance owner is responsible for understanding the configuration, customization, and usage of the service. Instance owners are responsible for provisioning a service instance in a new IBM Cloud location when necessary and restoring their data to the same location.

## High_availability
{: high availability}
{{site.data.keyword.wh-acd_short}} is hosted in the Dallas and Washington locations.  Traffic to any instance is load-balanced across multiple data centers.

## Disaster recovery
{: disaster_recovery}
Disaster recovery can become a necessity if an IBM Cloud region experiences a significant failure that includes the potential loss of data. 

Disaster recovery can be accomplished by either provisioning an instance of the service in multiple regions or provisioning an instance in a new regions if an existing region becomes unavailable.  The URL and and apikey for the new region need to be provided to the solution accessing the service to complete the recovery from one region to another.

Instance owners are responsible for maintaining up-to-date cartridge files outside of IBM Cloud or keeping instances in multiple IBM Cloud regions in sync. The same cartridge file can be deployed to different {{site.data.keyword.wh-acd_short}} instance in different regions for the synchronization purpose. 

### Detecting a location outage
{: outage_detection}
The {{site.data.keyword.wh-acd_full}} service provides a health check API that can be called repeatedly to ensure the service is available.  Successive internal service error responses from the API could be used as indicator that the service is no longer available in a specific location.


#### Recovery
{: recovery}
The instance owner must ensure the custom corpora is available in the new location prior to recovering a custom {{site.data.keyword.wh-acd_short}} instance.

To recover a custom instance:
  1.  Provision a new instance of the {{site.data.keyword.wh-acd_full}} service in a different region.
  2.  Deploy your existing cartridge files to the new service instance.
  3.  Modify your applications to use the URL and credentials of the new service instance.

