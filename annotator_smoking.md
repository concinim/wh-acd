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

# Smoking
{: #smoking}

The smoking annotator identifies whether the patient is a current or former smoker. Furthermore, it identifies the amount and substance(s) being smoked as well as the rate and duration of the smoking habit.
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

* aci.SmokingInd

###### aci.SmokingInd

<table>
<tr><th>__Fields__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.SmokingInd</td></tr>
<tr><td>amount</td><td>Contains the amount of the smoking substance specified in the text.  For example, one pack, 2 to 3 packs, etc.</td></tr>
<tr><td>current</td><td>Indicates whether the patient is a current smoker.  The values of this feature are true or false. True indicates that the patient is a current smoker. False indicates that the patient has history of smoking and is not presently smoking.</td></tr>
<tr><td>duration</td><td>Indicates how long the patient has been smoking.  For example, "for 10 years".</td></tr>
<tr><td>modality</td><td>Determines the likeliness of the annotation. Modality for the text "smokes daily" is "positive" while the modality for the text "never smoked" is "negative".</td></tr>
<tr><td>participation</td><td>Indicates the participant that is related to the annotation.  For instance, when a SmokingInd annotation is identified, the participation feature indicates whether the SmokingInd is related to a patient, surroundings, or a family member of the patient.  The three possible values are "patient", "environmental", and "family".</td></tr>
<tr><td>rate</td><td>Indicates the rate at which the patient smokes.  For example, in the text "smokes 1 pack a week", the rate value will be "a week".</td></tr>
<tr><td>sectionSurfaceForm</td><td>Medical documents have many sections such as patient's information, previous medical history, family history, etc.  The covered text that identifies which section of the document that spans the annotation. The default value of this feature is "document".</td></tr>
<tr><td>sectionNormalizedName</td><td>The normalized term for the section.</td></tr>
<tr><td>smokeTermSurfaceForm</td><td>The covered text that indicates the action for the smoking activity. For example, in text "He smokes 2 packs a day", the smoke term  is "smokes".</td></tr>
<tr><td>smokeTermNormalizedName</td><td>The normalized term for the smoke term.</td></tr>
<tr><td>smokeSubstanceSurfaceForm</td><td>The covered text that refers to the substance being smoked. For example, in text "He smokes 2 packs cigarettes a day", the smoke substance is "cigarettes".</td></tr>
<tr><td>smokeSubstanceNormalizedName</td><td>The normalized term for the smoke substance.</td></tr>
<tr><td>illicitDrugSurfaceForm</td><td>The covered text that refers to the substance being smoked if it is an illicit drug.</td></tr>
<tr><td>illicitDrugNormalizedName</td><td>The normalized term for the illicit drug substance.</td></tr></table>

### Sample Response

Sample response from the symptom disease annotator for the text: `The patient smokes 2 packs of cigarettes per week.`

```
{
  "unstructured": [
  {
   "text": "The patient smokes 2 packs of cigarettes per week.",
   "data": {
     "SmokingInd": [
       {
         "type": "aci.SmokingInd",
         "begin": 12,
         "end": 49,
         "coveredText": "smokes 2 packs of cigarettes per week",
         "participation": "patient",
         "amount": "2 packs",
         "current": "true",
         "modality": "positive",
         "rate": "per week",
         "smokeSubstanceSurfaceForm": "cigarettes",
         "smokeTermSurfaceForm": "smokes",
         "smokeTermNormalizedName": "smoke",
         "smokeSubstanceNormalizedName": "cigarettes"
       }
     ]
   }
  }]
}
```
