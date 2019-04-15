<h3 id="augmentation">Whitelists</h3>

In addition to filters, whitelists are another configuration option. Whereas filters remove annotations, whitelists provide a way for ACD consumers to supply additional surface forms to annotators in order to detect additional annotations.

The main purpose of whitelists are to create annotations over text that is not currently annotated. As an example, adding the SmokingInd annotation over the text <q>mary jane</q> enables the analysis of an unstructured text <q>The patient uses mary jane on regular basis.</q> Another example, adding a SymptomDiseaseInd annotation over abbreviations of HTN with a normalized name of Hypertension allows the analysis of an unstructured text <q>HTN is a common condition in the United States.</q>

Whitelists that have been predefined and persisted within ACD can be accessed during a _POST /v1/analyze_ request by supplying the whitelist file name associated with the key _dictionaryFileName_ in the configurations whitelist section of the input JSON. For example, suppose you have clinical notes from a region where they refer to colon cancer as _colocer_. This text would obviously not be annotated with any IcaCancerDiagnosisInd annotations. You could create a custom whitelist cancer dictionary with this specific text surface form and save it as, for example, MyCancerWhitelist.dic and persist that config file within ACD. At _POST /v1/analyze_ request time you supply the custom dictionary name, MyCancerWhitelist.dic with the request. A sample JSON for this example follows:

```javascript
{
"annotatorFlows": [
   {
    "flow": {
      "elements": [
         {
          "annotator": {
            "name": "cancer",
            "configurations": [
               {
                "whitelist": {
                  "dictionaryFileName": "MyCancerWhiltelist.dic"
                 }
               }
             ]
           }
         }
       ],
      "async": false
     }
   }
 ],
"unstructured": [
   {
    "text": "The patient was diagnosed with colocer."
   }
 ]
}
```

If a whitelist is not predefined and you wish to add new surface forms to be annotated you can define your whitelist in the configuration section of the request to specify the covered text, which annotation to create, and any features to be associated with the annotation. The following example shows a whitelist definition to produce CustomDrug annotations with features of rxNormID and drugNormalizedName of aspirin for text that contains an incorrect spelling of aspirin. This drug whitelist definition is available for the allergy annotator.

```javascript
{
"annotatorFlows": [
   {
    "flow": {
      "elements": [
         {
          "annotator": {
            "name": "allergy",
            "configurations": [
               {
                "whitelist": {
                  "name": "drug",
                  "entries": [
                     {
                       "surfaceForms": [
                           "asprin"
                        ],
                       "features": {
                           "drugNormalizedName": "aspirin",
                           "rxNormID": "1191"
                        }
                     }
                   ]
                 }
               }
             ]
           }
         }
       ],
      "async": false
     }
   }
 ],
"unstructured": [
   {
    "text": "The patient takes asprin for allergy symptons."
   }
 ]
}
```

The Whitelist definition is composed of surface forms and a list of feature names. The surface form is required but the list of feature names are optional. Existing feature names for each whitelist dictionary are listed in the following table. As an example, the <q>drug</q> whitelist dictionary has two feature names, i.e., rxNormID and drugNormalizedName.

