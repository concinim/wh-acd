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

<h4>Dependencies</h4>

The concept_value annotator detects values from unstructured clinical text and associates them with previously detected concepts from the concept_detection annotator. Thus concept_detection must run prior to concept_value within an annotator flow to function properly.

<h4>Annotation Types</h4>

* ConceptValue

<h4>Response Fields</h4>

<table>
<caption>Response Fields</caption>
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

##### Example 2: Greater than or equal to Concept Value with units and natural language expression of value - _<q>twenty</q>_

> **Text:** _<q>The patient must have a **platelet count of at least twenty L.**</q>_

This example illustrates the capability within concept value to detect and normalize numeric values articulated in natural language from unstructured data. Concept value is able to normalize the value <q>20</q> from the text <q>twenty</q>.

```javascript
"conceptValues": [
  {
    "cui": "C1287267",
    "dimension": "volume",
    "preferredName": "Finding of platelet count",
    "trigger": "greater than or equal to",
    "unit": "L.",
    "value": "20",
    "type": "ConceptValue",
    "begin": 24,
    "end": 57,
    "coveredText": "platelet count of at least twenty L."
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

> **Text:** _<q>The area of a typical **aortic valve is 3.0 to 4.0 cm2**.</q>_

This example demonstrates a set of range values. The trigger **within** indicates that a ConceptValue annotation encompasses a set of range values.

```javascript
"conceptValues": [
  {
    "cui": "C1269005",
    "dimension": "area",
    "preferredName": "Entire aortic valve",
    "trigger": "within",
    "unit": "cm2",
    "rangeBegin": "3.0",
    "rangeEnd": "4.0",
    "type": "ConceptValue",
    "begin": 22,
    "end": 52,
    "coveredText": "aortic valve is 3.0 to 4.0 cm2"
  }
]
```

Custom concept values can be passed into the concept value annotation service using a <q>whcs.CustomValue</q> type.
Custom trigger can be passed into the concept value annotation service using a <q>whcs.CustomTrigger</q> type.

##### Example 5: ConceptValue with a range value set

This example demonstrates a custom concept values. The trigger **equal sign** indicates that a ConceptValue annotation encompasses a monetary value starting from the euro sign.

```javascript
{
  "unstructured": [
    {
      "text": "The measurements showed creatinine = €226.15",
      "data": {
        "concepts": [
 		{
            "begin": 37,
            "end": 44,
            "type": "whcs.CustomValue",
            "coveredText": "€226.15",
            "units":"€",
            "value":"226.15",
            "dimension":"monetary"
          },
          {
            "type": "com.ibm.watson.hutt.umls.OrganicChemical",
            "begin": 24,
            "end": 34,
            "coveredText": "creatinine",
            "componentId": "ConceptDetection/UMLS",
            "confidence": 1,
            "cui": "C0010294",
            "preferredName": "Creatinine",
            "semanticType": "orch",
            "source": "umls"
          }
        ]
      }
    }
  ]
}
```

##### Example 6: ConceptValue with a custom date value

This example demonstrates a custom concept values. The trigger **equal sign** indicates that a ConceptValue annotation encompasses a custom date string value .

```javascript
{
  "unstructured": [
    {
      "text": "The measurements showed creatinine = 3/8/2013.",
      "data": {
        "concepts": [
 		{
            "begin": 37,
            "end": 45,
            "type": "whcs.CustomValue",
            "coveredText": "3/8/2013",
            "dimension": "time"
          },
          {
            "type": "com.ibm.watson.hutt.umls.OrganicChemical",
            "begin": 24,
            "end": 34,
            "coveredText": "creatinine",
            "componentId": "ConceptDetection/UMLS",
            "confidence": 1,
            "cui": "C0010294",
            "preferredName": "Creatinine",
            "semanticType": "orch",
            "source": "umls"
          }
        ]
      }
    }
  ]
}
```

#### Example 7: ConceptValue with a custom trigger and a custom value

This example demonstrates the use of both custom concept values and custom trigger. The custom value is specified to be of type <q>whcs.CustomValue</q> and have a value of **20** . The custom trigger is specified to be of type <q>whcs.CustomComparison</q>. The converedText is not specified and is determined directly from the begin and end annotation. The comparison string is set to be **greater than**.

> **Text:** _<q>History of smoking beyond 20 packs per year</q>_

```javascript
{
  "unstructured": [
    {
      "text": "History of smoking beyond 20 packs per year",
 "data": {
        "concepts": [
          {
            "begin": 26,
            "end": 43,
            "type":"whcs.CustomValue",
            "coveredText": "20 packs per year",
            "units":"packs",
            "value":"20",
            "dimension":"quantity"
           },
          {
            "begin":19,
            "end":25,
            "type":"whcs.CustomComparison",
            "comparison":<q>greater than</q>
          }
         ]
      }
    }
  ]
}
```

#### Example 8: ConceptValue with a custom trigger and a custom value

This example demonstrates the use of both custom concept values and custom trigger. The custom value is specified to be of type <q>whcs.CustomValue</q> and have a value of **1x2x3** . The custom trigger is specified to be of type <q>whcs.CustomComparison</q>. The converedText is not specified and is determined directly from the begin and end annotation. The comparison string is set to be **smaller than**.

> **Text:** _<q>Tumor size smaller than 1 x 2 x 3 cm3.</q>_

```javascript
{
"unstructured": [
{
 "text": "Tumor size smaller than 1 x 2 x 3 cm3.",
      "data": {
	    "concepts": [
	         {
            "begin": 19,
            "end": 37,
            "type": "whcs.CustomValue",
            "coveredText": "1 x 2 x 3 cm3",
            "units":"cm3",
            "value": "1 x 2 x 3",
            "dimension":"quantity"
            },
			     {
            "begin": 11,
            "end": 18,
            "type": "whcs.CustomComparison",
            "comparison": "smaller than"
          }
         ]
      }
    }
  ]
}
```
