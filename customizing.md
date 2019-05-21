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


## Flows
{: #flows}

An annotator flow within  {{site.data.keyword.wh-acd_short}} defines a set of one or more annotators, and optionally, includes annotator configurations and flow sequence. Annotator flows can be dynamically defined as part of a request, or predefined and persisted for a specific tenant. When persisted, a flow definition also contains a name, ID, and description of the flow, in addition to the annotators and their configurations. When a flow is specified as part of an analyze request, the sequence of annotators and any configurations defined in the flow are internally applied to the request when processing and analyzing the input text.
{:shortdesc}

The [Domain Expert Tool (DET)](https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html) should be used for standard flow operations such as flow listing, creation, updating and deletion. {{site.data.keyword.wh-acd_short}} provides two predefined flows for evaluation purposes.

<table>
<tr>
<th>Annotator Flow</th><th>Description</th>
</tr>
<tr><td>general_medical_v1.0_flow</td><td> Includes the concept detection annotator with the umls.2017AA library and attribute detection annotator with the general_medical_v1.0 and general_labs_v1.0 attribute sets. This flow might be used for detecting clinical attributes in a general medical domain.</td></tr>
<tr><td>general_cancer_v1.0_flow</td><td> Includes the concept detection annotator with the umls.2017AA library and attribute detection annotator with the attribute sets: general_medical_v1.0, general_labs_v1.0 and general_cancer_v1.0. This flow might be used for detecting clinical attributes in a medical oncology and disease domain.</td>
</tr>
</table>
