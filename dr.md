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
The {{site.data.keyword.wh-acd_full}} service is highly available within an IBM Cloud region. Disruption in the network connectivity may happen when a clould region is down. Recovering from potential disasters that affect an entire region requires planning and preparation. Thus, instance owners need to have recovery plans based on their use cases. 

The instance owners are responsible for understanding the configuration, customization, and usage of the service. See [What are the responsibilities of the instance owner and the service provider?](/docs/overview?topic=overview-shared-responsibilities){: external} for more information.

Instance owners are responsible for provisioning a service instance in a new IBM Cloud location when necessary and restoring their data to the same location.  See [How do I ensure zero downtime?](/docs/overview?topic=overview-zero-downtime#zero-downtime){: external} for more information.


## High_availability
{: high availability}
{{site.data.keyword.wh-acd_short}} is hosted in the Dallas and Washington locations.  Traffic to any instance is load-balanced across multiple data centers.


## Disaster recovery
{: disaster_recovery}
Disaster recovery can become a necessity if an IBM Cloud region experiences a significant failure that includes the potential loss of data. 

Disaster recovery can be accomplished by either provisioning an instance of the service in multiple regions or provisioning an instance in a new region if an existing region becomes unavailable.  The URL and and apikey for the new region need to be provided to the solution accessing the service to complete the recovery from one region to another.

Instance owners are responsible for maintaining up-to-date cartridge files outside of IBM Cloud or keeping instances in multiple IBM Cloud regions in sync. The same cartridge file can be deployed to a different {{site.data.keyword.wh-acd_short}} instance in different regions for the synchronization purpose. If instance owners are using a cartridge in one region and they're switching over to another region, they need to deploy that same cartridge in the second region. In other words, cartridge deployments are isolated to the region in which they're being deployed.


### Detecting a location outage
{: outage_detection}
The {{site.data.keyword.wh-acd_full}} service provides a health check API that can be called repeatedly to ensure the service is available.  Successive internal service error responses from the API could be used as an indicator that the service is no longer available in a specific location.


#### Recovery
{: recovery}
The instance owner must ensure the custom cartridge is available in the new location prior to recovering an existing {{site.data.keyword.wh-acd_short}} instance. The following steps can be performed for recovery:

  1.  Provision a new instance of the {{site.data.keyword.wh-acd_full}} service in a different region.
  2.  Deploy your existing cartridge files to the new service instance.
  3.  Modify your applications to use the URL and credentials of the new service instance.

