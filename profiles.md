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

# Profiles
{: #profiles}

Profiles within ACD house annotator configurations associated with one or more annotators. Profiles can then be referenced within an ACD request where ACD will look up the annotator configurations defined within the referenced profile and inject annotator configurations within the profile into the corresponding annotators defined within the ACD request flow.
{:shortdesc}

##### 1. View list of available profiles within ACD (id & descriptions)

ACD deploys with some predefined profiles available to all ACD tenants - e.g. predefined profiles for evaluating predefined attribute sets. Use the _GET /v1/profiles_ API to view the list of available profiles for your tenant, including any descriptions of the profile that have been provided.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X GET --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" "https://host/services/clinical_data_annotator/api/v1/profiles?version=2019-02-06"
```

**Sample Response**

```javascript
{
    "default_profile_v1.0": {
      "description":"Default parameters for the concept detection and the attribute detection annotators when no profile id is specified in the flow. "
    },
    "general_cancer_v1.0": {
        "description": "This profile features a collection of Clinical Attributes that focus on cancer patient disease characteristics including the cancer type, disease progression, staging, tumor markers, and treatments."
    },
    "general_medical_v1.0": {
        "description": "This profile feature a collection of Clinical Attributes that represent the patient characteristics commonly used by physicians during a medical examination including laboratory, demographics, symptoms, diseases, and procedures."
    }
}
```

##### 2. View the contents of an individual profile

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X GET --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" "https://host/services/clinical_data_annotator/api/v1/profiles/default_profile_v1.0?version=2019-02-06"
```

**Sample Response**

```javascript
{
  "id": "default_profile_v1.0",
  "name": "Default Profile v1.0",
  "description": "Default parameters for concept detection and attribute detection annotators when no profile id is specified in the flow.",
  "annotators": [
    {
      "name": "attribute_detection",
      "parameters": {
        "attribute_set": [
          "general_medical_v1.0",
          "general_labs_v1.0"
        ]
      }
    },
    {
      "name": "concept_detection",
      "parameters": {
        "libraries": [
          "umls.2018aa"
        ]
      }
    }
  ]
}
```

##### 3. Reference a profile from an ACD request

In order to make use of the configurations defined within a profile, a profile may be referenced within a request as shown below. When ACD processes the request, configurations associated with the referenced profile are retrieved and injected into the request internally for processing. The configurations are only injected internally and are not returned as part of the annotator flow returned in the response.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" -d "{
  \"unstructured\": [
    {
      \"text\": \"Patient has lung cancer, but did not smoke. She may consider chemotherapy as part of a treatment plan.\"
    }
  ],
  \"annotatorFlows\": [
    {
	\"profile\" : \"default_profile_v1.0\",
      \"flow\": {
        \"elements\": [
          {
            \"annotator\": {
                \"name\":\"concept_detection\"
             }
          },
          {
            \"annotator\": {
                \"name\":\"concept_value\"
             }
          },
          {
            \"annotator\": {
                \"name\":\"attribute_detection\"
             }
          }
        ],
        \"async\":\"false\"
       }
    }
  ]
}" "https://host/services/clinical_data_annotator/api/v1/analyze?version=2019-02-06"
```
##### 4. Default profile and Empty Profile

The default ACD profile will be used if there is no profile is specified in the flow. The default profile contains parameters for the concept detection and the attribute detection annotators. If absolutely no parameter is desired, then an empty profile can be created and be used in the annotator flow. In other words, Profile is a necessary for annotator flow starting from **2019-02-06**.

```bash
{
  "id": "empty_profile",
  "description": "This profile has no parameters for any annotators."
}
```


##### 5. Adjudicating configurations passed in the request and those found within a referenced profile

ACD consumers can simultaneously reference configurations housed within a profile and pass additional configurations within the request.
Configurations found in a referenced profile will be merged with any configurations present within the request, with the exception of the following scenario, in which configurations present in the request will supersede those found in the referenced profile.

###### Scenarios where configurations present in the request supersede those defined within a referenced profile

1.  The same configuration parameter is defined for an annotator in both the incoming request and the referenced profile. In this case, the config parameter defined within the request will supersede the config parameter value defined within the profile.
2.  There are configuration entries such as filters or whitelists in both the incoming request and the referenced profile. In this case, configuration entries defined within the request will supersede the configuration entries defined within the profile.
