<h3 id="living_assistance">Living Assistance</h3>

#### Bathing Assistance

This daily living activities annotator identifies text that indicates whether a patient needs any type of assistance while bathing or taking shower. Additionally, the annotator will also identify patients who potentially needing help if the text mentions patient is having difficulty with a specific bathing task such as needing help washing feet.

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

* aci.BathingAssistanceInd

###### aci.BathingAssistanceInd

<table>
<caption>aci.BathingAssistanceInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.BathingAssistanceInd</td></tr>
<tr><td>modality</td><td>Potenial values are: <q>fully dependent</q>, <q>semi dependent</q>, and <q>independent</q>.  If help is required or an assistance device is used with the activity then the modality will be <q>fully dependent</q>.  If help may or may not required with the activity the modality will be <q>semi dependent</q>.  If it can be determined that no help is required with the activity then the modality will be <q>independent</q>.</td></tr>
<tr><td>actionImplementSurfaceForm</td><td>The covered text that refers to objects that are associated with the secondary actions.  For example, in the text <q>He needs help cleaning his feet.</q>, the action implement is <q>feet</q>.</td></tr>
<tr><td>actionImplementNormalizedName</td><td>The normalized term for the action implement.</td></tr>
<tr><td>assistanceDeviceSurfaceForm</td><td>The covered text that refers to devices that provide assistance during the activity.  For example, in the text <q>He does not need a bath seat.</q>, the assistance device is <q>bath seat</q>.</td></tr>
<tr><td>assistanceDeviceNormalizedName</td><td>The normalized term for the assistance device.</td></tr>
<tr><td>primaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with primary functions related to an activity. For example, in the text <q>He washes his back with difficulty.</q>, the primary action is <q>washes</q>.</td></tr>
<tr><td>primaryActionNormalizedName</td><td>The normalized term for the primary action.</td></tr>
<tr><td>secondaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with actions that are related to the primary activity or an action associated with an implement.   For example, in the text <q>He needs help cleaning his feet.</q>, the secondary action is <q>cleaning</q>.</td></tr>
<tr><td>secondaryActionNormalizedName</td><td>The normalized term for the secondary action.</td></tr>
</table>

---

#### Dressing Assistance

This daily living activities annotator identifies text that indicates whether a patient needs any type of assistance while dressing.

<h4>Configrations</h4>

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
<td>Defines the version of the UMLS library that is used when annotating unstructured data.  The value <q>umls.latest</q> is used to indicate the latest version of the available UMLS libraries (2018AA).  It is also the default value for the <b>library</b> configuration.
</td>
</tr>
</table>

<h4>Annotation Types</h4>

* aci.DressingAssistanceInd

###### aci.DressingAssistanceInd

<table>
<caption>aci.DressingAssistanceInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.DressingAssistanceInd</td></tr>
<tr><td>modality</td><td>Potenial values are: <q>fully dependent</q>, <q>semi dependent</q>, and <q>independent</q>.  If help is required or an assistance device is used with the activity then the modality will be <q>fully dependent</q>.  If help may or may not required with the activity the modality will be <q>semi dependent</q>.  If it can be determined that no help is required with the activity then the modality will be <q>independent</q>.</td></tr>
<tr><td>actionImplementSurfaceForm</td><td>The covered text that refers to objects that are associated with the secondary actions.  For example, in the text <q>She is not able to put on her clothes.</q>, the action implement is <q>clothes</q>.</td></tr>
<tr><td>actionImplementNormalizedName</td><td>The normalized term for the action implement.</td></tr>
<tr><td>assistanceDeviceSurfaceForm</td><td>The covered text that refers to devices that provide assistance during the activity.  For example, in the text <q>He uses a shoe horn to put on his shoe.</q>, the assistance device is <q>shoe horn</q>.</td></tr>
<tr><td>assistanceDeviceNormalizedName</td><td>The normalized term for the assistance device.</td></tr>
<tr><td>primaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with primary functions related to an activity. For example, in the text <q>She needs help dressing.</q>, the primary action is <q>dressing</q>.</td></tr>
<tr><td>primaryActionNormalizedName</td><td>The normalized term for the primary action.</td></tr>
<tr><td>secondaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with actions that are related to the primary activity or an action associated with an implement.   For example, in the text <q>She is not able to put on her clothes.</q>, the secondary action is <q>put on</q>.</td></tr>
<tr><td>secondaryActionNormalizedName</td><td>The normalized term for the secondary action.</td></tr>
</table>

