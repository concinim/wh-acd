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

Using the  {{site.data.keyword.wh-acd_short}} Configuration Editor, you can customize the annotations provided by  {{site.data.keyword.wh-acd_short}}.  The configuration editor is currently not exposed externally.  If you wish to customize your {{site.data.keyword.wh-acd_short}} deployment, contact IBM services.  

The configuration editor allows you to create several types of configuration artifacts that can be used to customize  {{site.data.keyword.wh-acd_short}}'s output. For example, you can create a custom dictionary to add your unique terminology for detecting concepts or you can define your own domain specific clinical attributes.

The customization artifacts are bundled into a knowledge cartridge that can be published and deployed to  {{site.data.keyword.wh-acd_short}}. The cartridge will include a profile that specifies the configurations for each annotator. The cartridge will also contain one or more flows that contain a series of annotators to invoke using the /v1/analyze/{flow_id} API.  

See the configuration editor for more information on customizing  {{site.data.keyword.wh-acd_short}} and for more information on standard profile operations such as profile listing, creation, updating and deletion.


## Flows
{: #flows}

An annotator flow within  {{site.data.keyword.wh-acd_short}} defines a set of one or more annotators, and optionally, includes annotator configurations and flow sequence. Annotator flows can be dynamically defined as part of a request, or predefined and persisted for a specific tenant. When persisted, a flow definition also contains a name, ID, and description of the flow, in addition to the annotators and their configurations. When a flow is specified as part of an analyze request, the sequence of annotators and any configurations defined in the flow are internally applied to the request when processing and analyzing the input text.
{:shortdesc}

The  {{site.data.keyword.wh-acd_short}} Configuration Editor should be used for standard flow operations such as flow listing, creation, updating and deletion. {{site.data.keyword.wh-acd_short}} provides two predefined flows for evaluation purposes.

<table>
<tr>
<th>Annotator Flow</th><th>Description</th>
</tr>
<tr><td>ibm_clinical_insights_v1.0_standard_flow</td><td> Annotator for Clinical Data provides a ready-to-use capability, called Clinical Insights, that extracts clinically relevant information by performing deep contextual analysis of clinical notes. The Clinical Insights flow is a default configuration provided with Annotator for Clinical Data that produces clinical attributes for Prescribed Medications, Diagnoses, Therapeutic Procedures, and Diagnostic Procedures by contextually evaluating each type of clinical information to determine that it is both relevant and pertinent to the patient. See the Clinical Insights documentation for a detailed explanation.
<br><br>
As new versions of the Clinical Insights flow are released, older versions will be deprecated and eventually retired. This is known as the version lifecycle. Annotator for Clinical Data will support two versions of the Clinical Insights flows, the current latest version and the previous version. This is known as an “n-1” version support scheme. Once an older version is marked as “deprecated”, a 90 day period will begin before the deprecated version is officially “retired” and no longer functional. The deprecated version will remain operational for a 90 day period before it is considered retired. Once a version has been retired, it will no longer be available and any attempts to use a retired version will fail.</td></tr>

</table>
