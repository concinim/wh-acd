---

copyright:
  years: 2011, 2019
lastupdated: "2019-04-12"

keywords: annotator clinical data, clinical data, annotation

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

# Analyzing Text
{: #analyze_text}

{{site.data.keyword.wh-acd_short}} detects medical concepts within unstructured data. When you send unstructured data to the service to be analyzed and designate the desired annotators to employ, the service will route your unstructured data through the designated annotators and return the medical concepts detected within your unstructured data.

How it works:
1. Designate which annotators to employ in analyzing your unstructured data. This designation is defined as an annotator flow. See [Annotator Flows] for more details.
2. Send your unstructured data along with the annotator flow to the service to extract the desired medical concepts.

**Example:** analyze request referencing a persisted flow

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: text/plain" \
--header "Accept: application/json" \
-d "Patient has lung cancer, but did not smoke. She may consider chemotherapy as part of a treatment plan." \
"{url}/v1/analyze/your_flow_id?version=2020-03-13"
```

When referencing a persisted flow in an analyze request, you can send plain text to the service for analysis.

**Example:** analyze request within flow included

```bash
curl -X POST -u "apikey:{apikey}" \
  --header "Content-Type: application/json" \
  --header "Accept: application/json" -d "{
  \"annotatorFlows\": [
    {
      \"flow\": {
        \"elements\": [
          {
            \"annotator\": {
              \"name\": \"cancer\"
            }
          },
          {
            \"annotator\": {
              \"name\": \"medication\"
             }
          }
        ],
        \"async\": false
      }
    }
  ],
  \"unstructured\": [
    {
      \"text\": \"Patient has lung cancer, but did not smoke. She may consider Cisplatin as part of a treatment plan.\"
    }
  ]
}" "{url}/v1/analyze?version=2020-03-13"
```

By default, the unstructured data input sent to the service is not returned in the response and the following characters are encoded in the response to protect against cross-site scripting attacks in the event the output is rendered within a browser. If you want the unstructured data input sent back in the response and you do not want the following characters encoded, include the following query parameter on the analyze request `return_analyzed_text=true`.

```bash
# Default character encodings in response
 & --> &amp;
 < --> &lt;
 > --> &gt;
 " --> &quot;
 ' --> &#x27;     
 / --> &#x2F;  
```

A sample ACD response is shown below when the default setting (i.e. return_analyzed_text=false) is used, i.e. when the encoding process is activated. Notice that the begin and the end field of the concepts are not affected by the character encoding.  Set return_analyzed_text=true to avoid the encoding results and to show the analyzed text in the ACD response.  

```bash
{
    "unstructured": [
        {
            "data": {
                "conceptValues": [
                    {
                        "cui": "C0005893",
                        "preferredName": "Body mass index procedure",
                        "trigger": "greater than",
                        "value": "40",
                        "type": "ConceptValue",
                        "begin": 1,
                        "end": 9,
                        "coveredText": "BMI &gt; 40"
                    }
               ]
            }
        }
    ]
}
```
