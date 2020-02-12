---

copyright:
  years: 2020
lastupdated: "2020-02-11"

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

# Clinical Insights Overview
{: #clinical_insights_overview}

The {{site.data.keyword.wh-acd_short}} provides an out-of-the-box capability to extract contextual information about key concept types in clinical notes about a patient.  The clinical insights function is composed of two core capabilities:

1. A set of models that provide contextual features for key clinical types (medication, diagnosis, and procedure).
2. An out of the box cartridge that uses those features to answer a simple question - does this entity apply to the patient?

<h4>Models</h4>

Each of the models provides contextual features relevant to the annotation types that the model processes.  The models add features to annotations that either come from out-of-the-box {{site.data.keyword.wh-acd_short}} annotators or from custom annotations you create using the {{site.data.keyword.wh-acd_short}} Configuration Editor.  There are currently models for the following:

1. [Medication](wh-acd?topic=wh-acd-clinical_insights_medication#clinical_insights_medication)
2. [Diagnosis](wh-acd?topic=wh-acd-clinical_insights_diagnosis#clinical_insights_diagnosis)
3. [Procedure](wh-acd?topic=wh-acd-clinical_insights_procedure#clinical_insights_procedure)
