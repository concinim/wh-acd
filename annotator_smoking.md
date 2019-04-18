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

Smoking Indicator annotator identifies whether the patient is or was a smoker. Furthermore, it identifies the amount and substance(s) being smoked as well as the rate and duration of the smoking habit.
{:shortdesc}

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
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
<td>Defines the version of the UMLS library that is used when annotating unstructured data.  The value <q>umls.latest</q> is used to indicate the latest version of the available UMLS libraries (2018AA).  It is also the default value for the <b>library</b> configuration.</td>
</tr>
</table>

<h4>Annotation Types</h4>

* aci.SmokingInd

###### aci.SmokingInd

<table>
<caption>aci.SmokingInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.SmokingInd</td></tr>
<tr><td>amount</td><td>Contains the amount of the smoking substance.  For example, one pack, 2 to 3 packs, etc.  If the smoking amount information is not specified in the text, then the feature will not be created.</td></tr>
<tr><td>current</td><td>Indicates whether the patient is a current smoker.  The values of this feature are true or false. True indicates that the patient is a current smoker. False indicates that the patient has history of smoking and is not presently smoking.</td></tr>
<tr><td>duration</td><td>Indicates how long the patient has been smoking.  For example, <q>for 10 years</q>.</td></tr>
<tr><td>modality</td><td>Determines the likeliness of the annotation. Modality for the text <q>smokes daily</q> is <q>positive</q> while the modality for the text <q>never smoked</q> is <q>negative</q>.</td></tr>
<tr><td>participation</td><td>Indicates the participant that is related to annotation.  For instance, when a SmokingInd annotation is identified, the participation feature indicates whether the SmokingInd is related to a patient, surroundings, or a family member of the patient.  The three possible values are <q>patient</q>, <q>environmental</q>, and <q>family</q>.</td></tr>
<tr><td>rate</td><td>Indicates the rate at which the patient smokes.  For example, in the text <q>smokes 1 pack a week</q>, the rate value will be <q>a week</q>.</td></tr>
<tr><td>sectionSurfaceForm</td><td>Medical documents have many sections such as patient's information, previous medical history, family history, etc.  The covered text that identifies which section of the document that spans the annotation. The default value of this feature is <q>document</q>.</td></tr>
<tr><td>sectionNormalizedName</td><td>The normalized term for the section.</td></tr>
<tr><td>smokeTermSurfaceForm</td><td>The covered text that indicates the action for the smoking activity. For example, in text <q>He smokes 2 packs a day</q>, the smoke term  is <q>smokes</q>.</td></tr>
<tr><td>smokeTermNormalizedName</td><td>The normalized term for the smoke term.</td></tr>
<tr><td>smokeSubstanceSurfaceForm</td><td>The covered text that refers to the substance being smoked. For example, in text <q>He smokes 2 packs cigarettes a day</q>, the smoke substance is <q>cigarettes</q>.</td></tr>
<tr><td>smokeSubstanceNormalizedName</td><td>The normalized term for the smoke substance.</td></tr>
<tr><td>illicitDrugSurfaceForm</td><td>The covered text that refers to the substance being smoked if it is an illicit drug.</td></tr>
<tr><td>illicitDrugNormalizedName</td><td>The normalized term for the illicit drug substance.</td></tr></table>
