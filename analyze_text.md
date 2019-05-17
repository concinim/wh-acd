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

{{site.data.keyword.wh-acd_short}} enables you to detect medical concepts within unstructured data. When you provide an annotator flow, typically defined within the Domain Expert Tool (DET), and plain text to be analyzed, the service will employ the annotators and configurations defined within the flow to detect medical concepts within the provided text.

**How it works:**

1. Define configurations for the service via the Domain Expert Tool (DET): https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html
2. Export your configurations as a cartridge zip.
3. Deploy the cartridge zip to the service via the deploy API as shown below:
```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/octet-stream" \
--header "Accept: application/json" \
--data-binary @/tmp/acd_cartridge_v1.0.zip \
"{url}/v1/deploy?version=2019-04-20"
```
{: pre}
4. Once the cartridge is deployed to the service, you can reference the desired annotator flow as a path parameter to the analyze API as shown below:

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: text/plain" \
--header "Accept: application/json" \
-d "Patient has lung cancer, but did not smoke. She may consider chemotherapy as part of a treatment plan." \
"{url}/v1/analyze/acd_cartridge_v1.0_default_flow?version=2019-04-20"
```
{: pre}
