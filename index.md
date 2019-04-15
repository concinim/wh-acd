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

The IBM Watson Annotator for Clinical Data (ACD) allows you to create domain specific medical NLP.  ACD provides turn key annotators along with highly customizable annotators that you can tune specifically for your application needs.  


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

If you choose to use the section, negation, and concept detection annotators in your ACD call, then the resulting concepts will contain section information as well as negation polarity.  Maybe for your use case, family history doesn't matter.  If you do not need these annotations for your application, you can specify filters in your ACD configuration that will remove all family history annotations.

<pre><code>  
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
</pre></code>  

Similarly, if you are not interested in negated concepts, you can filter them at the application level based on the value of the **negated** flag or you can configure ACD to not return negated concepts.

<pre><code>  
{
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
  }
  </pre></code>

### Medical codes
{: #medicalcodes}

ACD normalizes medical concepts into many common medical codes.  The following table shows the medical code support for each annotator available in ACD.

<table>
  <tr>
    <th><b>Medical Codes</b></th>
    <th>NCI</th>
    <th>ICD 9/10</th>
    <th>LOINC</th>
    <th>MeSH</th>
    <th>RxNorm</th>
    <th>SNOMED CT</th>
    <th>CPT</th>
    <th>CCS</th>
    <th>HCC</th>
    <th>UMLS CUI</th>
  </tr>

  <tr>
    <th colspan="11"><b>Turn Key Annotators</b></th>
  </tr>
  <tr><td>Allergy</td> <td></td> <td></td> <td></td> <td></td> <td>&#10004;</td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td>Cancer</td> <td></td> <td>&#10004;</td> <td></td> <td></td> <td></td> <td>&#10004;</td> <td></td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td>   </tr>
  <tr><td>Ejection Fraction</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td>Lab Value</td> <td></td> <td></td> <td>&#10004;</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td>Living Assistance</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td>Medication</td> <td></td> <td></td> <td></td> <td></td> <td>&#10004;</td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td>Named Entities</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td>Procedure</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td>&#10004;</td> <td></td> <td></td> <td>&#10004;</td>   </tr>
  <tr><td>Symptom Disease</td> <td></td> <td>&#10004;</td> <td></td> <td></td> <td></td> <td>&#10004;</td> <td></td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td>   </tr>

  <tr>
    <th colspan="11"><b>Configurable Concept Annotators</b></th>
  </tr>
  <tr><td>Attribute</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td>   </tr>
  <tr><td>Concept (UMLS 2018AA+)</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td></td> <td></td> <td>&#10004;</td>   </tr>
  <tr><td>Concept Value</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td>&#10004;</td></tr>
  <tr><td>Relation</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>

  <tr>
    <th colspan="11"><b>Cotextual Annotators</b></th>
  </tr>
  <tr><td>Disambiguation</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>
  <tr><td>Hypothetical</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>
  <tr><td>Negation</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>
  <tr><td>Section</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>

</table>

### Attributes
{: #attribues}

Attributes are customizable higher order concepts generally composed of multiple pieces of information found in a document.

For more information, see [Attributes](docs/servics/wh-acd?topic=attributes)

### Concepts
{: #concepts}

The concept annotator finds Unified Medical Language System (UMLS) concepts in unstructured text.

For more information, see [Concepts](docs/servics/wh-acd?topic=concepts)

### Concept Value
{: #conceptValue}

The concept value annotator creates composite attributes resulting from a medical concept and an associated value.  It supports scalar values as well as value ranges.

For more information, see [Concept Value](docs/servics/wh-acd?topic=conceptValues)


### Negation
{: #negation}

Identifies spans of text with an implied negative meaning.  For example: _there are no signs of ulceration in the stomach lining_

For more information, see [Negation](docs/servics/wh-acd?topic=negation)

### Hypothetical
{: #hypothetical}

Identifies spans of text are the object of a hypothetical statement.

For more information, see [Hypothetical](docs/servics/wh-acd?topic=negation)

### Turn Key Annotators
{: #turnKeyAnnotators}

Allergy
Cancer
Ejection Fraction
Lab Values
Living Assistance
Medications
Named Entities
Procedures
Sections
Smoking
Symptoms & Diseases

### Concept Disambiguation
{: #disambiguation}

Description of Disambiguation
