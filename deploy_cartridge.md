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

## Cartridge deployment scenario:

1.  The consumer uses the {{site.data.keyword.wh-acd_short}} Configuration Editor to create a new cartridge (or modify an existing one) and customizes the contents (artifacts) of the cartridge to their domain.
2.  Next, using the configuration editor, the consumer will **Export** the cartridge in order to save a snapshot of the cartridge to their computer.
3.  Lastly, the consumer deploys the cartridge snapshot (a zip file) to  {{site.data.keyword.wh-acd_short}} using _POST /v1/deploy_ API. In the following curl example, the consumer's cartridge file is `./my_cartridges/name_of_cartridge_file.zip`, and `update=false` means do not update the resource if it already exists with the {{site.data.keyword.wh-acd_short}} service.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for requests within the Watson Platform for Health
curl -X POST --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" -F "archive_file=@./my_cartridges/name_of_cartridge_file.zip" "http://host/services/clinical_data_annotator/api/v1/deploy?update=false&version=2018-01-17"
```

* A successful cartridge deploy will result in <q>201 Created</q> if it is a new resource, or <q>200 OK</q> if `update=true` was specified and the existing resource was updated.

**Note:** some large cartridge deployments can exceed the request timeout thresholds defined in the DataPower gateways (usually after 2 mins). In that event, you may receive the following error response:

```javascript
{
  "httpCode":"500",
  "httpMessage":"Internal Server Error",
  "moreInformation":"Failed to establish a backside connection"
}
```

This timeout occurs outside of  {{site.data.keyword.wh-acd_short}} and does not prevent your cartridge from being successfully deployed. You just won't get the itemized response confirming successful deployment of each individual artifact within your cartridge. If your cartridge deployment request times out, here are steps you can take to verify successful deployment after giving the process about 15 minutes to complete.

* For initial deployment of a cartridge, you can look for the creation of the annotator flow to determine whether deployment has completed. The annotator flow is the last artifact created during the deployment process and its existence signals completion of deployment in the initial deployment of a cartridge.

Sample request to retrieve flows for your tenant, for verifying completion of initial cartridge deployment:

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for requests within the Watson Platform for Health
curl -X GET --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" "http://host/services/clinical_data_annotator/api/v1/flows?version=2018-02-14"
```

* For updates to a previously deployed cartridge and to verify successful deployment of a cartridge in general upon a deployment request timeout, run some sample text through the _POST /v1/analyze_ API and verify that the response adheres to the configurations defined within your cartridge.
