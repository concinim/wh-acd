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

# Concept Detection
{: #concept_detection}

The concept detection service detects Unified Medical Language System (UMLS) concepts from unstructured data.
As of the 2018AA version of the UMLS library, the consumers can elect to have a set of medical codes associated with the umls concepts by specifying the optional configuration parameter to return the medical codes. Then, the UMLS concept annotations from concept detection will include the applicable medical codes as metadata within the annotations. If a CPT Codes file is referenced in the profile and there is a valid CUI-to-CPT code mapping, the CPT Code value is retuned with the concept detected.
{:shortdesc}

Notice that not all of these medical codes are applicable to every concept. Applicable codes for a given UMLS concept are based on the vocabulary sources of the surface forms for a given concept. A list of applicable medical codes are: NCI, NCI, ICD-9, ICD-10, LOINC, MeSH, RxNorm, and SNOMED CT.


<h4>Available UMLS Libraries</h4>

<table>
<tr><th>__UMLS Version__</th><th>__Semantic Types__</th></tr>
</tr><td>2016AB <i>(deprecated - will be removed in 2019)</i></td><td><a href="content/umls/UMLS_2016AB_2017AA_SemanticTypes.htm" target=>UMLS 2016AB Types</a></td></tr>
<tr><td>2017AA</td><td><a href="content/umls/UMLS_2016AB_2017AA_SemanticTypes.htm" target=>UMLS 2017AA Types</a></td></tr>
<tr><td>2018AA</td><td></td></tr>
</table>



<h4>Sample Request</h4>


````javascript
{
  "annotatorFlows": [
    {
      "flow": {
        "elements": [
          {
            "annotator": {
              "name": "concept_detection",
              "parameters": {
                "longest_span": [
                  "false"
                ],
                "libraries": [
                  "umls.2018AA"
                ]
              }
            }
          }
        ],
        "async": false
      }
    }
  ],
  "unstructured": [
    {
      "text": "Patient has lung cancer, but did not smoke. She may consider chemotherapy as part of a treatment plan."
    }
  ]
}
````

The following table lists parameters of the concept_detection service.

<table>
  <caption>Configurations</caption>
  <tr>
    <th>Configuration</th>
    <th>Values</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>longest_span</td>
    <td>true/false</td>
    <td>When true _(default)_, only the concept with the longest text span will be returned if there are multiple concepts overlapping the same span of text.</td>
  </tr>
  <tr>
    <td>expanded</td>
    <td>true/false</td>
    <td>When true, the concept detection annotator will attempt to expand concept coverage beyond the surface forms explicitly listed in the specified library.  For example - if "broken collarbone" is a surface from for C0159658 (Fracture of clavicle), the expanded option would match textual representations of that concept like "broke my collarbone".  This option is _false_ by default.</td>
  </tr>
  <tr>
    <td>libraries</td>
    <td><ul><li>umls.2016AB <i>(deprecated - will be removed in 2019)</i></li> <li>umls.2017AA</li> <li>umls.2018AA</li> <li>umls.latest</li></ul></td>
    <td>Defines the version of the UMLS library that is used when detecting concepts from unstructured data.  The value <q>umls.latest</q> is used to indicate the latest version of the available UMLS libraries (2018AA).  It is also the default value if <b>libraries</b> is not specified in the configuration.</td>
  </tr>
  <tr>
    <td>include_optional_fields</td>
    <td>medical_codes </br> source_vocabularies </td>
    <td>Optional fields that should also be returned for each concept. If not specified, only the libary's default fields will be returned. </td>
  </tr>
</table>



<h4>Sample Concepts Returned in Response</h4>

```javascript
{
  "cui": "C0242379",
  "preferredName": "Malignant neoplasm of lung",
  "semanticType": "neop",
  "source": "umls",
  "sourceVersion": "2016AB",
  "type": "com.ibm.watson.hutt.umls.NeoplasticProcess",
  "begin": 12,
  "end": 23,
  "coveredText": "lung cancer"
}
```


<table>
<caption>Response Fields</caption>
<tr>
<th>Fields</th>
<th>Description</th>
</tr>
<tr>
<td>cui</td>
<td>UMLS Concept Unique ID (CUI). CUIs are used to uniquely identify concepts across different UMLS sources.</td>
</tr>
</tr>
<tr>
<td>preferredName</td>
<td>Normalized name for the UMLS concept.</td>
</tr>
</tr>
<tr>
<td>semanticType</td>
<td>Shorthand version of the UMLS semantic type.</td>
</tr>
</tr>
<tr>
<td>source</td>
<td>The library source used for the detection of the concepts.</td>
</tr>
</tr>
<tr>
<td>sourceVersion</td>
<td>The version of the library source used for the detection of the concepts.</td>
</tr>
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
</tr>
<tr>
<td>coveredText</td>
<td>The text covered by an annotation as a string.</td>
</tr>
<tr>
<td>cptCode</td>
<td>This code represents the type of procedure that is performed. CPT stands for Current Procedural Terminology. This code a standard terminology used by different members of medical society such as physicians, financial administrators, coders, and other organizations.</td>
</tr>
</table>


The response of the concept detection annotator includes the following fields when the concept annotator is executed with the parameter  "include_optional_fields=medical_codes". Those optional response fields are listed in the following table.

<table>
<tr>
<th>Fields</th>
<th>Description</th>
</tr>
<tr><td>loincId</td><td>LOINC stands for Logical Observations Identifiers, Names, Codes.  The value for this feature comes from UMLS.</td></tr>
<tr><td>NCI Code </td><td> The <a href="https://www.nlm.nih.gov/research/umls/sourcereleasedocs/current/NCI/">NCI Thesaurus</a> covers vocabulary for cancer-related clinical care, translational and basic research, and public information and administrative activities.  The value for this feature comes from UMLS. </td></tr>
<tr><td>snomedConceptId</td><td>Numerical code provided by the SNOMED dictionaries that represents the cancer.</td></tr>
<tr><td>MeSHId </td><td>The <a href="https://www.nlm.nih.gov/research/umls/sourcereleasedocs/current/MSH/">MeSH thesaurus</a> is a controlled vocabulary used for indexing, cataloging, and searching for biomedical and health-related information and documents.  The value for this feature comes from UMLS.</td></tr>
<tr><td>icd9Code</td><td>ICD stands for International Classification of Diseases.  The number 9 is a revision number for this code set.</td></tr>
<tr><td>icd10Code</td><td>ICD stands for International Classification of Diseases.  The number 10 is a revision number for this code set.</td></tr>
<tr><td>rxNormID</td><td>Also called the RXCUI which is a normalized id that is defined in the RxNorm standard and commonly used amongst different organizations.</td></tr>
</table>
