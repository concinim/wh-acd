---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-07"

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

# Attribute Detection
{: #attribute_detection}

The attribute detection annotator provides support for domain specific attribute values to be discovered in unstructured clinical text. The annotator identifies pieces of information pertinent to the domain to create named attributes with associated values. Attribute values are identified by promoting relevant concept, concept values, and clinical annotations such as allergies, cancer, ejection fraction, hypothetical, lab values, living assistance, medications, named entities, negation, procedures, sections, smoking, and symptons & diseases. ACD consumers, through the attribute detection annotator, can build upon the output of the concept detection, concept value, and  clinical annotators to generate a higher-level concept in which consumers can define the display name, possible values, and value ranges to suit the needs of their solution.
{:shortdesc}

Similar to the <a data-scroll="" href="wh-acd?topic=wh-acd-concept_detection#concept_detection">concept detection</a> annotator, the attribute detection annotator may attach the medical codes for applicable concepts , e.g. , NCI, ICD-9, ICD-10, LOINC, MeSH, RxNorm, SNOMED CT, and CPT codes. Attribute detection can also provide two additional medical codes (CCS code and HCC Code) made available by the <a data-scroll="" href="wh-acd?topic=cancer#cancer">cancer</a> and <a data-scroll="" href="wh-acd?topic=wh-acd-symptom_disease#symptom_disease">symptom disease</a> annotators. The consumers can elect to have the set of medical codes associated with the attribute by specifying the optional configuration parameter to return the medical codes.

The attribute detection annotator also supports identification of qualifiers on the discovered attribute values. A qualifier is typically an adjective that describes the attribute. For example, an attribute that identifies a medical condition may have qualifiers related to whether the condition is active or whether it is part of the patient's prior history.

ACD provides several predefined attribute sets that can be used to identify general medical related attributes. The consumer may also use the [Domain Expert Tool](https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/) (DET) to easily construct other attributes and qualifiers for their specific domain. Once the attribute definition process is complete in DET, the attributes and qualifiers can be <a data-scroll="" href="wh-acd?topic=wh-acd-deployed#deployed">deployed</a> to ACD and used with the attribute detection annotator.

#### Predefined Attribute Sets

ACD provides three predefined attribute sets for evaluation purposes.

<table>
<tr>
<th>Attribute Set</th>
<th>Description</th>
</tr>
<tbody>
<tr>
<td>general_medical_v1.0</td>
<td>Clinical attributes that represent the patient characteristics commonly used by physicians during a medical examination including demographics, symptoms, diseases, and procedures. Included in the general_medical_v1.0 and default_profile_v1.0 profiles.</td>
</tr>
<tr>
<td>general_labs_v1.0</td>
<td>Clinical attributes that represent the laboratory measurements commonly used by physicians. Included in the general_medical_v1.0 and default_profile_v1.0 profiles.</td>
</tr>
<tr>
<td>general_cancer_v1.0</td>
<td>Clinical Attributes that focus on cancer patient disease characteristics including the cancer type, disease progression, staging, tumor markers, and treatments. Included in the general_cancer_v1.0 profile.</td>
</tr>
</tbody>
</table>

#### Configurations

<table>
<tr>
<th>Configuration</th>
<th>Description</th>
</tr>
<tr>
<td>attribute_set</td>
<td>The name of the desired attribute set to leverage when running the attribute_detection annotator. Multiple attribute sets can be designated for a given request. </td>
</tr>
<tr>
<td>inference_rules</td>
<td>The name of a derived attribute rule set that will be used for deriving additional attributes based on the attributes discovered by the <b>attribute_set</b> parameter. The derived attribute rules are developed using the <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html" target="_blank">DET</a>.</td>
</tr>
<tr>
<td>qualifier_set</td>
<td>The name of the desired attribute qualifier set to leverage when running the attribute_detection annotator. Multiple qualifier sets can be designated for a given request. The detect_qualifiers parameter must also be set to true.</td>
</tr>
<tr>
<td>detect_qualifiers</td>
<td>When true, attribute annotations will include qualifiers as defined in the qualifier set identified on the qualifier_set parameter.</td>
</tr>
<tr>
<td>include_optional_fields</td>
<td>Specify additional fields from the underlying concepts in the attribute values. Use 'medical_codes' to return medical code fields in the attribute annotations. </td>
</tr>
</table>

#### Dependencies

The attribute_detection annotator detects attributes from previously detected concepts and concept values. Configurations defined within the attribute sets determine which concepts and concept values to promote to attributes. The concept value annotator is needed as a dependency to associate values from the unstructured text with a detected attribute. The attribute detection annotator does not detect any explicit concepts from the unstructured data itself.

The attribute_detection annotator will propagate contextual information from the underlying concepts and concept values to the discovered attribute, such as whether the concept is negated or what section the attribute appears in. The contextual annotators (negation, hypothetical, disambiguation, or section) should be designated to run prior to attribute detection in the flow.

<h4>Annotation Types</h4>

* Attribute Value

###### Attribute Value

<table>
<tr>
<th>Fields</th>
<th>Description</th>
</tr>
<tr>
<td>name</td>
<td>The configured name of the detected attribute.</td>
</tr>
<tr>
<td>preferredName</td>
<td>The normalized or preferred name of the underlying medical concept promoted to the attribute.</td>
</tr>
<tr>
<td>values</td>
<td>Any values associated with the detected attribute. Each value can contain the following information
<ul>
<li> value - the value associated with the attribute</li>
<li> unit - the unit of measure</li>
<li> frequency - the frequency associated with the value</li>
<li> duration - the duration associated with the value</li>
<li> dimension - the dimension associated with the value</li>
<li> modality - the modality associated with the value</li>
</ul>
</td>
</tr>
<tr>
<td>qualifiers</td>
<td>Any qualifiers associated with the detected attribute. Each qualifier can contain the following information:
<ul><li>qualifier - the name of the qualifier</li>
<li>value - the value associated with the qualifier</li>
</ul>
</td>
</tr>
<tr>
<td>source</td>
<td>The attribute configuration set source from which the attribute was detected.</td>
</tr>
<tr>
<td>sourceVersion</td>
<td>The version of the attribute configuration set source from which the attribute was detected.</td>
</tr>
<tr>
<td>concept</td>
<td>Reference to the medical concept related to this attribute.</td>
</tr>
<tr>
<td>conceptValue</td>
<td>Reference to the medical concept value related to this attribute.</td>
</tr>
<tr>
<td>begin </td>
<td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td>
</tr>
<tr>
<td>end</td>
<td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td>
</tr>
<tr>
<td>coveredText</td>
<td>The text covered by an annotation as a string.</td>
</tr>
</table>

### Sample Response

Sample response from the attribute detection annotator for the text: `Study participants must not have an active or untreated brain metastases.`

This example provides example of including optional medical codes and qualifiers.

```javascript
{
  "unstructured": [
    {
      "text": "Study participants must not have an active or untreated brain metastases.",
      "data": {
        "attributeValues": [
          {
            "name": "Disease",
            "preferredName": "Metastatic malignant neoplasm to brain",
            "values": [
              {
                "value": "Disease"
              }
            ],
            "qualifiers": [
              {
                "value": "true",
                "qualifier": "Active",
                "begin": 36,
                "end": 42
              },
              {
                "value": "false",
                "qualifier": "Treated",
                "begin": 46,
                "end": 55
              }
            ],
            "source": "General Medical",
            "sourceVersion": "v1.0",
            "concept": {
              "uid": 2
            },
            "begin": 56,
            "end": 72,
            "coveredText": "brain metastases",
            "negated": true,
            "hypothetical": false,
            "icd10Code": "C79.31",
            "nciCode": "C3813",
            "snomedConceptId": "94225005"
          }
        ]
      }
    }
  ]
}
]
```
