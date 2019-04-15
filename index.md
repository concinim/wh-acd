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

Every annotator in ACD has the ability to add additional information to an annotation.  These pieces of information are called _features_.  Features from each annotator are aggregated internally to give you easy to use annotations that contain all relevant information about a text span.  ACD allows you to filter annotations that may not be important for your use case from the API response.  An example of this is a disease that is detected in the _family history_ section of a medical record.  Since that disease does not apply directly to the patient, it may be something you choose to ignore in your application.  For more details on features, see [Features](docs/servics/wh-acd?topic=features).


### Medical codes
{: #medicalcodes}

ACD normalizes medical concepts into many common medical codes.  The following table shows the medical code support for each annotator available in ACD.

**REMOVE ME!!! DEBUG VERSION: 1.5**

<table>
  <tr>
    <th style="width:100%; min-width:0 !important">Medical Codes</th>
    <th style="width:1%; min-width:0 !important">NCI</th>
    <th style="width:1%; min-width:0 !important">ICD 9/10</th>
    <th style="width:1%; min-width:0 !important">LOINC</th>
    <th style="width:1%; min-width:0 !important">MeSH</th>
    <th style="width:1%; min-width:0 !important">RxNorm</th>
    <th style="width:1%; min-width:0 !important">SNOMED CT</th>
    <th style="width:1%; min-width:0 !important">CPT</th>
    <th style="width:1%; min-width:0 !important">CCS</th>
    <th style="width:1%; min-width:0 !important">HCC</th>
    <th style="width:1%; min-width:0 !important">UMLS CUI</th>
  </tr>

  <tr>
    <th colspan="11" width="1%"><b>Turn Key Annotators</b></th>
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

  <tr><th></th></tr>
  <tr>
    <th colspan="11"><b>Configurable Concept Annotators</b></th>
  </tr>
  <tr><td>Attribute</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td>   </tr>
  <tr><td>Concept (UMLS 2018AA+)</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td>&#10004;</td> <td></td> <td></td> <td>&#10004;</td>   </tr>
  <tr><td>Concept Value</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td>&#10004;</td></tr>
  <tr><td>Relation</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>

  <tr><th></th></tr>
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

### NLU
{: #nlu}

ACD provides integration with the IBM Watson Natural Language Understanding (NLU) service.  You can use the out of the box models provided by NLU or you can call a custom NLU model and integrate it into a larger ACD flow.

For more information, see [NLU](docs/servics/wh-acd?topic=nlu)

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
