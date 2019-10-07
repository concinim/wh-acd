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

# Cartridge Deployment
{: #deploy_cartridges}

1. The consumer uses the [Domain Expert Tool (DET)](https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/) to create a new cartridge (or modify an existing one) and customizes the contents (artifacts) of the cartridge to their domain.
2. Next, using the DET, the consumer will **Export** the cartridge in order to save a snapshot of the cartridge.
3. The consumer deploys the cartridge snapshot (a zip file) to  {{site.data.keyword.wh-acd_short}} using _POST /v1/cartridges_ API.  In the following curl example, the consumer's cartridge file is `/path/to/name_of_cartridge_file.zip`. A successful request for creating a cartridge will response in <q>202 ACCEPTED</q> and will include the path to the resource, e.g., /v1/cartridges/cartridge_id in the response body and the response header. The resource path can be used in _GET /v1/cartridges/catridgeId API to obtain the overall deployment status.

Multiple deployment of the same cartridges should initially use POST operation and, subsequently, use PUT operations. Deployment of the same cartridges using POST multiple times will result in <q>409 CONFLICT</q> .

```Curl
 curl -X POST -u "apikey":"{apikey}" \
 --header "Content-Type:application/octet-stream" \
 --header "Accept:application/json" \
 --data-binary @/path/to/name_of_cartridge_file.zip \
 "{url}/v1/cartridges?vesion=2019-09-01"
```

4. The consumer updates the cartridge snapshot using _PUT /v1/cartridges_ API. The cartridges id is not required in the path parameter and is extracted directly from the zip file. A successful request for updating the cartridge deployment will result in <q>202 ACCEPTED</q> and will include the path to the resource, e.g., /v1/cartridges/cartridge_id in the response body and the response header.

```Curl
curl -X PUT -u "apikey":"{apikey}" \
--header "Content-Type:application/octet-stream" \
--header "Accept:application/json" \
--data-binary @/path/to/name_of_cartridge_file.zip \
"{url}/v1/cartridges?vesion=2019-09-01"
```

Updating a cartridge deployment assumes that the cartridge has been previously deployed. The consumer creates an initial deployment with the POST operation and subsequent deployment uses the PUT operation. Updating a cartridge deployment with missing or empty deployment status will return with <q>404 Not Found</q>.  

5.  The consumer retrieves all deployment status using _GET /v1/cartridges_ API, which include all cartridge deployed for a specific tenant. An empty list is returned if no catridge has been deployed.  

```Curl
curl -X GET -u "apikey":"{apikey}" \
--header "Accept:application/json" \
"{url}/v1/cartridges?version=2019-09-01"
```

6.  The consumer can view the contents of a specific deployment by invoking the _GET /v1/cartridges_ API with the cartridge ID supplied as the path parameter . If the supplied ID does not exists, then a response  <q> 404 Not Found </q> is returned. The following curl command returns the deployment status of the cartridge_id.

```Curl
curl -X GET -u "apikey":"{apikey}" \
--header "Accept:application/json" \
"{url}/v1/cartridges/cartridge_id?version=2019-09-01"
```

Replace `{apikey}` and `{url}` with the actual API key and URL in all sample codes above.
