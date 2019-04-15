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

The attribute detection annotator provides support for domain specific attribute values to be discovered in unstructured clinical text. The annotator identify pieces of information pertinent to the domain and are used to create the attribute values by promoting relevant concept, concept values, and clinical annotations such as allergies, cancer, ejection fraction, hypothetical, lab values, living assistance, medications, named entities, negation, procedures, sections, smoking, and symptons & diseases. ACD consumers, through the attribute detection annotator,  can build upon the output of the concept detection, concept value, and  clinical annotators to generate a higher-level <q>concept</q> in which consumers can define the display name, possible values, and value ranges to suit the needs of their solution.
{:shortdesc}

Similar to the <a data-scroll="" href="#concept_detection">Concept detection</a> annotator, the attribute detection annotator may attach the medical codes for applicable concepts , e.g. , NCI, ICD-9, ICD-10, LOINC, MeSH, RxNorm, and SNOMED CT. Attribute detection can detect three additional medical codes, i.e., ccsCode, hccCode, cptCode, in addition to the medical codes available from the concept detection annotator. As of the 2018AA version of the UMLS library, the consumers can elect to have a set of medical codes associated with the umls concepts by specifying the optional configuration parameter to return the medical codes. Notice that not all of these medical codes are applicable to every concept. Applicable codes for a given UMLS concept are based on the vocabulary sources of the surface forms for a given concept.


The attribute detection annotator also supports identification of qualifiers on the discovered attribute values. A qualifier is typically an adjective related to the attribute value. For example, an attribute that identifies a medical condition may have qualifiers related to whether the condition is active or whether it is part of the patient's prior history.

To detect attributes and attribute qualifiers , the consumer must first define the attribute and its metadata, include the attribute in an attribute set, and optionally define possible values and qualifiers for the attribute. After an attribute or qualifier set has been defined, it is specified as an API query parameter and then used during request processing to detect attribute values and qualifiers in pre-annotated unstructured text. To simplify the attribute definition process, ACD provides several predefined attributes set.



The consumer may also use the [Domain Expert Tool](http://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/) (DET) to easily construct other attributes, attribute sets, qualifiers, and qualifier sets for their specific domain. Once the attribute definition process is complete in DET, the artifacts and attribute detection annotator configuration (defined in the profile flow, see <a data-scroll="" href="#profiles">Profiles</a> section) can be exported from DET via a cartridge and then deployed to ACD for use by this consumer.

#### Predefined Attribute Sets

ACD provides three predefined attribute sets for evaluation purposes. The attribute sets are provided through two predefined profiles, the general_medical_v1.0 profile and the general_cancer_v1.0 profile. See the <a data-scroll="" href="#profiles">Profiles</a> section for more details on the profiles.

If the attribute detection annotator is included in a flow without explicitly designating any attribute_set parameters, then the general_medical_v1.0 and general_labs_v1.0 attribute sets are used by default.<br/>

<table>
<caption>Provided Attribute Sets</caption>
<tr>
<th>Attribute Set</th>
<th>Description</th>
</tr>
<tbody>
<tr>
<td>general_medical_v1.0</td>
<td>Clinical attributes that represent the patient characteristics commonly used by physicians during a medical examination including demographics, symptoms, diseases, and procedures. Included in the general_medical_v1.0 profile.</td>
</tr>
<tr>
<td>general_labs_v1.0</td>
<td>Clinical attributes that represent the laboratory measurements commonly used by physicians. Included in the general_medical_v1.0 profile.</td>
</tr>
<tr>
<td>general_cancer_v1.0</td>
<td>Clinical Attributes that focus on cancer patient disease characteristics including the cancer type, disease progression, staging, tumor markers, and treatments. Included in the general_cancer_v1.0 profile.</td>
</tr>
</tbody>
</table>

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
<tr>
<th>Configuration</th>
<th>Description</th>
</tr>
<tr>
<td>attribute_set</td>
<td>The name of the desired attribute set to leverage when running the attribute_detection annotator. Multiple attribute sets can be designated for a given request. </td>
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





<h4>Dependencies</h4>

The attribute_detection annotator detects attributes from previously detected concepts and concept values. Configurations defined within the attribute sets determine which concepts and concept values to <q>promote</q> to attributes. The concept_value annotator is needed as a dependency to associate values from the unstructured text with a detected attribute. The attribute_detection annotator does not detect any explicit concepts from the unstructured data itself.

###### Sample Annotator Flow for Attribute Detection

Sample request for running the attribute detection annotator, leveraging the **General Medical V1.0 Profile**.

```javascript
{
  "unstructured": [
    {
      "text": "Patient has an atypical carcinoid lung tumor."
    }
  ],
  "annotatorFlows": [
    {
	"profile" : "general_medical_v1.0",
      "flow": {
        "elements": [
          {
            "annotator": {
                "name":"concept_detection"
             }
          },
          {
            "annotator": {
                "name":"concept_value"
             }
          },
          {
            "annotator": {
                "name":"attribute_detection"
             }
          }
        ],
        "async":"false"
       }
    }
  ]
}
```

##### Contextual Annotator Flow Sequence Recommendation

If negation, hypothetical, disambiguation, or section annotators are included within the annotator flow alongside attribute_detection, it is recommended that those annotators be designated to run prior to attribute_detection. This flow is recommended for the following reasons:

1.  If you choose to have negated, hypothetical, or contextually invalid concepts removed, we recommend these annotations be removed prior to running attribute_detection, to avoid detection of an attribute based on concepts that will end up being truncated from the response.
2.  The attribute_detection annotator will propagate contextual information from the underlying concepts and concept values to the discovered attribute. For example :
    <br/>**2.1 Negated** - if the attribute is detected as a boolean (where value would be set to _true_), the boolean value is flipped to _false_ if negated. Otherwise, the negated flags are propagated within the attribute annotation.
    <br/>**2.2 Hypothetical** - the hypothetical boolean field is propagated within the attribute annotation.
    <br/>**2.3 sectionSurfaceForm and sectionNormalizedName** - the section features are propagated within the attribute annotation.

<h4> Sample Attribute with Qualifier Detection Annotation</h4>

The _carcinoid lung tumor_ concept detected in the clinical text within the sample request above is rolled up into a higher-level _Disease_ attribute. In this example, _atypical_ is detected as an attribute qualifier.

```javascript
"attributeValues": [
  {
    "preferredName": "Carcinoid tumor of lung",
    "values": [
      {
        "value": "true"
      }
    ],
    “qualifiers”: [
      {
        “value”: “true”,
        “qualifier”: “atypical”,
        “begin”: 15,
        “end”: 23
      }
    ],
    "source": "General Medical",
    "sourceVersion": "v1.0",
    "concept": {
      "uid": 2
    },
    "begin": 24,
    "end": 44,
    "coveredText": "carcinoid lung tumor",
    "name": "Disease"
  }
]
```

<h4>Response Fields</h4>

<table>
<caption>Response Fields</caption>
<tr>
<th>Fields</th>
<th>Description</th>
</tr>
<tr>
<td>preferredName</td>
<td>The preferredName of the underlying medical concept promoted to an attribute.</td>
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
<td>Reference to the medical concept promoted to an attribute.</td>
</tr>
<tr>
<td>conceptValue</td>
<td>Reference to the medical concept value promoted to an attribute.</td>
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
<tr>
<td>name</td>
<td>The configured name of the detected attribute.</td>
</tr>
</table>
