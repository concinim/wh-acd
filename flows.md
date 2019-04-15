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

# Flows
{: #flows}

An annotator flow within ACD defines a set of one or more annotators, and optionally, includes annotator configurations and flow sequence. Annotator flows can be dynamically defined as part of a request, or predefined and persisted for a specific tenant. When persisted, a flow definition also contains a name, ID, and description of the flow, in addition to the annotators and their configurations. When a flow is specified as part of an analyze request, the sequence of annotators and any configurations defined in the flow are internally applied to the request when processing and analyzing the input text.
{:shortdesc}

#### Provided Annotator Flows

ACD provides two predefined flows for evaluation purposes. Each flow contains the same annotators and configurations that are provided through two predefined profiles, the general_medical_v1.0 profile and the general_cancer_v1.0 profile. See the <a data-scroll="" href="#profiles">Profiles</a> section for more details on the profiles.

Predefined flows can not be updated or deleted.

<table>
<tr>
<th>Annotator Flow</th><th>Description</th>
</tr>
</tbody>
<tr>
<td>
general_medical_v1.0_flow | Includes the concept detection annotator with the umls.2017AA library and attribute detection annotator with the general_medical_v1.0 and general_labs_v1.0 attribute sets. This flow might be used for detecting clinical attributes in a general medical domain.
</td>
<td>
general_cancer_v1.0_flow | Includes the concept detection annotator with the umls.2017AA library and attribute detection annotator with the attribute sets: general_medical_v1.0, general_labs_v1.0 and general_cancer_v1.0. This flow might be used for detecting clinical attributes in a medical oncology and disease domain.
</td>
</tr>
</tbody>
</table>

##### 1. View list of available flows within ACD (ID & descriptions)

Use the _GET /v1/flows_ API to view the list of available predefined or persisted flows for your tenant, including any provided descriptions of the flows.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X GET --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" "https://host/services/clinical_data_annotator/api/v1/flows?version=2017-10-02"
```

**Sample Response**

```javascript
{
  "flow_simple": {
    "description": "A simple flow with two annotators and a profile reference"
  },
  "flow_daily_living_assistance": {
    "description": "A flow containing the set of living assistance annotators"
  },
  "general_cancer_v1.0_flow": {
    "description": "This flow uses the Concept and Attribute Detection annotators with common configuration as defined in the General Cancer V1.0 Profile."
  },
  "general_medical_v1.0_flow": {
    "description": "This flow uses the Concept and Attribute Detection annotators with common configuration as defined in the General Medical V1.0 Profile."
  }
}
```

##### 2. View the contents of a specific flow

To view the contents of a specific flow, invoke the REST API with the flow ID supplied as the path parameter.
The following curl command returns the contents of `flow_simple`.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X GET --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" "https://host/services/clinical_data_annotator/api/v1/flows/flow_simple?version=2017-10-02"
```

**Sample Response**

```javascript
{
    "id": "flow_simple",
    "description": "A simple flow with two annotators and a profile reference",
    "annotatorFlows": [
        {
            "profile": "general_medical_v1.0",
            "flow": {
                "elements": [
                    {
                        "annotator": {
                            "name": "concept_detection"
                        }
                    },
                    {
                        "annotator": {
                            "name": "symptom_disease"
                        }
                    }
                ]
            }
        }
    ]
}
```

##### 3. Create a flow from an ACD request

Creating an annotator flow is carried out using a POST operation. A flow is identified by an ID. A flow definition contains a list one or more annotators, and optionally can include annotator configuration, a profile ID, and/or flow sequence. If a caller chooses to have the ID of the new flow generated on their behalf, then in the request body the <q>id</q> field of the flow definition should be an empty string (<q></q>). The auto-generated ID would be a normalized form of the <q>name</q> field from the flow definition. The following curl command creates `my_flow`.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" -d "{
  \"id\": \"my_flow\",
  "\name\": \"my flow",
  \"description\": \"A simple flow with two annotators\",
  \"annotatorFlows\": [
      {
       \"flow\": {
          \"elements\": [
             {
               \"annotator\": {
                   \"name\": \"concept_detection\"
                }
             },
             {
               \"annotator\": {
                   \"name\": \"symptom_disease\"
                }
             }
           ]
        }
      }
   ]
}" "http://host/services/clinical_data_annotator/api/v1/flows?version=2017-11-03"
```

##### 4. Update a flow from an ACD request

A persisted flow definition can be changed or updated using the PUT operation. The existing flow will be updated in its entirety by the new flow definition. The following curl command updates the definition of `my_flow`.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X PUT --header "Content-Type: application/json" --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" -d "{
  \"id\": \"my_flow\",
  \"description\": \"An advanced flow with two annotators\",
  \"annotatorFlows\": [
    {
      \"flow\": {
        \"elements\": [
          {
            \"annotator\": {
              \"name\": \"concept_detection\"
            }
          },
          {
            \"annotator\": {
              \"name\": \"symptom_disease\"
            }
          }
        ]
      }
    }
  ]
}" "http://host/services/clinical_data_annotator/api/v1/flows/my_flow?version=2017-11-03"
```

##### 5. Delete a flow from an ACD request

A tenant defined flow can be removed from the list of persisted flows by using the flow ID. The following curl command deletes `flow_sample2`.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X DELETE --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" "http://host/services/clinical_data_annotator/api/v1/flows/flow_sample2?version=2017-11-03"
```

##### 6. Reference a flow from an ACD request

A persisted flow can be used in several ways as shown below.
When ACD processes a user's request (see 6.a - 6.d),
the annotator sequence along with any annotator configuration defined in the persisted flow are retrieved and injected into the request internally for processing.
Note: The flow definition is used internally and is not returned in the response.

###### 6.a Directly use the flow ID in the request

Indicate the flow ID as a path parameter in the _POST /v1/analyze_ REST API request (also contained in the REST request is the unstructured plain text). The following curl command references `flow_id`.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X POST --header "Content-Type: text/plain" --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" -d \"Patient will start on cisplatin 80mg on 1/1/2018.\"
"https://host/services/clinical_data_annotator/api/v1/analyze/flow_id?version=2017-10-02"
```

###### 6.b Passing unstructured text along with annotated concepts to a persisted flow

Indicate the flow ID as a path parameter in the _POST /v1/analyze_ API.
In this case, the unstructured text is inside a JSON structure which may contain additional concepts originated from other external annotators. The following curl command references `flow_id`.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" -d "{
  \"unstructured\": [
    {
      \"text\": \"Patient will start on cisplatin 80mg on 1/1/2018. Patient is also diabetic.\",
      \"data\": {
        \"concepts\": [
          {
            \"cui\": \"C0030705\",
            \"preferredName\": \"Patients\",
            \"semanticType\": \"podg\",
            \"source\": \"umls\",
            \"sourceVersion\": \"2017AA\",
            \"type\": \"umls.PatientOrDisabledGroup\",
            \"begin\": 0,
            \"end\": 7,
            \"coveredText\": \"Patient\"
          }
        ]
      }
    }
  ]
}" "http://host/services/clinical_data_annotator/api/v1/analyze/flow_id?version=2017-11-01"
```
