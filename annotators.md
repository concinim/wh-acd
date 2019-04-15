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

# Annotators
{: #annotators}

<h3 id="customize-acd">Customization</h3>

The <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html" target="_blank">Domain Expert Tool (DET)</a> is provided as a means of defining and evaluating customizations for ACD. Once defined, customizations are exported from DET in the form of a cartridge (zip file). The cartridge can then be deployed to ACD via the /deploy API on a per-tenant basis. Consumers can then apply these customizations when analyzing text by including the corresponding flow ID for a cartridge as a path parameter on the /analyze/{flow_id} request.

See the DET <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/help/DET_GettingStartedGuide.pdf">Getting Started Guide</a> for details on the ACD configurations supported by the tool.

<h4>Unified Medical Language System (UMLS) Versions</h4>
The following annotators leverage UMLS vocabularies: <i>allergy, cancer, daily living assistance annotators (bathing_assistance, dressing_assistance, eating_assistance, seeing_assistance, toileting_assistance, walking_assistance), ejection_fraction, lab_value, medication, procedure, smoking, symptom_disease.</i>
Also, a UMLS library is provided with the concept_detection annotator.
UMLS itself is updated twice each year in May (AA release) and November (AB release).
ACD will provide new versions of the UMLS-based libraries each year and retain n-2 versions of UMLS with each version update, with the n-2 version becoming deprecated and the n-3 version removed.
If ACD consumers want to automatically be upgraded to the latest version of UMLS each year, they should designate <b>umls.latest</b> as the UMLS version.
If ACD consumers want to control if and when they upgrade to a particular new version of UMLS, they should designate an explicit version of UMLS (e.g. umls.2018AA).
Consumers defining an explicit version of UMLS will need to upgrade to a new version when the version they're using becomes deprecated, before it is ultimately truncated with the next UMLS version update.
