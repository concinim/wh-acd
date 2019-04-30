---

copyright:
  years: 2017, 2019
lastupdated: "2019-04-18"

keywords: certificates, SSL,

subcollection: certificate-manager

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

# Managing service access roles
{: #managing-service-access-roles}

You can secure services within {{site.data.keyword.cloud_notm}} by allowing only users with specified access roles to complete certain actions.
{: shortdesc}

## Platform access roles
{: #platform-access-roles}

You can use platform access roles to enable users to complete tasks on platform resources, such as creating or deleting instances in your {{site.data.keyword.cloud_notm}} account.

<table>
<caption> Table 1. Actions that are mapped to platform access roles</caption>
  <tr>
    <th> Action </th>
    <th> Role </th>
  </tr>
  <tr>
    <td>View instances of {{site.data.keyword.wh-acd_short}}</td>
    <td> Administrator, Operator, Editor, Viewer </td>
  </tr>
  <tr>
    <td>Create an instance of {{site.data.keyword.wh-acd_short}}</td>
    <td> Administrator, Editor </td>
  </tr>
  <tr>
    <td>Delete an instance of {{site.data.keyword.wh-acd_short}}</td>
    <td> Administrator, Editor </td>
  </tr>
</table>

## Service access roles
{: #service-access-roles}

You can use service access roles to enable users to complete tasks in {{site.data.keyword.wh-acd_short}} instances, such as importing, downloading, editing, or deleting certificates.

<table>
<caption> Table 2. Actions that are mapped to service access roles</caption>
  <tr>
    <th> Action </th>
    <th> Role </th>
  </tr>
  <tr>
    <td>List certificates</td>
    <td> Manager, Writer, Reader </td>
  </tr>
  <tr>
    <td>Download a certificate and private key </td>
    <td> Manager, Writer </td>
  </tr>
  <tr>
     <td>Get certificate metadata </td>
     <td> Manager, Writer, Reader </td>
  </tr>       
  <tr>
    <td>Update certificate's metadata</td>
    <td> Manager, Writer </td>
  </tr>
  <tr>
    <td>Import or reimport certificates, private keys, and intermediate certificates </td>
    <td> Manager </td>
  </tr>
  <tr>
    <td>Order a certificate </td>
    <td> Manager </td>
  </tr>  
  <tr>
    <td>Delete a certificate and private key </td>
    <td> Manager </td>
  </tr>
      <tr>
        <td>List all notification channels </td>
        <td> Manager, Writer, Reader </td>
      </tr>
   <tr>
     <td>Add, update, or delete a notification channel </td>
     <td> Manager </td>
   </tr>
     <tr>
       <td>Test a notification channel </td>
       <td> Manager, Writer, Reader </td>
     </tr>

</table>

For more information about user roles and permissions, see [User roles](/docs/iam?topic=iam-userroles#userroles).
