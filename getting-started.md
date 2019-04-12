---

copyright:
  years: 2011, 2019
lastupdated: "2019-04-10"

keywords: getting started tutorial, IBM Cloud, ACD, annotator for clinical data

subcollection: writing

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

<!-- Name your file `getting-started.md` and include it in the Learn nav group in your toc file. -->


# Getting started tutorial
{: #getting-started}

This short tutorial introduces the IBM Watson Annotator for Clinical Data (ACD) with example requests and links to additional resources.

{: shortdesc}

## Before you begin
{: #prereqs}

* Create an instance of the service:
  1. Go to the [IBM Watson Annotator for Clinical Data](https://dev.console.test.cloud.ibm.com/catalog/services/wh-acd) page in the IBM Cloud Catalog.
  2. Sign up for a free IBM Cloud account or log in.
  3. Click **Create**.
* Copy the credentials to authenticate to your service instance:
  1. From the [IBM Cloud dashboard](https://dev.console.test.cloud.ibm.com/dashboard/apps), click on your IBM Watson Annotator for Clinical Data service instance to go to the Annotator for Clinical Data service dashboard page.
  2. On the **Manage** page, click **Show** to view your credentials.
  3. Copy the `API Key` and `URL` values.
* Make sure that you have the `curl` command.
  * The examples use the `curl` command to call methods of the HTTP interface. Install the version for your operating system from [curl.haxx.se](https://curl.haxx.se). Install the version that supports the Secure Sockets Layer (SSL) protocol. Make sure to include the installed binary file on your `PATH` environment variable.  

When you enter a command, replace `{apikey}` and `{url}` with your actual API key and URL. Omit the braces, which indicate a variable value, from the command. An actual value resembles the following example:

```Curl
  $ curl -X POST -u "apikey:L_HALhLVIksh1b73l97LSs6R_3gLo4xkujAaxm7i-b9x"
  . . .
  "https://gateway.watsonplatform.net/wh-acd/api/v1/analyze?version=2017-09-21"
```

## Step 1. Send plain text input to be analyzed using an existing flow and receive JSON output
{: #anchor_value}

The first example passes plain text data to the analyze API using a predefined flow that identifies concepts using the concept_detection annotator and clinical attributes using the attribute_detection annotator.

  ```Curl
  $ curl -X POST -u "apikey:{apikey}" \
  --header "Content-Type: text/plain;charset=utf-8" \
  --header "Accept: application/json" \
  -d "Patient has lung cancer, but did not smoke. She may consider chemotherapy as part of a treatment plan." \
  "{url}/v1/analyze/general_cancer_v1.0_flow?version=2017-10-13"
  ```
  {: pre}

The service returns a JSON object that includes annotations for medical concepts found using the [Unified Medical Language System (UMLS)](https://www.nlm.nih.gov/research/umls/) and clinical attributes related to general cancer.

## Step 2. Send JSON input to be analyzed using an existing flow and receive JSON output.
{: #anchor_value}

The second example passes unstructured text as JSON input to the analyze API using a predefined flow that identifies concepts using the concept_detection annotator and clinical attributes using the attribute_detection annotator.

```Curl
  $ curl -X POST -u "apikey:{apikey}" \
  --header "Content-Type: text/plain;charset=utf-8" \
  --header "Accept: application/json" \
  -d "{
   \"unstructured\": [
    {
      \"text\": \"Patient will not start on cisplatin 80mg on 1/1/2018. Patient is also diabetic.\"     
    }
   ]
  }" \
  "{url}/v1/analyze/general_medical_v1.0_flow?version=2019-04-02&return_analyzed_text=false"
```
{: pre}

The service returns a JSON object that includes annotations for medical concepts found using the [UMLS](https://www.nlm.nih.gov/research/umls/) and clinical attributes related to general medical.

## Step 3. Send JSON input to be analyzed and receive JSON output.
{: #anchor_value}

The third example passes the annotators to run as part of the input request. This example shows running the concept_detection and the symptom_disease annotators.

```Curl
  $ curl -X POST -u "apikey:{apikey}" \
  --header "Content-Type: text/plain;charset=utf-8" \
  --header "Accept: application/json" \
  -d "{
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
          ],
          \"async\": false
        }
      }
    ],
    \"unstructured\": [
      {
        \"text\": \"Patient has lung cancer, but did not smoke. She may consider chemotherapy as part of a treatment plan.\"
      }
    ]
    }"  "{url}/v1/analyze?version=2019-04-02&return_analyzed_text=false"
```
{: pre}

## Next steps
{: #anchor_value}

* Learn more abou tthe API in the [API reference](https://cloud.ibm.com/apidocs/wh-acd).
* _TODO: Come back and decide if there's additional links we want to provide here_
