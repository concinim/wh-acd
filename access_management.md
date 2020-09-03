---

copyright:
  years: 2017, 2019
lastupdated: "2020-0903"

keywords: annotator clinical data, clinical data, annotation, certificates, SSL

subcollection: wh-acd

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}

# Managing Access Roles
{: #managing-access-roles}

You can secure services within {{site.data.keyword.cloud_notm}} by allowing only users with specified access roles to complete certain actions.
{: shortdesc}

## Platform access roles
{: #platform-access-roles}

You can use platform access roles to enable users to complete tasks on platform resources, such as provisioning or de-provisioning instances in your {{site.data.keyword.cloud_notm}} account.

<table>
<caption> Table 1. Actions that are mapped to platform access roles</caption>
  <tr>
    <th> Action </th>
    <th> Role </th>
  </tr>
  <tr>
    <td>View instances of {{site.data.keyword.wh-acd_short}}</td>
    <td> Administrator, Operator, Editor </td>
  </tr>
  <tr>
    <td>Provosion an instance of {{site.data.keyword.wh-acd_short}}</td>
    <td> Administrator, Editor </td>
  </tr>
  <tr>
    <td>De-provosion an instance of {{site.data.keyword.wh-acd_short}}</td>
    <td> Administrator, Editor </td>
  </tr>
</table>

## Service access roles
{: #service-access-roles}

You can use service access roles to enable users to perform service actions in the form of HTTP requests.

<table>
<caption> Table 2. Actions that are mapped to service access roles</caption>
  <tr>
    <th> Action </th>
    <th> Role </th>
  </tr>
  <tr>
    <td>GET /wh-acd </td>
    <td> Manager, Writer, Reader </td>
  </tr>
  <tr>
    <td> POST /analyze </td>
    <td> Manager, Writer, Reader </td>
  </tr>
  <tr>
    <td> POST/PUT/DELETE /flow and /profiles</td>
    <td> Manager, Writer </td>
  </tr>
  <tr>
    <td> POST/PUT /deploy and /cartridges </td>
    <td> Manager, Writer </td>
  </tr>
  <tr>
     <td> DELETE /user_data </td>
     <td> Manager</td>
  </tr>       
</table>

For more information about user roles and permissions, see [User roles](/docs/iam?topic=iam-userroles#userroles).
