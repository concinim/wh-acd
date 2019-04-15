<h3 id="nlu_annotator">NLU Annotator (Experimental) </h3>


The Natural Language Understanding (NLU) annotator enables the ACD service to interact with the <a href="https://console.bluemix.net/catalog/services/natural-language-understanding">IBM Watson NLU service</a>. The NLU service extracts features from the unstructured text based on the NLU configuration. The ACD service will supply the unstructured text to the NLU service, capture the response, and extract the relevant response features so that they can be easily used by other annotators in the ACD flow.

The NLU service uses advanced NLP to analyze text and extract features from content such as **concepts**, **entities**, **keywords**, **categories**, **sentiment**, **emotion**, **relations**, and **semantic roles**. Depending upon the model selected in the NLU configuration, pronouns related to the trained entities may also be resolved to the relevant entities.

At this moment, the ACD service provides a custom drug model out of the box. You may also apply a custom entity-relationship model developed using <a> Watson Knowledge Studio </a> to identify industry/domain specific entities and relations in unstructured text with Watson NLU. The full documentation of the NLU service is available at <a href="https://console.bluemix.net/catalog/services/natural-language-understanding">IBM Watson</a>.



<h4>Sample Request</h4>

The NLU annotator can be directly invoked as a stand-alone annotator in the ACD service as depicted in the following annotator flow.

```javascript

{
  "annotatorFlows": [
    {
      "flow": {
        "elements": [
          {
            "annotator": {
              "name": "nlu",
              "parameters": {
                  "configuration": ["ibm_drug"]
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
    	  "text": "Moexipril may cause dizziness"
    }
  ]
}

```

Similar to the other annotators, the <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html" target="_blank">Domain Expert Tool (DET)</a> is provided as a means to select a specific configuration for the NLU annotator.
Valid parameter for the NLU annotator is listed in the following table.

<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>configuration</td>
<td>An identify of a specific configuration. Available configurations are as follows.

<table role="presentation"><tbody>
  <tr><td>default_nlu_configuration</td><td> Default NLU entities and relations.</td></tr>
  <tr><td>ibm_drug</td><td> WH ACD Model for Drugs and Diseases entities and relations. </td>
</tbody>
</tr>
</table>



<h4> Sample  Response </h4>

Responses from the NLU annotator are organized into three groups inside the unstructured data object. Each group represents different aspects of the response.
- The **nluEntities** group includes all entities extracted from the original NLU response.
- The **relations** group identify the relations between two entities.
- The **nluResults** group contains the original response of the NLU service.

```javascript
{
  "unstructured": [
    {
      "text": "Moexipril may cause dizziness",
      "data": {
        "nluEntities": [
        ...
        ],
        "relations":[
        ...
        ],
        "nluResults": [
        ...
        ]
      }
    }
  ]
}
```


The following snippet lists a typical **nluEntities** group.
Each object in the **nluEntities** group includes the source, type, begin, end, coveredText, and uid field.
The "uid" field is available only if the entities will be referenced by a relation, which will be listed in the **relations** group .

```javascript

 "nluEntities": [
	{
		"source": "IBM Drug NLU Model",
		"type": "drug",
		"begin": 0,
		"end": 9,
		"coveredText": "Moexipril"
	},
	{
		"source": "IBM Drug NLU Model",
		"type": "symptom",
		"begin": 20,
		"end": 29,
		"coveredText": "dizziness"
	},
	{
		"source": "IBM Drug NLU Model",
		"type": "drug",
		"begin": 0,
		"end": 9,
		"coveredText": "Moexipril",
		"uid": 1
	},
	{
		"source": "IBM Drug NLU Model",
		"type": "symptom",
		"begin": 20,
		"end": 29,
		"coveredText": "dizziness",
		"uid": 2
	}
]

```


The following snippet lists a typical **relations** group.
The **relations** group contains a list of relation object.
Each object has the *source*, *score*, *nodes* and *type* fields.
The nodes field list the connection between two entities which are uniquely identified by uids.
The same uids are used to identify entities in both the **relation** group and the **nluEntities** group.

```javascript
   "relations": [
	{
		"source": "IBM Drug NLU Model",
		"score": 0.992617,
		"nodes": [
			{
				"entity": {
					"uid": 1
				}
			},
			{
				"entity": {
					"uid": 2
				}
			}
		],
		"type": "canCause"
	}
]
```

The following snippet shows a  **nluResults** group.
The **nluResults** group contains an original response to the NLUService.

