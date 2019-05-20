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

See the DET <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/help/DET_GettingStartedGuide.pdf">Getting Started Guide</a> for more information on customizing  {{site.data.keyword.wh-acd_short}}.
