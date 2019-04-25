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

# Analyzing Text
{: #analyze_text}

Annotator for Clinical Data (ACD) enables you to detect medical concepts within unstructured data. ACD provides a diverse set of medical-domain annotators and annotator artifacts that can be leveraged out-of-the-box or customized via the Domain Expert Tool (DET).

**How it works:**

1. Configure your ACD Knowledge Cartridge via the Domain Expert Tool (DET): https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html
2. Export your cartridge zip from DET.
3. Deploy the cartridge zip to ACD via the ACD /deploy API as shown below:

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/octet-stream" \
--header "Accept: application/json" \
--data-binary @/tmp/acd_cartridge_v1.0.zip \
"{url}/v1/deploy?version=2019-04-20"
```
{: pre}

4. Once the cartridge is deployed to ACD, you can reference the desired annotator flow as a path parameter to the /analyze API as shown below:

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: text/plain" \
--header "Accept: application/json" \
"{url}/v1/analyze/acd_cartridge_v1.0_default_flow?version=2019-04-20"
```
{: pre}
