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

Once your customizations are complete, you can use the DET to publish your cartridge and export the published cartridge to a zip file. The exported cartridge can be deployed to  {{site.data.keyword.wh-acd_short}} using the POST /v1/deploy API.

For example (replace `{apikey}` and `{url}` with your actual API key and URL):

```Curl
  curl -X POST -u "apikey:{apikey}" \
  --header "Accept: application/json" \
  -F "archive_file=@./my_cartridges/name_of_cartridge_file.zip" \
  "{url}/v1/deploy?update=false&version=2018-01-17"

```
{: pre}

To update an existing cartridge, specify the **update=true** parameter on the deploy API.

For deployment of large cartridges, see [Cartridge Deployment Timeout](wh-acd?topic=wh-acd-troubleshoot#troubleshoot_deploy_timeout) for additional considerations.
