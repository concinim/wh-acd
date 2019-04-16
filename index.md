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

The IBM Watson Annotator for Clinical Data (ACD) is built to find medical concepts, medical codes, and contextual information in unstructured text.  ACD provides turn key annotators as well as highly customizable annotators that you can tune specifically for your application needs.  The Unified Medical Language System ([UMLS](https://www.nlm.nih.gov/research/umls/)) is the primary source for ACD concepts and medical codes.  ACD can also work with user provided ontologies beyond UMLS.  

To illustrate the basic function of ACD, let's look at this with a simple example.  Imagine that we have the following small snippet of text:

```There were no signs of ulceration```

The resulting concept over ulceration will contain standard medical codes along with contextual information about the concept - in this example, the concept is negated.

```
{
    "cui": "C3887532",
    "preferredName": "Ulceration",
    "semanticType": "patf",
    "source": "umls",
    "sourceVersion": "2018AA",
    "type": "umls.PathologicFunction",
    "begin": 23,
    "end": 33,
    "coveredText": "ulceration",
    "negated": true,
    "nciCode": "C25757",
    "snomedConceptId": "263913002",
    "vocabs": "MTH,NCI_CDISC,NCI_FDA,NCI,OMIM,SNOMEDCT_US,NCI_NCI-GLOSS"
}```

To learn about all of the ways you can customize ACD, see the [Customizing](wh-acd?topic=wh-acd-customizing#customizing) section and learn ahow you can use the Domain Expert Tool to build custom medical NLP for your application.


{: shortdesc}

## Customizable concept annotators

These annotators can be tailored to your needs using the Domain Expert Tool.
### Attributes
{: #attribues}

Attributes are higher order concepts generally composed of multiple pieces of information found in a document.  An example of this might be understanding if a patient is overweight or not.  Given some example text, we would like to know if the patient is overweight or not.

```The patient is a 37 year old male who is 6 feet tall and weighs 170 lbs.```

Using configurable [concept values](wh-acd?topic=wh-acd-concept_value#concept_value), we know the patient's height and weight.  ACD can run inference rules to distill this text down to a single attribute that we'll call `NORMAL_WEIGHT`.  Custom attributes like this are a powerful way to distill unstructured text into actionable insights.

For more information, see [Attributes](wh-acd?topic=whc-acd-attribute_detection#attribute_detection)

### Concepts
{: #concepts}

The concept annotator finds UMLS or custom concepts in unstructured text.

For more information, see [Concepts](wh-acd?topic=wh-acd-concept_detection#concept_detection)

### Concept Value
{: #conceptValue}

The concept value annotator creates composite attributes resulting from a medical concept and an associated value.  It supports scalar values as well as value ranges.  In our attribute example above, the combination of `height` with `6 feet` is an example of how concept values work.

For more information, see [Concept Value](wh-acd?topic=wh-acd-concept_value#concept_value)

## Contextual Annotators

Contextual annotators use the surrounding context of the document to provide a deeper understanding of concepts.

### Negation
{: #negation}

Identifies spans of text with an implied negative meaning.  For example: _There are no signs of ulceration in the stomach lining._

For more information, see [Negation](wh-acd?topic=wh-acd-negation_detection#negation_detection)

### Hypothetical
{: #hypothetical}

Identifies spans of text are the object of a hypothetical statement.  For example: _We discussed the pros and cons of chemotherapy._

For more information, see [Hypothetical](wh-acd?topic=wh-acd-hypothetical_detection#hypothetical_detection)

### Concept Disambiguation
{: #disambiguation}

Determines the validity of UMLS concepts detected in a document.

For more information, see [Disambiguation](wh-acd?topic=wh-acd-concept_disambiguation#concept_disambiguation)


### Turn Key Annotators
{: #turnKeyAnnotators}

ACD provides a set of prebuilt annotators targeted at specific medical domains.

* [Allergy](wh-acd?topic=wh-acd-allergies#allergies)
* [Cancer](wh-acd?topic=wh-acd-cancer#cancer)
* [Ejection Fraction](wh-acd?topic=wh-acd-ejection_fraction#ejection_fraction)
* [Lab Values](wh-acd?topic=wh-acd-lab_values#lab_values)
* [Living Assistance](wh-acd?topic=wh-acd-living_assistance#living_assistance)
* [Medications](wh-acd?topic=wh-acd-medications#medications)
* [Named Entities](wh-acd?topic=wh-acd-named_entities#named_entities)
* [Procedures](wh-acd?topic=wh-acd-procedure#procedure)
* [Sections](wh-acd?topic=wh-acd-sections#sections)
* [Smoking](wh-acd?topic=wh-acd-smoking#smoking)
* [Symptoms & Diseases](wh-acd?topic=wh-acd-symptom_disease#symptom_disease)

### Integration with Natural Language Understanding
{: #nlu}

ACD provides integration with the IBM Watson Natural Language Understanding (NLU) service.  You can use the out of the box models provided by NLU or you can call a custom NLU model and integrate it into your ACD API call.

For more information, see [NLU](wh-acd?topic=wh-acd-nlu_annotator#nlu_annotator)