<table>
<caption>Whitelist definition</caption>
<tbody>
 <tr><th>__Whitelist__ __Dictionary__</th><th>__Information__</th></tr>
 <tr><td>actionImplement</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new area of the body requiring the assisted action, or to add new phrases, acronyms, or abbreviations for existing areas of the body that are already covered in the base dictionary.</td></tr>
    <tr><td>__Annotators:__ BathingAssistance, DressingAssistance, EatingAssistance, SeeingAssistance, ToiletingAssistance, and WalkingAssistance.</td></tr>
    <tr><td>__Example:__ Adding a word like onyxis for ingrown toenail.</td></tr>
    <tr><td>__featureNames:__ actionImplementNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>assistanceDevice</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new device that is used to help with the needed assistance, or to add new phrases, acronyms, or abbreviations for existing devices that are already covered in the base dictionary.</td></tr>
    <tr><td>__Annotators:__ BathingAssistance, DressingAssistance, EatingAssistance, SeeingAssistance, ToiletingAssistance, and WalkingAssistance.</td></tr>
    <tr><td>__Example:__ Adding a phrase like Makizume Robo for a tool that helps correct ingrown toenails.</td></tr>
    <tr><td>__featureNames:__ assistanceDeviceNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>cancer</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new type of cancer that is not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing cancers already covered in the base dictionary.</td></tr>
    <tr><td>__Annotators:__ Cancer</td></tr>
    <tr><td>__Example:__ Adding new cancer, TOT cancer.</td></tr>
    <tr><td>__featureNames:__ hccCode, icd9Code, icd10Code, ccsCode, cui, cancerNormalizedName, snomedConceptId</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>drug</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new drug that is not currently covered with the base dictionary, to add a new generic name for the same drug, or to add new commonly used phrases, acronyms, or abbreviations for existing drugs already covered in the base dictionary.</td></tr>
    <tr><td>__Annotators:__ Allergy and Medication</td></tr>
    <tr><td>__Example:__ Adding a misspelling aspirin - 'asprin.</td></tr>
    <tr><td>__featureNames:__ rxNormID, drugNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>echocardiogram</td>
     <td><table role="presentation"><tbody>
      <tr><td>__Description:__ Used to add a new type of ultrasound not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing echocardiogram phrases already covered with the base dictionary. </td></tr>
      <tr><td>__Annotators:__ EjectionFraction</td></tr>
      <tr><td>__Example:__ Adding TTE for transthoracic echocardiogram.</td></tr>
      <tr><td>__featureNames:__ echocardiogramNormalizedName</td></tr>
      <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>EFTerm</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new term not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing terms already covered with the base dictionary. </td></tr>
    <tr><td>__Annotators:__ EjectionFraction</td></tr>
    <tr><td>__Example:__ Adding HFpEF for preserved ejection fraction.</td></tr>
    <tr><td>__featureNames:__ efTermNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>EFAlphabeticValue</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new value not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing values already covered with the base dictionary.  The values in this table are words or phrases modifying the EF value.</td></tr>
    <tr><td>__Annotators:__ EjectionFraction</td></tr>
    <tr><td>__Example:__ Adding the word falling.</td></tr>
    <tr><td>__featureNames:__ efAlphabeticValueNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
   <tr><td>familyHistory</td>
     <td><table role="presentation"><tbody>
      <tr><td>__Description:__ Used to add additional family history trigger words not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing family history trigger words already covered in the base dictionary.</td></tr>
      <tr><td>__Annotators:__ Hypothetical</td></tr>
      <tr><td>__Example:__ Adding an alternate spelling for an existing family history trigger term or a new trigger term not currently in the base dictionary such as "sis."</td></tr>
      <tr><td>__featureNames:__ </td></tr>
      <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
     </tbody></table></td></tr>
   <tr><td>hypothetical</td>
     <td><table role="presentation"><tbody>
      <tr><td>__Description:__ Used to add additional hypothetical trigger words not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing hypothetical trigger words already covered in the base dictionary.</td></tr>
      <tr><td>__Annotators:__ Hypothetical</td></tr>
      <tr><td>__Example:__ Adding an alternate spelling for an existing hypothetical trigger term or a new trigger term not currently in the base dictionary such as "reviewed."</td></tr>
      <tr><td>__featureNames:__ </td></tr>
      <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ No</td></tr>
     </tbody></table></td></tr>
 <tr><td>illicitDrug</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new illegal drug that is not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing drugs already covered in the base dictionary.</td></tr>
    <tr><td>__Annotators:__ Smoking</td></tr>
    <tr><td>__Example:__ Adding a regional slang phrase like Calcutta Gold.</td></tr>
    <tr><td>__featureNames:__ illicitDrugNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>labType</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new type of lab type that is not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing lab types already covered in the base dictionary.</td></tr>
    <tr><td>__Annotators:__ Allergy, LabValue, and Medication</td></tr>
    <tr><td>__Example:__ Adding new phrase, platlet screening.</td></tr>
    <tr><td>__featureNames:__ loincId, labTypeNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>medicalCenter</td>
     <td><table role="presentation"><tbody>
      <tr><td>__Description:__ Used to add a new medical center or institution name not covered with the base dictionary, or to add alternate representations of a medical center name that is included.</td></tr>
      <tr><td>__Annotators:__ NamedEntities</td></tr>
      <tr><td>__Example:__ Adding a new medical center, Atrium Health.</td></tr>
      <tr><td>__featureNames:__ </td></tr>
      <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
     </tbody></table></td></tr>
 <tr><td>name</td>
     <td><table role="presentation"><tbody>
     <tr><td>__Description:__ Used to add a new proper name not covered with the base dictionary, or to add alternate spellings of a name that already exists.</td></tr>
     <tr><td>__Annotators:__ NamedEntities</td></tr>
     <tr><td>__Example:__ Adding a new proper name, or an alternate spelling of an existing one, Aleyah.</td></tr>
     <tr><td>__featureNames:__ </td></tr>
     <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>primaryAction</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new primary action that is used to help with the needed assistance, or to add new phrases, acronyms, or abbreviations for existing actions that are already covered in the base dictionary. </td></tr>
    <tr><td>__Annotators:__ BathingAssistance, DressingAssistance, EatingAssistance, SeeingAssistance, ToiletingAssistance, and WalkingAssistance</td></tr>
    <tr><td>__Example:__ Adding a phrase like weekly pedicure maintenance.</td></tr>
    <tr><td>__featureNames:__ primaryActionNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
    <tr><td>procedure</td>
     <td><table role="presentation"><tbody>
      <tr><td>__Description:__ Used to add a new procedure that is not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing procedures already covered in the base dictionary. </td></tr>
      <tr><td>__Annotators:__ Procedure</td></tr>
      <tr><td>__Example:__ Adding a phrase like <q>electric heart test</q>.</td></tr>
      <tr><td>__featureNames:__ cui, snomedConceptId, cptCode </td></tr>
      <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
     </tbody></table role="presentation"></td></tr>
   <tr><td>procedure</td>
     <td><table role="presentation"><tbody>
      <tr><td>__Description:__ Used to add a new procedure that is not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing procedures already covered in the base dictionary. </td></tr>
      <tr><td>__Annotators:__ Procedure</td></tr>
      <tr><td>__Example:__ Adding a phrase like <q>electric heart test</q>.</td></tr>
      <tr><td>__featureNames:__ cui, snomedConceptId, cptCode </td></tr>
      <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
     </tbody></table></td></tr>
 <tr><td>section</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new section that is not currently covered by the section annotator..</td></tr>
    <tr><td>__Annotators:__ Section</td></tr>
    <tr><td>__Example:__ Adding a phrase like, addendum to previous visit.</td></tr>
    <tr><td>__featureNames:__ sectionNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>secondaryAction</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new secondary action that is used to help with the needed assistance, or to add new phrases, acronyms, or abbreviations for existing actions that are already covered in the base dictionary.</td></tr>
    <tr><td>__Annotators:__ BathingAssistance, DressingAssistance, EatingAssistance, SeeingAssistance, ToiletingAssistance, and WalkingAssistance</td></tr>
    <tr><td>__Example:__ Adding a phrase like toenail straightening.</td></tr>
    <tr><td>__featureNames:__ secondaryActionNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>smokeSubstance</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new substance that might be lit and inhaled that is not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing substances already covered in the base dictionary.</td></tr>
    <tr><td>__Annotators:__ Smoking</td></tr>
    <tr><td>__Example:__ Adding the phrase hookah pipe.</td></tr>
    <tr><td>__featureNames:__ smokeSubstanceNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>smokeTerms</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new term for how the substance is ingested that is not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing terms already covered in the base dictionary.</td></tr>
    <tr><td>__Annotators:__ Smoking</td></tr>
    <tr><td>__Example:__ Adding a phrase second-hand hookah.</td></tr>
    <tr><td>__featureNames:__ smokeTermsNormalizedName</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
   </tbody></table></td></tr>
 <tr><td>symptomDisease</td>
   <td><table role="presentation"><tbody>
    <tr><td>__Description:__ Used to add a new disease that is not currently covered with the base dictionary, or to add new commonly used phrases, acronyms, or abbreviations for existing diseases already covered in the base dictionary.</td></tr>
    <tr><td>__Annotators:__ SymptomDisease</td></tr>
    <tr><td>__Example:__ Adding an ICD10 code for a phrase that did not have one.</td></tr>
    <tr><td>__featureNames:__ hccCode, icd9Code, icd10Code, ccsCode, cui, symptomDiseaseNormalizedName, snomedConceptId</td></tr>
    <tr><td>__Supports Regex patterns defined in the Domain Expert Tool:__ Yes</td></tr>
