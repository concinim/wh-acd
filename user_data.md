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

# User Data Deletion
{: #user_data}

The ACD service enables you to delete all data that is associated to a specific tenant.
{:shortdesc}

The method has no effect if no data is associated with the customer ID.
You must issue the request with credentials for the same instance of the service that was used to associate the customer ID with the data.

Every ACD request is, by default, associated with a tenant id.
A default tenant id is assigned if no tenant id is supplied in a request.
This deletion operation is only allowed for a specific tenant id and is not permitted for a default tenant.
Use the DELETE /v1/user_data method to delete all data that is associated with a specified tenant id; see Deleting data.
The following example deletes all data for the customer ID my_ID:

```console
curl -X DELETE
http://host/services/clinical_data_annotator/api/v1/user_data
```

The DELETE /v1/user_data method deletes all data that is associated with the specified tenant ID, regardless of the method by which the information was added.
