---

copyright:
  years: 2019
lastupdated: "2019-04-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# About
{: #about}

The IBM Watson Annotator for Clinical Data (ACD) allows you to create domain specific medical NLP.  ACD provides turn key annotators along with highly customizable annotators that you can tune specifically for your needs.  ACD normalizes concepts into many common medical ontologies including UMLS, SNOMED, RXNORM, LOINC, and ICD *** OTHERS WE NEED TO ADD ***

The ACD annotators can pass feature information from annotator to the next.  


{: shortdesc}

## Features
{: #features}

ACD allows you to customize the annotators you need for your use case and package them into a single API call.  Features from each annotator are aggregated internally to give you easy to use annotations.  For example, given the following text:

```
FAMILY HISTORY:

The patient's father died of heart disease.

HISTORY OF PRESENT ILLNESS:

The patient is having digestive problems.  Previous testing has ruled out crohns disease, but further testing is needed to determine the cause of these issues.
```

If you choose to use the section, negation, and concept detection annotators in your ACD call, then the resulting concepts will contain section information as well as negation polarity.  Maybe for your use case, family history doesn't matter.  If you consider these annotations noise, tou can specify filters in your ACD configuration that will remove all family history annotations.

```
{
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
            "sectionNormalizedName": "Family History",
            "nciCode": "C3079",
            "snomedConceptId": "56265001",
            "meshId": "M0009951",
            "vocabs": "MTH,LNC,NCI_NICHD,CCS_10,CSP,MSH,CST,COSTAR,CHV,CCS,MEDLINEPLUS,NCI,LCH_NW,AOD,NDFRT,SNOMEDCT_US",
            "sectionSurfaceForm": "FAMILY HISTORY",
            "icd9Code": "429.89,V47.2",
            "loincId": "LA10523-1"
}
```

Similarly, if you are not interested in negated concepts...

*** Need to get an example that works

### Concepts
{: #concepts}

Description of concepts and expanded concepts


### Attributes
{: #attribues}

Description of attributes

### Negation
{: #negation}

Description of negation

### Section
{: #section}

Description of section

### Hypothetical
{: #hypothetical}

Description of hypothetical

### ACI annotators
{: #aci}

Probably don't want to call this ACI - Just a placeholder at this point

### Disambiguation
{: #disambiguation}

Description of Disambiguation

