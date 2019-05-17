---

copyright:
  years: 2011, 2019
lastupdated: "2019-04-12"

keywords: annotator clinical data, clinical data, annotation

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

# Symptoms & Diseases
{: #symptom_disease}

This annotator identifies symptoms and diseases mentioned in the text. It also identifies related text that describes the symptom or disease.
{:shortdesc}

<h4>Configurations</h4>

<table>
<tr>
<th>Configuration</th>
<th>Values</th>
<th>Description</th>
</tr>
<tr>
<td>library</td>
<td>
<ul>
  <li>umls.latest</li>
  <li>umls.2018AA</li>
  <li>umls.2017AA</li>
  <li>umls.2016AA <i>(deprecated - will be removed in 2019)</i></li>
</ul>
</td>
<td>Defines the version of the UMLS library that is used when annotating unstructured data.  The value "umls.latest" is used to indicate the latest version of the available UMLS libraries (2018AA).  It is also the default value for the **library** configuration.</td>
</tr>
</table>

<h4>Annotation Types</h4>

* aci.SymptomDiseaseInd

###### aci.SymptomDiseaseInd

<table>
<tr><th>__Fields__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.SymptomDiseaseInd</td></tr>
<tr><td>date</td><td>Indicates the date related to the event.  For instance, in a patient's medical form, this date may indicate the date of surgery, or the date of last diagnosis.  The value of date is detected from the date that is nearest to the text that is annotated.</td></tr>
<tr><td>dateInMilliseconds</td><td>It is a java.util.Calendar date and is the difference, measured in milliseconds, between the date of the event and midnight, January 1, 1970 UTC.</td></tr>
<tr><td>dateSource</td><td>Indicates where in the document or text the date value is identified. For example, "sentence" is one possible option for dateSource</td></tr>
<tr><td>snomedConceptId</td><td>Numerical code provided by the SNOMED dictionaries that represents the symptom or disease.</td></tr>
<tr><td>ccsCode</td><td>Clinical Classification System (CCS) code is used to categorize the symptom and diseases such that it can be used for further analysis.</td></tr>
<tr><td>hccCode</td><td>Hierarchical Condition Categories (HCC) code is primarily used by Medicare and Medicaid.</td></tr>
<tr><td>cui</td><td>UMLS Concept Unique ID (CUI). CUIs are used to uniquely identify concepts across different UMLS sources. Depending on the source of the symptom/disease information, this value may not be available.</td></tr>
<tr><td>modality</td><td>There are three potential values for this feature: positive, negative, and potential.  Positive modality means there is a high probability that the identified text is related to symptoms or diseases.  Negative modality means that the identified text is not a symptom or a disease.  Potential modality means there is some likelihood that the identified text is related to symptoms or diseases.</td></tr>
<tr><td>icd9Code</td><td>ICD stands for International Classification of Diseases.  The number 9 is a revision number for this code set.</td></tr>
<tr><td>icd10Code</td><td>ICD stands for International Classification of Diseases.  The number 10 is a revision number for this code set.</td></tr>
<tr><td>symptomDiseaseSurfaceForm</td><td>The covered text that refers to the sympton or disease identified by the annotation. For example, in text "He had a persistent cough.", the symptom is "persistent cough".</td></tr>
<tr><td>symptomDiseaseSurfaceFormNormalizedName</td><td>The normalized term for the sympton or disease. For instance, for the term "roll-in shower bench", the normalized form can be "shower bench".</td></tr>
<tr><td>sectionSurfaceForm</td><td>Medical documents have many sections such as patient's information, previous medical history, family history, etc.  The covered text that identifies which section of the document that spans the annotation. The default value of this feature is "document".</td></tr>
<tr><td>sectionNormalizedName</td><td>The normalized term for the section.</td></tr>
<tr><td>modifiers</td><td>
  Modifiers represents text that describes the disease or symptom or identifies the related body site or location.
  <table role="presentation"><tbody>
    <tr><td>type</td><td>aci.SiteInd</td></tr>
    <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
    <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
    <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
    <tr><td>type</td><td>aci.Measurement</td></tr>
    <tr><td>gradeValue</td><td>The value of the grade.</td></tr>
    <tr><td>siteNormalizedName</td><td>The normalized name for the site from UMLS.</td></tr>
    <tr><td>compound</td><td>Whether this a multi-site term.</td></tr>
    </tbody></table>
  <table role="presentation"><tbody>
    <tr><td>type</td><td>aci.ModifierGroupInd</td></tr>
    <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
    <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
    <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
    <tr><td>type</td><td>aci.ModifierGroupInd</td></tr>
    </tbody></table>
    </td></tr>
</table>

### Sample Response

Sample response from the symptom disease annotator for the text: `He has severe cramping and pain in his left leg due to diabetic neuropathy.`

```
{
  "unstructured": [
    {
      "text": "He has severe cramping and pain in his left leg due to diabetic neuropathy.",
      "data": {
        "SymptomDiseaseInd": [
          {
            "type": "aci.SymptomDiseaseInd",
            "begin": 7,
            "end": 22,
            "coveredText": "severe cramping",
            "icd9Code": "729.82",
            "icd10Code": "R25.2",
            "modality": "positive",
            "symptomDiseaseSurfaceForm": "cramping",
            "cui": "C0026821",
            "dateInMilliseconds": " ",
            "snomedConceptId": "55300003",
            "modifiers": [
              {
                "coveredText": "severe",
                "end": 13,
                "type": "aci.ModifierGroupInd",
                "begin": 7
              }
            ],
            "ccsCode": "211",
            "symptomDiseaseNormalizedName": "cramp"
          },
          {
            "type": "aci.SymptomDiseaseInd",
            "begin": 27,
            "end": 47,
            "coveredText": "pain in his left leg",
            "modality": "positive",
            "symptomDiseaseSurfaceForm": "pain",
            "dateInMilliseconds": " ",
            "modifiers": [
              {
                "coveredText": "his left leg",
                "end": 47,
                "siteNormalizedName": "structure of left lower leg",
                "type": "aci.SiteInd",
                "snomedConceptId": "48979004",
                "begin": 35,
                "compound": "false"
              }
            ],
            "symptomDiseaseNormalizedName": "pain"
          },
          {
            "type": "aci.SymptomDiseaseInd",
            "begin": 55,
            "end": 74,
            "coveredText": "diabetic neuropathy",
            "icd9Code": "355.9,250.60",
            "icd10Code": "E14.4,G63.2,E11.40",
            "modality": "positive",
            "symptomDiseaseSurfaceForm": "diabetic neuropathy",
            "cui": "C0011882",
            "dateInMilliseconds": " ",
            "snomedConceptId": "230572002",
            "ccsCode": "50",
            "symptomDiseaseNormalizedName": "diabetic neuropathy",
            "hccCode": "18"
          }
        ]
      }
    }
  ]
}
```