</tbody></table></td></tr></tbody></table>

Another example of the cancer whitelist option is listed in the following snippet.
The targeted surfaceforms is lungcancer and the featureNames include hccCode, icd9Code, icd10Code, ccsCode, cui, cancerNormalizedName, and snomedConceptId.

```javascript
"whitelist": {
    "name": "cancer",
    "entries": [
        {
            "surfaceForms": [
                "lungcancer"
            ],
            "features": {
                "cancerNormalizedName": "lung cancer",
                "hccCode": "9",
                "icd10Code": "C34.9",
                "ccsCode": "19",
                "icd9Code": "162.9",
                "snomedConceptId": "93880001",
                "cui": "C1306460"
            }
        }
    ]
}
```

<table>
<caption>Whitelist Options</caption>
<tr>
<th>Annotator Names</th>
<th>Possible Whitelist Options Dictionaries</th>
</tr>
<tr>
<td>**Allergy**</td>
<td>drug, labType</td>
</tr>
<tr>
<td>**Cancer**</td>
<td>cancer, neoplasticDisease</td>
</tr>
<tr>
<td>**BathingAssistance, DressingAssistance, EatingAssistance, SeeingAssistance, ToiletingAssistance, WalkingAssistance**</td>
<td>actionImplement, assistiveDevice, primaryAction, secondaryAction</td>
</tr>
<tr>
<td>**EjectionFraction**</td>
<td>echocardiogram, EFAlphabeticValue, EFTerm</td>
</tr>
<tr>
<td>**Hypothetical** </td>
<td>hypothetical, familyHistory</td>
</tr>
<tr>
<td>**LabValue**</td>
<td>labType</td>
</tr>
<tr>
<td>**Medication**</td>
<td>drug</td>
</tr>
<tr>
<td>**NamedEntities**</td>
<td>medicalCenter, name</td>
</tr>
<tr>
<td>**Procedure**</td>
<td>procedure</td>
</tr>
<tr>
<td>**Section**</td>
<td>section</td>
</tr>
<tr>
<td>**Smoking**</td>
<td>illicitDrug, smokeSubstance, smokeTerms</td>
</tr>
<tr>
<td>**SymptomDisease**</td>
<td>symptomDisease</td>
</tr>
</table>

