---

copyright:
  years: 2020
lastupdated: "2020-04-21"

keywords: annotator clinical data, clinical data, annotation

subcollection: wh-acd

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:codeblock: .codeblock}
{:tip: .tip}

# Responsibilities for {{site.data.keyword.wh-acd_short}}
{: #responsibilities}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.wh-acd_short}}.

## Disaster recovery
{: #disaster-recovery-responsibilities}

<table>
  <thead>
    <th>Task</th>
    <th>{{site.data.keyword.IBM_notm}} Responsibilities</th>
    <th>Your Responsibilities</th>
  </thead>
  <tbody>
    <tr>
      <td>High availability, backup, and disaster recovery</td>
      <td>
        <ul>
          <li>
            Host service in multiple regions
          </li>
          <li>
            Load-balance requests across multiple data centers per region
          </li>
          <li>
            Back up user configuration data daily
          </li>
        </ul>
      </td>
      <td>
        <ul>
          <li>
            Back up service configuration artifacts: annotator flows, profiles, cartridges
          </li>
          <li>
            Provision service instances in multiple regions
          </li>
          <li>
            In the event one region becomes unavailable, restore configuration artifacts from backup or keep configuration artifacts in sync across regions
          </li>
          <li>
            Update the service endpoint and api key in your solution to begin leveraging the service in an alternate region
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
{: caption="Table 1. Responsibilities for disaster recovery" caption-side="top"}