```javascript

  "nluResults": [
	{
		"usage": {
			"text_units": 1,
			"text_characters": 29,
			"features": 2
		},
		"relations": [
			{
				"type": "canCause",
				"sentence": "Moexipril may cause dizziness",
				"score": 0.992617,
				"arguments": [
					{
						"text": "Moexipril",
						"location": [
							0,
							9
						],
						"entities": [
							{
								"type": "drug",
								"text": "Moexipril",
								"disambiguation": {
									"subtype": [
										"NONE"
									]
								}
							}
						]
					},
					{
						"text": "dizziness",
						"location": [
							20,
							29
						],
						"entities": [
							{
								"type": "symptom",
								"text": "dizziness",
								"disambiguation": {
									"subtype": [
										"NONE"
									]
								}
							}
						]
					}
				]
			}
		],
		"language": "en",
		"entities": [
			{
				"type": "drug",
				"text": "Moexipril",
				"mentions": [
					{
						"text": "Moexipril",
						"location": [
							0,
							9
						]
					}
				],
				"disambiguation": {
					"subtype": [
						"NONE"
					]
				},
				"count": 1
			},
			{
				"type": "symptom",
				"text": "dizziness",
				"mentions": [
					{
						"text": "dizziness",
						"location": [
							20,
							29
						]
					}
				],
				"disambiguation": {
					"subtype": [
						"NONE"
					]
				},
				"count": 1
			}
		]
	}
]
```

<h4> IBM Drug Model  Response </h4>

The recommended entity and relation types of the IBM drug model are listed in the following tables. The IBM drug model is trained with and is intended to be used for the drug labels and medical literatures such as medline or pubmed publications. The IBM drug model works best with properly formed sentences rather than phrase fragment. **Entity types** are listed in the following table.

```javascript
- druggroup
- drug
- indication
- symptom
- population
- substance
- bodyfunction
- virus
- bodypart
- organism
- food
- riskfactors
- diseaseclass
- combinationmed
- vitals
- treatment
```


<table>
	<caption>Relation Types</captions>
	<tr><th>Relation Name</th><th>Left Entities</th><th>Right Entities</th></tr>
<tr>
<td>isContraindicatedFor</td>
<td>druggroup,food,drug,combinationmed</td>
<td>diseaseclass,indication,symptom</td>
</tr>

<tr>
<td>interactWith</td>
<td>drug,food,druggroup,combinationmed</td>
<td>food,substance,druggroup,combinationmed,drug</td>
</tr>

<tr>
<td>relieve</td>
<td>drug,combinationmed,druggroup,food</td>
<td>indication,system</td>
</tr>

<tr>
<td>occurInPopulation</td>
<td>indication,symptom,diseaseclass</td>
<td>population</td>
</tr>

<tr>
<td>belongToDiseaseclass</td>
<td>indication</td>
<td>diseaseclass</td>
</tr>

<tr>
<td>attack</td>
<td>druggroup,drug,combinationmed</td>
<td>virus</td>
</tr>

<tr>
<td>blockReleaseOf</td>
<td>drug,combinationmed,food,druggroup</td>
<td>substance</td>
</tr>

<tr>
<td>treat</td>
<td>drug, food, druggroup, combinationmed</td>
<td>symptom, diseaseclass, indication</td>
</tr>


<tr>
<td>impactedBodypart</td>
<td>surgery,symptom,indication,treatment,radiation,</br> diseaseclass,combinationmed,bodyfunction,chemotherapy,food,druggroup,drug</td>
<td>bodypart</td>
</tr>

<tr>
<td>usedInPopulation</td>
<td>food,drug,druggroup,combinationmed</td>
<td>population</td>
</tr>

<tr>
<td>contain</td>
<td>drug, food, combinationmed</td>
<td>virus, drug, food</td>
</tr>


<tr>
<td>indicatedFor</td>
<td>combinationmed,druggroup,food,drug</td>
<td>indication,diseaseclass,symptom</td>
</tr>


<tr>
<td>control</td>
<td>food,druggroup,combinationmed,substance,drug</td>
<td>indication,substance,bodyfunction,symptom</td>
</tr>

<tr>
<td>reduceRiskOf </td>
<td>food,druggroup,combinationmed,drug</td>
<td>symptom,diseaseclass,indication</td>
</tr>

<tr>
<td>canCause</td>
<td>treatment, surgery, symptom, substance, drug,</br>
combinationmed,organism,diseaseclass,indication,druggroup,food</td>
<td>indication, symptom</td>
</tr>

<tr>
<td>hasSideEffectOf</td>
<td>drug,combinationmed,food,druggroup</td>
<td>symptom,indication</td>
</tr>


<tr>
<td>decrease</td>
<td>drug,druggroup,combinationmed,food</td>
<td>symptom,indication</td>
</tr>

<tr>
<td>usedWithDrug</td>
<td>food,treatment,combinationmed,druggroup,drug</td>
<td>food,drug,combinationmed,druggroup</td>
</tr>

<tr>
<td>prevent</td>
<td>drug,food,combinationmed,druggroup</td>
<td>symptom,diseaseclass,indication</td>
</tr>

<tr>
<td>belongToDruggroup</td>
<td>druggroup,food,drug,combinationmed</td>
<td>treatment,druggroup,food</td>
</tr>

</table>
