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
{:caption: .caption}
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

The {{site.data.keyword.wh-acd_short}} Configuration Editor supports extensive customization of the annotators as well as the ability to preview the customizations and export them in the form of a cartridge (zip file) that can be deployed directly to the service via the `/cartridges` APIs.

The configuration editor facilitates the following customizations:

| Customization | Description |
|----|----|
| Dictionaries | A set of terms describing a unique concept that is matched against the provided text to be analyzed. |
| Derived Concepts | Rules for deriving concepts when one or more other concepts or tokens appears in the surrounding context. |
| Filters | Conditional rules for omitting undesired annotations from the service response. |
| Clinical Attributes | Configurable annotations built upon one or more other annotations. Optionally, semantically linked values in the surrounding context can be captured and associated with the attribute. |
| Derived Clincal Attributes | Conditional logic and expressions for deriving new attributes based on values associated with other attributes. |
| Attribute Qualifiers | Configurations for detecting qualifying terms in the immediate context of an attribute and capturing the qualifiers as a field within the output attribute annotation. |
| Ontological Relations | Ontology configurations for extracting ontological relations between concepts cooccurring within the same sentence. |
| CPT Code Mapping | Mapping configurations for outputting CPT codes from the concept and procedure annotators. |
{: caption="Table 1. Customizations facilitated by the configuration editor" caption-side="top"}

[Contact your IBM representative](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watsonhealthna) to learn more about leveraging the configuration editor to customize the behavior of the service.
