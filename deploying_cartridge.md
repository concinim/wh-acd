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

# Deploying a Cartridge
{: #deploy_cartridge}

1.  The consumer uses the [Domain Expert Tool (DET)](https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/) to create a new cartridge (or modify an existing one) and customizes the contents (artifacts) of the cartridge to their domain.
2.  Next, using the DET, the consumer will **Export** the cartridge in order to save a snapshot of the cartridge.
3.  Lastly, the consumer deploys the cartridge snapshot (a zip file) to  {{site.data.keyword.wh-acd_short}} using _POST /v1/deploy_ API. In the following curl example, the consumer's cartridge file is `./my_cartridges/name_of_cartridge_file.zip`, and `update=false` means do not update the resource if it already exists. Specifying the **update=true** parameter on the deploy API to update an existing cartridge.

Replace `{apikey}` and `{url}` with the actual API key and URL in the following example. A successful cartridge deploy will result in <q>201 Created</q> if it is a new resource, or <q>200 OK</q> if `update=true` was specified and the existing resource was updated.

```Curl
  curl -X POST -u "apikey:{apikey}" \
  --header "Accept: application/json" \
  -F "archive_file=@./my_cartridges/name_of_cartridge_file.zip" \
  "{url}/v1/deploy?update=false&version=2018-01-17"

```
{: pre}

**Note:**  Some large cartridge deployments can exceed the request timeout thresholds defined in the DataPower gateways (usually after 2 mins). In that event, you may receive the following error response. See [Cartridge Deployment Timeout](wh-acd?topic=wh-acd-troubleshoot#troubleshoot_deploy_timeout) for additional considerations during the deployment of large cartridges.
