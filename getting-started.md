---

copyright:
  years: 2011, 2019
lastupdated: "2019-04-10"

keywords: annotator clinical data, clinical data, annotation, getting started tutorial, IBM Cloud, annotator for clinical data

subcollection: wh-acd

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

This short tutorial introduces the {{site.data.keyword.wh-acd_full_notm}} with example requests and links to additional resources.
{:shortdesc}

## Before you begin
{: #before-you-begin}

- {: hide-dashboard} Create an instance of the service:
    1.  Go to the [{{site.data.keyword.wh-acd_short}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog/services/wh-acd){: new_window} page in the {{site.data.keyword.Bluemix_notm}} Catalog.
    2.  Sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in.
    3.  Click **Create**.
- Copy the credentials to authenticate to your service instance:
    1.  On the **Manage** page, click **Show** to view your credentials.
    2.  Copy the `API Key` and `URL` values.
- Make sure that you have the `curl` command:
    - The examples use `curl` command to call methods of the HTTP interface. Install the version for your operating system from [curl.haxx.se ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://curl.haxx.se/){: new_window}. Install the version that supports the Secure Sockets Layer (SSL) protocol. Make sure to include the installed binary file on your `PATH` environment variable.

## Step 1. Send plain text input to be analyzed using an existing flow and receive JSON output
{: #getting_started_step1}

The first example passes plain text data to the analyze API using a predefined flow that identifies concepts using the concept_detection annotator and clinical attributes using the attribute_detection annotator.

```Curl
  curl -X POST -u "apikey:{apikey}" \
  --header "Content-Type: text/plain;charset=utf-8" \
  --header "Accept: application/json" \
  -d "Patient has lung cancer, but did not smoke. She may consider chemotherapy as part of a treatment plan." \
  "{url}/v1/analyze/general_cancer_v1.0_flow?version=2017-10-13"
```
{: pre}

The service returns a JSON object that includes annotations for medical concepts found using the [Unified Medical Language System (UMLS)](https://www.nlm.nih.gov/research/umls/) and clinical attributes related to general cancer.

## Step 2. Send JSON input to be analyzed using an existing flow and receive JSON output.
{: #getting_started_step2}

The second example passes unstructured text as JSON input to the analyze API using a predefined flow that identifies concepts using the concept_detection annotator and clinical attributes using the attribute_detection annotator.

```Curl
  curl -X POST -u "apikey:{apikey}" \
  --header "Content-Type: application/json;charset=utf-8" \
  --header "Accept: application/json" \
  -d "{
   \"unstructured\": [
    {
      \"text\": \"Patient has lung cancer, but did not smoke. She may consider chemotherapy as part of a treatment plan.\"     
    }
   ]
  }" \
  "{url}/v1/analyze/general_cancer_v1.0_flow?version=2019-04-02&return_analyzed_text=false"
```
{: pre}

The service returns a JSON object that includes annotations for medical concepts found using the [UMLS](https://www.nlm.nih.gov/research/umls/) and clinical attributes related to general medical.


## Next steps
{: #getting_started_step3}

* Learn more about [customizing](/docs/services/wh-acd?topic=wh-acd-customizing#customizing)  {{site.data.keyword.wh-acd_short}}
* Learn more about the API in the [API reference](https://cloud.ibm.com/apidocs/wh-acd).
