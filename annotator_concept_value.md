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

# Concept Value
{: #concept_value}

The concept_value annotator is intended to be used in conjunction with the concept_detection annotator to identify values within unstructured data associated with concepts retrieved from the concept_detection annotator. Values can be either scalar, a range, boolean, or textual. Concept Values are detected via identifying lexical triggers in unstructured data indicating a mathematical relationship (e.g >, >=, <, <=, etc.) between a previously detected concept and value. For that reason they are particularly useful for criteria matching use cases since they can be used to build a set of constraints or rules that must be met in order for something to be eligible. The concept_value annotator however is intended to be used generically and not just in criteria matching solutions.
{:shortdesc}

#### Dependencies

The concept_value annotator detects values from unstructured clinical text and associates them with previously detected concepts from the concept_detection annotator. Thus concept_detection must run prior to concept_value within an annotator flow to function properly.

#### Annotation Types

* ConceptValue

#### Response Fields

<table>
<tr>
<th>Fields</th><th>Description</th>
</tr>
<tr>
<td>cui</td>
<td>UMLS Concept Unique ID (CUI). CUIs are used to uniquely identify concepts across different UMLS sources.</td>
</tr>
<tr>
<td>preferredName</td>
<td>Normalized name for the UMLS concept.</td>
</tr>
<tr>
<td>trigger</td>
<td>The lexical trigger that fired the ConceptValue relationship, for example: <q>greater than</q>, <q>less than</q>, <q>at least</q>, or <q>more than</q>, etc.</td>
</tr>
<tr>
<td>type</td>
<td>The long-form UMLS semantic type.</td>
</tr>
<tr>
<td>begin</td>
<td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td>
</tr>
<tr>
<td>end</td>
<td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td>
<td></td>
</tr>
<tr>
<td>unit</td>
<td>The units in which the value is specified.</td>
</tr>
<tr>
<td>value</td>
<td>The value for the subject concept.</td>
</tr>
<tr>
<td>dimension</td>
<td>This feature contains the dimension of the units of this value, for example: <q>time</q>, <q>length</q>, <q>volume</q>, <q>pressure</q>, etc.</td>
</tr>
<tr>
<td>rangeBegin</td>
<td>When the value is a range this feature contains the beginning value of the range.</td>
</tr>
<tr>
<td>rangeEnd</td>
<td>When the value is a range this feature contains the end value of the range.</td>
</tr>
</table>

#### Concept Value Examples

##### Example 1: Greater than or equal to Concept Value with units

> **Text:** _<q>The patient must have **platelet count at least 100,000/mm^3**.</q>_

In the example text above, a ConceptValue annotation will be constructed in reference to the <q>platelet count</q> concept. The ConceptValue annotation in this case sufficiently captures the platelet count constraint articulated in natural language.

```javascript
"conceptValues": [
  {
    "cui": "C1287267",
    "dimension": "concentration",
    "preferredName": "Finding of platelet count",
    "trigger": "greater than or equal to",
    "unit": "/mm^3",
    "value": "100,000",
    "type": "ConceptValue",
    "begin": 22,
    "end": 58,
    "coveredText": "platelet count at least 100,000/mm^3"
  }
]
```

The **trigger** field can be used to construct and evaluate the constraint described therein. i.e. the **platelet count** finding must be >= the value (100,000) in units (mm^3). Assuming a patient's platelet count is 90,000 mm^3, 90,000mm^3 <= 100,000mm^3 == true, so this criteria would be met.

##### Example 2: Greater than or equal to Concept Value with units and natural language expression of value - _<q>at least</q>_

> **Text:** _The patient must have a **platelet count of at least 100000/μl**._

This example illustrates the capability within concept value to detect and normalize numeric values articulated in natural language from unstructured data.

```javascript
"conceptValues": [
  {
    "cui": "C0032181",
    "dimension": "concentration",
    "preferredName": "Platelet Count measurement",
    "trigger": "greater than or equal to",
    "unit": "/μl",
    "value": "100000",
    "type": "ConceptValue",
    "begin": 24,
    "end": 60,
    "coveredText": "platelet count of at least 100000/μl",
    "negated": false,
    "hypothetical": false
  }
]
```

##### Example 3: ConceptValue with non-numeric value - _<q>positive</q>_

> **Text:** _<q>**Hormone receptor positive** patients are candidates for anti-estrogen therapy.</q>_

This example demonstrates a non-numeric value (**positive**) for a concept that does not use numeric values.

```javascript
"conceptValues": [
  {
    "cui": "C0019929",
    "preferredName": "Hormone Receptor",
    "value": "positive",
    "type": "ConceptValue",
    "begin": 1,
    "end": 26,
    "coveredText": "Hormone receptor positive"
  }
]
```

##### Example 4: ConceptValue with a range value set

> **Text:** _The area of a typical **aortic valve is 3.0 to 4.0 cm2**._

This example demonstrates a set of range values. The trigger **within** indicates that a ConceptValue annotation encompasses a set of range values.

```javascript
"conceptValues": [
    {
      "cui": "C0003501",
      "dimension": "area",
      "preferredName": "Aortic valve structure",
      "trigger": "within",
      "unit": "cm2",
      "rangeBegin": "3.0",
      "rangeEnd": "4.0",
      "type": "ConceptValue",
      "begin": 22,
      "end": 52,
      "coveredText": "aortic valve is 3.0 to 4.0 cm2",
      "negated": false,
      "hypothetical": false
    }
]
```

Custom concept values can be passed into the concept value annotation service using a <q>whcs.CustomValue</q> type.
Custom trigger can be passed into the concept value annotation service using a <q>whcs.CustomTrigger</q> type.
