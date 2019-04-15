---

copyright:
  years: 2019
lastupdated: "2019-04-15"

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

# Annotation Features
{: #features}

Features are additional pieces of information about an annotation.  In ACD, features are used to convey a broad range of information about an annotation including negation status, hypothetical status, the section in which the annotation was found, medical codes associated with a concept, etc.

Let's look at a simple example to understand how features can be used to help hone in on the concepts that are most important for your application.

Given the following text, we want to identify the disease attributes that are directly associated with the patient.

```
FAMILY HISTORY:

The patient's father died of heart disease.

HISTORY OF PRESENT ILLNESS:

The patient is having digestive problems.  Previous testing has ruled out crohns disease, but further testing is needed to determine the cause of these issues.
```

For this example, our [cartridge](wh-acd?topic=wh-acd-cartridges#cartridges) defines a [flow](wh-acd?topic=wh-acd-flows#flows) that uses the following annotators:
[section](wh-acd?topic=wh-acd-sections#sections), [concept detection](wh-acd?topic=wh-acd-concept_detection#concept_detection), and [negation](wh-acd?topic=wh-acd-negation_detection#negation_detection).

Because the section annotator and negation annotator are part of the flow, section and negation attributes will be included in the concept annotations as appropriate.

The first disease we find is _Heart Disease (UMLS CUI C0018799)_.  For this sample use case, we do not want to consider this concept because it appears in the family history section of the document.  Notice that section information is included in the annotation.  You can have ACD filter this annotation from the API response using a [Filter](wh-acd?topic=wh-acd-filters#filters).

<pre><code>{
            "cui": "C0018799",
            "preferredName": "Heart Diseases",
            "semanticType": "dsyn",
            "source": "umls",
            "sourceVersion": "2018AA",
            "type": "umls.DiseaseOrSyndrome",
            "begin": 46,
            "end": 59,
            "coveredText": "heart disease",
            "icd10Code": "I51.9",
            <b>"sectionNormalizedName": "Family History"</b>,
            "nciCode": "C3079",
            "snomedConceptId": "56265001",
            "meshId": "M0009951",
            "vocabs": "MTH,LNC,NCI_NICHD,CCS_10,CSP,MSH,CST,COSTAR,CHV,CCS,MEDLINEPLUS,NCI,LCH_NW,AOD,NDFRT,SNOMEDCT_US",
            <b>"sectionSurfaceForm": "FAMILY HISTORY"</b>,
            "icd9Code": "429.89,V47.2",
            "loincId": "LA10523-1"
}</pre></code>  

In the next section of the document, there are two concepts present that describe a medical condition - _digestive problems_ and _crohns disease_.  In this example, the language in the document around crohns disease indicates that the patient does not have crohns disease.  The resulting annotation indicates that the concept for crohns disease is negated.  As before, you can configure ACD to filter negated concepts from the API response if you do not want to process them.

<pre><code>{
            "cui": "C0010346",
            "preferredName": "Crohn Disease",
            "semanticType": "dsyn",
            "source": "umls",
            "sourceVersion": "2018AA",
            "type": "umls.DiseaseOrSyndrome",
            "begin": 165,
            "end": 179,
            "coveredText": "crohns disease",
            <b>"negated": true</b>,
            "loincId": "LA10554-6",
            "icd10Code": "K50.90",
            "sectionNormalizedName": "History of present illness",
            "nciCode": "C2965",
            "snomedConceptId": "34000006",
            "meshId": "M0005335",
            "vocabs": "MTH,NCI_NICHD,LNC,CSP,MSH,CST,HPO,OMIM,COSTAR,AIR,MTHMST,NCI_NCI-GLOSS,CHV,MEDLINEPLUS,NCI,LCH_NW,AOD,NDFRT,SNOMEDCT_US,DXP",
            "sectionSurfaceForm": "HISTORY OF PRESENT ILLNESS"
  }</pre></code>

  The concept over _digestive problems_ is not negated and appears in a section of the document that we are interested in so we'll keep it for use in our application.

  <pre><code>{
  "cui": "C0851121",
  "preferredName": "digestive problem",
  "semanticType": "sosy",
  "source": "umls",
  "sourceVersion": "2018AA",
  "type": "umls.SignOrSymptom",
  "begin": 113,
  "end": 131,
  "coveredText": "digestive problems",
  "sectionNormalizedName": "History of present illness",
  "vocabs": "CHV",
  "sectionSurfaceForm": "HISTORY OF PRESENT ILLNESS"
}</pre></code>
