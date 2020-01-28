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

{{site.data.keyword.wh-acd_short}} enables you to detect medical concepts within unstructured data. When you provide an annotator flow, typically defined within the {{site.data.keyword.wh-acd_short}} Configuration Editor, and plain text to be analyzed, the service will employ the annotators and configurations defined within the flow to detect medical concepts within the provided text.

How it works:
1. Define configurations for the service via the configuration editor.
2. Export your configurations as a cartridge zip.
3. Deploy the cartridge zip to the service via the deploy API as shown:

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/octet-stream" \
--header "Accept: application/json" \
--data-binary @/tmp/acd_cartridge_v1.0.zip \
"{url}/v1/deploy?version=2019-04-20"
```

Once the cartridge is deployed to the service, you can reference the desired annotator flow as a path parameter to the analyze API as shown:

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: text/plain" \
--header "Accept: application/json" \
-d "Patient has lung cancer, but did not smoke. She may consider chemotherapy as part of a treatment plan." \
"{url}/v1/analyze/acd_cartridge_v1.0_default_flow?version=2019-04-20&return_analyzed_text=false"
```

The **return_analyzed_text** parameter is a boolean query parameter with _false_ as the default value.  
By default (i.e. return_analyzed_text=false), certain characters are encoded in the ACD response to protect against cross-site scripting attacks in the event the ACD output is rendered within a browser. 
Examples of encoding are as shown below. 

```bash
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