---

#### Eating Assistance

This daily living activities annotator identifies text that indicates whether a patient needs any type of assistance consuming food. This will include any type of food consumption such as eating, drinking, chewing, swallowing, etc. Furthermore, the annotator will also identify difficulty using utensils as potentially needing help with eating such as <q>difficulty holding a fork and a knife</q>.

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

* aci.EatingAssistanceInd

###### aci.EatingAssistanceInd

<table>
<caption>aci.EatingAssistanceInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.EatingAssistanceInd</td></tr>
<tr><td>modality</td><td>Potenial values are: <q>fully dependent</q>, <q>semi dependent</q>, and <q>independent</q>.  If help is required or an assistance device is used with the activity then the modality will be <q>fully dependent</q>.  If help may or may not required with the activity the modality will be <q>semi dependent</q>.  If it can be determined that no help is required with the activity then the modality will be <q>independent</q>.</td></tr>
<tr><td>actionImplementSurfaceForm</td><td>The covered text that refers to objects that are associated with the secondary actions.  For example, in the text <q>He uses a small cup with difficulty.</q>, the action implement is <q>cup</q>.</td></tr>
<tr><td>actionImplementNormalizedName</td><td>The normalized term for the action implement.</td></tr>
<tr><td>assistanceDeviceSurfaceForm</td><td>The covered text that refers to devices that provide assistance during the activity. For example, in the text <q>He uses a cup holder to drink.</q>, the assistance device is <q>cup holder</q>. </td></tr>
<tr><td>assistanceDeviceNormalizedName</td><td>The normalized term for the assistance device.</td></tr>
<tr><td>primaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with primary functions related to an activity. For example, in the text <q>He needs help eating.</q>, the primary action is <q>eating</q>.</td></tr>
<tr><td>primaryActionNormalizedName</td><td>The normalized term for the primary action.</td></tr>
<tr><td>secondaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with actions that are related to the primary activity or an action associated with an implement.   For example, in the text <q>He uses a small cup with difficulty.</q>, the secondary action is <q>uses</q>.</td></tr>
<tr><td>secondaryActionNormalizedName</td><td>The normalized term for the secondary action.</td></tr>
</table>

---

#### Seeing Assistance

This daily living activities annotator identifies text that indicates whether a patient has difficulty seeing. However, this annotator will not identify text if the patient uses assistive devices such as eye glasses or contact lenses to see properly.

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

* aci.SeeingAssistanceInd

###### aci.SeeingAssistanceInd

<table><caption>aci.SeeingAssistanceInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.SeeingAssistanceInd</td></tr>
<tr><td>modality</td><td>Potenial values are: <q>fully dependent</q>, <q>semi dependent</q>, and <q>independent</q>.  If help is required or an assistance device is used with the activity then the modality will be <q>fully dependent</q>.  If help may or may not required with the activity the modality will be <q>semi dependent</q>.  If it can be determined that no help is required with the activity then the modality will be <q>independent</q>.</td></tr>
<tr><td>actionImplementSurfaceForm</td><td>The covered text that refers to objects that are associated with the secondary actions.  For example, in the text <q>He opens his eyes with difficulty.</q>, the action implement is <q>eyes</q>.</td></tr>
<tr><td>actionImplementNormalizedName</td><td>The normalized term for the action implement.</td></tr>
<tr><td>assistanceDeviceSurfaceForm</td><td>The covered text that refers to devices that provide assistance during the activity. For example, in the text <q>He uses a screen reader.</q>, the assistance device is <q>reader</q>. </td></tr>
<tr><td>assistanceDeviceNormalizedName</td><td>The normalized term for the assistance device.</td></tr>
<tr><td>primaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with primary functions related to an activity. For example, in the text <q>He needs help seeing.</q>, the primary action is <q>seeing</q>.</td></tr>
<tr><td>primaryActionNormalizedName</td><td>The normalized term for the primary action.</td></tr>
<tr><td>secondaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with actions that are related to the primary activity or an action associated with an implement.   For example, in the text <q>He opens his eyes with difficulty.</q>, the secondary action is <q>opens</q>.</td></tr>
<tr><td>secondaryActionNormalizedName</td><td>The normalized term for the secondary action.</td></tr>
</table>

