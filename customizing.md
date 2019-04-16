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

# Customizing
{: #Customizing}

## Cartridges
{: #cartridges}

Cartridges are containers used for the customization of ACD. Within a cartridge are domain-specific artifacts chosen by the consumer detailing ACD configuration information. Artifacts created by the consumer are restricted to be less then 2MB.  Cartridges are built using the [Domain Expert Tool (DET)](https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/). Following the creation of a cartridge, the consumer will customize ACD by deploying a snapshot of the cartridge to ACD. The deployment of the cartridge snapshot will create <q>profile</q> and <q>flow</q> objects within the ACD service. These objects can then be referenced as part of the request when invoking ACD.
{:shortdesc}

## Domain Expert Tool
{: #det}

The <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html" target="_blank">Domain Expert Tool (DET)</a> is provided as a means of defining and evaluating customizations for ACD. Once defined, customizations are exported from DET in the form of a cartridge (zip file). The cartridge can then be deployed to ACD via the /deploy API on a per-tenant basis. Consumers can then apply these customizations when analyzing text by including the corresponding flow ID for a cartridge as a path parameter on the /analyze/{flow_id} request.

See the DET <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/help/DET_GettingStartedGuide.pdf">Getting Started Guide</a> for details on the ACD configurations supported by the tool.
