<h3 id="symptom_disease">Symptoms & Diseases</h3>

This annotator identifies symptoms and diseases mentioned in the text. It also identifies related text that describes the symptom or disease.


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
  <li>umls.2016AA <i>(deprecated - will be removed in 2019)</i></li>
  <li>umls.2017AA</li>
  <li>umls.2018AA</li>
  <li>umls.latest</li>
</ul>
</td>
<td>Defines the version of the UMLS library that is used when annotating unstructured data.  The value <q>umls.latest</q> is used to indicate the latest version of the available UMLS libraries (2018AA).  It is also the default value for the <b>library</b> configuration.</td>
</tr>
</table>

<h4>Annotation Types</h4>

* aci.SymptomDiseaseInd

###### aci.SymptomDiseaseInd

<table>
<caption>aci.SymptomDiseaseInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.SymptomDiseaseInd</td></tr>
<tr><td>date</td><td>Indicates the date that is related to the event.  For instance, in a patient's medical form, this date may indicate the date of surgery, or the date of last diagnosis.  The value of date is detected from the date that is nearest to the text that is annotated.</td></tr>
<tr><td>dateInMilliseconds</td><td>It is a java.util.Calendar date and is the difference, measured in milliseconds, between the date of the event and midnight, January 1, 1970 UTC.</td></tr>
<tr><td>dateSource</td><td>Indicates where in the document or text the date value is identified. For example, <q>sentence</q> is one possible option for dateSource</td></tr>
<tr><td>snomedConceptId</td><td>Numerical code provided by the SNOMED dictionaries that represents the symptom or disease.</td></tr>
<tr><td>ccsCode</td><td>CCS stands for Clinical Classification System, used to categorize the  symptom and diseases such that it can be used for further analysis.</td></tr>
<tr><td>hccCode</td><td>HCC stands for Hierarchical Condition Categories and primarily used by Medicare and Medicaid.</td></tr>
<tr><td>cui</td><td>UMLS Concept Unique ID (CUI). CUIs are used to uniquely identify concepts across different UMLS sources. Depending on the source of the symptom/disease information, this value may not be available.</td></tr>
<tr><td>modality</td><td>There are three potential values for this feature: positive, negative, and potential.  Positive modality means there is a high probability that the identified text is related to symptoms or disease.  Negative modality presents that the identified is not a symptom or a disease.  Potential modality means there is some likelihood that the identified text is related to symptoms or disease.</td></tr>
<tr><td>icd9Code</td><td>ICD stands for International Classification of Diseases.  The number 9 is a revision number for this code set.</td></tr>
<tr><td>icd10Code</td><td>ICD stands for International Classification of Diseases.  The number 10 is a revision number for this code set.</td></tr>
<tr><td>symptomDiseaseSurfaceForm</td><td>The covered text that refers to the sympton or disease identified by the annotation. For example, in text <q>He had a persistent cough..</q>, the symptom is <q>persistent cough</q>.</td></tr>
<tr><td>symptomDiseaseSurfaceFormNormalizedName</td><td>The normalized term for the sympton or disease. For instance, for the term <q>roll-in shower bench</q>, the normalized form can be <q>shower bench</q>.</td></tr>
<tr><td>sectionSurfaceForm</td><td>Medical documents have many sections such as patient's information, previous medical history, family history, etc.  The covered text that identifies which section of the document that spans the annotation. The default value of this feature is <q>document</q>.</td></tr>
<tr><td>sectionNormalizedName</td><td>The normalized term for the section.</td></tr>
<tr><td>modifiers</td><td>
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
