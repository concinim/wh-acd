---

copyright:
  years: 2011, 2019
lastupdated: "2019-04-12"

keywords: annotator clinical data, clinical data, annotation

subcollection: wh-acd

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Customizing
{: #customizing}

Using the <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html" target="_blank">Domain Expert Tool (DET)</a>, you can customize the annotations provided by  {{site.data.keyword.wh-acd_short}}. The DET allows you to create several types of configuration artifacts that can be used to customize  {{site.data.keyword.wh-acd_short}}'s output. For example, you can create a custom dictionary to add your unique terminology for detecting concepts or you can define your own domain specific clinical attributes.

The customization artifacts are bundled into a knowledge cartridge that can be published and deployed to  {{site.data.keyword.wh-acd_short}}. The cartridge will include a profile that specifies the configurations for each annotator. The cartridge will also contain one or more flows that contain a series of annotators to invoke using the /v1/analyze/{flow_id} API.  

See the DET <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/help/DET_GettingStartedGuide.pdf">Getting Started Guide</a> for more information on customizing  {{site.data.keyword.wh-acd_short}} and for more information on standard profile operations such as profile listing, creation, updating and deletion.

## Profiles
{: #profiles}

Profiles within  {{site.data.keyword.wh-acd_short}} house annotator configurations associated with one or more annotators. Profiles can then be referenced within an  analyze request where  {{site.data.keyword.wh-acd_short}} will look up the annotator configurations defined within the referenced profile and inject annotator configurations within the profile into the corresponding annotators defined within the  {{site.data.keyword.wh-acd_short}} request flow. Some predefined profiles available to all tenants - e.g. predefined profiles for evaluating predefined attribute sets are listed below.
{:shortdesc}

```javascript
{
    "default_profile_v1.0": {
      "description":"Default parameters for the concept detection and the attribute detection annotators when no profile id is specified in the flow. "
    },
    "general_cancer_v1.0": {
        "description": "This profile features a collection of Clinical Attributes that focus on cancer patient disease characteristics including the cancer type, disease progression, staging, tumor markers, and treatments."
    },
    "general_medical_v1.0": {
        "description": "This profile feature a collection of Clinical Attributes that represent the patient characteristics commonly used by physicians during a medical examination including laboratory, demographics, symptoms, diseases, and procedures."
    }
}
```
