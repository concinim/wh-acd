---

copyright:
  years: 2011, 2019
lastupdated: "2019-04-12"

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

# Customization
{: #customization}

## Domain Expert Tool

The <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html" target="_blank">Domain Expert Tool (DET)</a> is provided as a means of defining and evaluating customizations for ACD. Once defined, customizations are exported from DET in the form of a cartridge (zip file). The cartridge can then be deployed to ACD via the /deploy API on a per-tenant basis. Consumers can then apply these customizations when analyzing text by including the corresponding flow ID for a cartridge as a path parameter on the /analyze/{flow_id} request.

See the DET <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/help/DET_GettingStartedGuide.pdf">Getting Started Guide</a> for details on the ACD configurations supported by the tool.


## Annotation Customization

Annotation customization can be carried out using either _filters_ or _whitelists_. _Filtering_ is the ability to define conditional filtering of annotations based on response annotation field values to address false-positive or otherwise non-applicable annotations. _Whitelists_ provide the ability to define additional surface forms for an annotator to address false-negatives.

The Filter and Whitelist content that follows describes how to provide customization definitions at request time or how to specify use of a stored configuration at request time.
