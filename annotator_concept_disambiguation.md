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

# Concept Disambiguation
{: #concept_disambiguation}

The Unified Medical Language System (UMLS) provides broad medical concept coverage.  The version that ships with ACD covers approximately 2 million concepts.  The breadth of this information is useful to explore a new medical domain, but it can also create false annotations over spans of text.  Consider a simple acronym like _TEC_.  In a recent version of UMLS, TEC is annotated with nine concepts, that represent seven different ideas - Thymic epithelial cell, Transient erythroblastopenia of childhood, Transluminal extraction catheter, TEC gene/protein, NR4A3 wt Allele, Tubingen electric campimetry, and RHBDF2 wt Allele.  Collisions like this are not uncommon in UMLS.

The Concept Disambiguation annotator ranks the contextual validity of a UMLS [concept](wh-acd?topic=wh-acd-concept_detection#concept_detection) based on sentence and document level information.

If your use case requires you to handle a broad range of medical topics and concept level precision is important, adding disambiguation to your ACD flow can help.  Conversely, if you work with a relatively small set of concepts or you only use complex derived  [attributes](wh-acd?topic=whc-acd-attribute_detection#attribute_detection), disambiguation may not be necessary.

The disambiguation annotator can be configured to remove annotations it determines are invalid or to tag them as invalid but leave them in the API response.