Possible whitelist dictionaries for the **Allergy** annotator are *drug*, and *labType*.
An **Allergy** annotator may contain one or both whitelist dictionaries.

The possible whitelist dictionaries for each of the assistance annotators are _actionImplement_, _assistiveDevice_, _primaryAction_, _secondaryAction_.
An assistance annotator may have one, two, three, or all four whitelist dictionaries.

The Whitelist definitions can include multiple surface forms.
The following snippet shows two surface form entries for the <q>symptomDisease</q> whitelist dictionary.
The first definition contains three surface forms, i.e., <q>High BP</q>, <q>HIGH B.P.</q>, <q>high blood pres</q>;
the second definition contains three surface forms, i.e., <q>diabetes</q>, <q>Diab</q>, <q>Diabet</q>.
In the first definition below, SymptomDiseaseInd annotations will be created for any of the three surface forms found within the text. Each annotation will contain the seven features and values defined in the features section.

```javascript
"whitelists": [{
    "name": "symptomDisease",
    "entries": [{
      "surfaceForms": [
          "HIGH BP",
          "HIGH B.P.",
          "high blood pres"
    ],
    "features": {
      "symptomDiseaseNormalizedName": "hypertensive disorder",
          "hccCode": "19",
          "icd10Code": "I10",
          "ccsCode": "98",
          "icd9Code": "401.9",
          "snomedConceptId": "38341003",
          "cui": "C0020538"
      }},
      {
      "surfaceForms": [
          "diabetees",
          "Diab",
          "Diabet"
      ],
      "features": {
          "symptomDiseaseNormalizedName": "diabetes",
          "hccCode": "19",
          "icd10Code": "E14.9",
          "ccsCode": "49",
          "icd9Code": "250.00",
          "snomedConceptId": "7321100",
          "cui": "C0011849"
      }
    }]
}]
```