---

#### Toileting Assistance

This daily living activities annotator identifies text that indicates whether a patient needs any type of assistance in using toileting facilities. Note that the annotator will not identify needing help with activities that are done before or after the toileting activities such as walking to the bathroom or washing hands.

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

* aci.ToiletingAssistanceInd

###### aci.ToiletingAssistanceInd

<table>
<caption>aci.ToiletingAssistanceInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.ToiletingAssistanceInd</td></tr>
<tr><td>modality</td><td>Potenial values are: <q>fully dependent</q>, <q>semi dependent</q>, and <q>independent</q>.  If help is required or an assistance device is used with the activity then the modality will be <q>fully dependent</q>.  If help may or may not required with the activity the modality will be <q>semi dependent</q>.  If it can be determined that no help is required with the activity then the modality will be <q>independent</q>.</td></tr>
<tr><td>actionImplementSurfaceForm</td><td>The covered text that refers to objects that are associated with the secondary actions.  For example, in the text <q>He needs help help raising the toilet seat.</q>, the action implement is <q>toilet seat</q>.</td></tr>
<tr><td>actionImplementNormalizedName</td><td>The normalized term for the action implement.</td></tr>
<tr><td>assistanceDeviceSurfaceForm</td><td>The covered text that refers to devices that provide assistance during the activity. For example, in the text <q>He needs a bedpan.</q>, the assistance device is <q>bedpan</q>. </td></tr>
<tr><td>assistanceDeviceNormalizedName</td><td>The normalized term for the assistance device.</td></tr>
<tr><td>primaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with primary functions related to an activity. For example, in the text <q>He needs help using the bathroom.</q>, the primary action is <q>using the bathroom</q>.</td></tr>
<tr><td>primaryActionNormalizedName</td><td>The normalized term for the primary action.</td></tr>
<tr><td>secondaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with actions that are related to the primary activity or an action associated with an implement.   For example, in the text <q>He needs help help raising the toilet seat.</q>, the secondary action is <q>raising</q>.</td></tr>
<tr><td>secondaryActionNormalizedName</td><td>The normalized term for the secondary action.</td></tr>
</table>

---

#### Walking Assistance

This daily living activities annotator identifies text that indicates whether a patient needs any type of assistance while walking. The annotator will also identify text where patient may potentially need assistance walking such as when patient is unable to move a leg or bend a knee.

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
<tr>
<th>Configuration</t>
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

* aci.WalkingAssistance

###### aci.walkingAssistance

<table>
<caption>aci.walkingAssistance</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.walkingAssistanceInd</td></tr>
<tr><td>modality</td><td>Potenial values are: <q>fully dependent</q>, <q>semi dependent</q>, and <q>independent</q>.  If help is required or an assistance device is used with the activity then the modality will be <q>fully dependent</q>.  If help may or may not required with the activity the modality will be <q>semi dependent</q>.  If it can be determined that no help is required with the activity then the modality will be <q>independent</q>.</td></tr>
<tr><td>actionImplementSurfaceForm</td><td>The covered text that refers to objects that are associated with the secondary actions.  For example, in the text <q>He can't move his legs.</q>, the action implement is <q>legs</q>.</td></tr>
<tr><td>actionImplementNormalizedName</td><td>The normalized term for the action implement.</td></tr>
<tr><td>assistanceDeviceSurfaceForm</td><td>The covered text that refers to devices that provide assistance during the activity. For example, in the text <q>He can't walk without a cane.</q>, the assistance device is <q>cane</q>. </td></tr>
<tr><td>assistanceDeviceNormalizedName</td><td>The normalized term for the assistance device.</td></tr>
<tr><td>primaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with primary functions related to an activity. For example, in the text <q>He can't really walk.</q>, the primary action is <q>walk</q>.</td></tr>
<tr><td>primaryActionNormalizedName</td><td>The normalized term for the primary action.</td></tr>
<tr><td>secondaryActionSurfaceForm</td><td>The covered text that refers to the terms associated with actions that are related to the primary activity or an action associated with an implement.   For example, in the text <q>He can't move his legs.</q>, the secondary action is <q>move</q>.</td></tr>
<tr><td>secondaryActionNormalizedName</td><td>The normalized term for the secondary action.</td></tr>
</table>
