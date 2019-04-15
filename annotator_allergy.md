---

copyright:
  years: 2015, 2018
lastupdated: "2019-04-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:generic: .ph data-hd-programlang='generic'}
{:curl: .ph data-hd-programlang='curl'}
{:go: .ph data-hd-programlang='go'}
{:java: .ph data-hd-programlang='java'}
{:node: .ph data-hd-programlang='node'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:middle: .ph data-hd-position='middle'}
{:right: .ph data-hd-position='right'}
{:here: .ph data-hd-vposition='here'}

# Allergies
{: #annotator_allergies}

<h3 id="allergy">Allergies</h3>

Detects text that follows allergy keywords such as <q>allergies:</q> and <q>allergic to:</q>. Items following the keywords are annotated with the AllergyInd type. The annotation includes all types of allergies such as environmental, animal, medication, food, etc. If annotation includes a medication then information related to the medication is also returned.

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
<tr>
<th>Configuration</th><th>Values</th><th>Description</th>
</tr>
</tbody>
<tr>
<td>
library
</td>
<td>
<ul>
  <li>umls.2016AA <i>(deprecated - will be removed in 2019)</i></li>
  <li>umls.2017AA</li>
  <li>umls.2018AA</li>
  <li>umls.latest</li>
</ul>
</td>
<td>
Defines the version of the UMLS library that is used when annotating unstructured data.  The value <q>umls.latest</q> is used to indicate the latest version of the available UMLS libraries (2018AA).  It is also the default value for the <b>library</b> configuration.
</td>
</tr>
</tbody>
</table>

<h4>Annotation Types</h4>

* aci.AllergyMedicationInd
* aci.AllergyInd

###### aci.AllergyInd

<table>
<caption>aci.AllergyInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.AllergyInd</td></tr>
</table>

---

###### aci.AllergyMedicationInd

<table>
<caption>aci.AllergyMedicationInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.AllergyMedicationInd</td></tr>
<tr><td>medication</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
  <tr><td>type</td><td>aci.MedicationInd</td></tr>
  <tr><td>sectionSurfaceForm</td><td>Medical documents have many sections such as patient's information, previous medical history, family history, etc.  The covered text that identifies which section of the document that spans the annotation. The default value of this feature is <q>document</q>.</td></tr>
  <tr><td>sectionNormalizedName</td><td>The normalized term for the section.</td></tr>
  <tr><td>date</td><td>Indicates the date that is related to the event.  For instance, in a patient's medical form, this date may indicate the date of surgery, or the date of last diagnosis.  The value of date is detected from the date that is nearest to the text that is annotated.</td></tr>
  <tr><td>dateInMilliseconds</td><td>It is a java.util.Calendar date and is the difference, measured in milliseconds, between the date of the event and midnight, January 1, 1970 UTC.</td></tr>
  <tr><td>dateSource</td><td>Indicates where in the document or text the date value is identified. For example, <q>sentence</q> is one possible option for dateSource.</td></tr>
  <tr><td>administration</td><td><table role="presentation"><tbody>
    <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
    <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
    <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
    <tr><td>type</td><td>aci.SubstanceAdministration</td></tr>
    <tr><td>dosageValue</td><td>The text that represents out often the medication is administered.</td></tr>
    <tr><td>frequencyValue</td><td>The text that represents the dosage of the medication.</td></tr>
    <tr><td>route</td><td><table role="presentation"><tbody>
      <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
      <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
      <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
      <tr><td>type</td><td>aci.DrugRoute</td></tr>
      <tr><td>normalized</td><td>The normalized term that represents the route.</td></tr>
      </tbody></table></td></tr>
    <tr><td>duration</td><td><table role="presentation"><tbody>
      <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
      <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
      <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
      <tr><td>type</td><td>aci.Duration</td></tr>
      </tbody></table></td></tr>
  </tbody></table></td></tr>
  <tr><td>drug</td><td><table role="presentation"><tbody>
    <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
    <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
    <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
    <tr><td>type</td><td>aci.Ind_Drug</td></tr>
    <tr><td>complex</td><td>Whether this a multi-drug medication.</td></tr>
    <tr><td>name1</td><td><table role="presentation"><tbody>
      <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
      <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
      <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
      <tr><td>type</td><td>aci.DrugName</td></tr>
      <tr><td>cui</td><td>UMLS Concept Unique ID (CUI). CUIs are used to uniquely identify concepts across different UMLS sources. Depending on the source of the medication information, this value may not be available.</td></tr>
      <tr><td>rxNormID</td><td>Also called the RXCUI which is a normalized id that is defined in the RxNorm standard and commonly used amongst different organizations. Depending on the source of the medication information, this value may not be available.</td></tr>
      <tr><td>drugSurfaceForm</td><td>The covered text that refers to the drug identified by the annotation.</td></tr>
      <tr><td>drugNormalizedName</td><td>The normalized term for the drug.</td></tr>
      </tbody></table></td></tr>
  </tbody></table></td></tr>
</tbody></table></td></tr>
</table>
