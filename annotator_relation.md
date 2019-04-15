<h3 id="relation">Relation (Experimental)</h3>

The relation annotator is intended to be used in conjunction with the concept_detection annotator to identify relations within unstructured data associated with concepts retrieved from the concept_detection annotator. The relations are detected via identifying triggering concepts within a sentence indicating a possible relationship. Thus, the concept_detection annotator must run prior to the relation annotator within an annotator flow to function properly.


The Domain Expert Tool (DET) allows customization of the relation annotator with a target ontology and a set of relation names. The ACD will use the deployed cartridge from the DET tool to annotate an unstructured text. The following snippet illustrates a typical annotator flow for a relation annotator along with its configuration.

```javascript
{
  ...
  "annotators": [
    {
      "name": "relation",
      "parameters": {
        "relationship_configurations": [
          "cartridge_name_relation_config_name"
        ]
      }
    }
  ]
}
```

The following json object illustrates a typical the relation object; which references two concepts using their concept uid. The UIDs are uniques to specific concepts and can be used to locate concepts in the concept sections. Each relation is uniquely identified by "relation_type".

```javascript

{
	"unstructured": [{
		"data": {
			"concepts": [{
				"cui": "C0039286",
				"uid": 3
			},
			{
				"cui": "C3540688"
			},
			{
				"cui": "C1458155",
				"uid": 2
			}],
			"relations": [{
				"source": "umls",
				"nodes": [{
					"entity": {
						"uid": 2
					}
				},
				{
					"entity": {
						"uid": 3
					}
				}],
				"type": "may_treat"
			}]
		}
	}]
}

```
