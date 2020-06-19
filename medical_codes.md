---

copyright:
  years: 2019
lastupdated: "2019-04-16"

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

# Medical Codes
{: #medical_codes}

{{site.data.keyword.wh-acd_short}} normalizes medical concepts into many common medical codes.  The following table shows the medical code support for each annotator available in  {{site.data.keyword.wh-acd_short}}.

<table summary="common medical codes">
  <tr>
    <th scope="col" style="width:100%; min-width:0 !important">Medical Codes</th>
    <th scope="col" style="width:1%; min-width:0 !important">NCI</th>
    <th scope="col" style="width:1%; min-width:0 !important">ICD 9/10</th>
    <th scope="col" style="width:1%; min-width:0 !important">LOINC</th>
    <th scope="col" style="width:1%; min-width:0 !important">MeSH</th>
    <th scope="col" style="width:1%; min-width:0 !important">RxNorm</th>
    <th scope="col" style="width:1%; min-width:0 !important">SNOMED CT</th>
    <th scope="col" style="width:1%; min-width:0 !important">CPT</th>
    <th scope="col" style="width:1%; min-width:0 !important">CCS</th>
    <th scope="col" style="width:1%; min-width:0 !important">HCC</th>
    <th scope="col" style="width:1%; min-width:0 !important">UMLS CUI</th>
  </tr>

  <tr>
    <th scope="row" colspan="11" width="1%"><b>Turn Key Annotators</b></th>
  </tr>
  <tr><td scope="row" >Allergy</td> <td></td> <td></td> <td></td> <td></td> <td>✔</td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td scope="row" >Cancer</td> <td></td> <td>✔</td> <td></td> <td></td> <td></td> <td>✔</td> <td></td> <td>✔</td> <td>✔</td> <td>✔</td>   </tr>
  <tr><td scope="row" >Ejection Fraction</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td scope="row" >Lab Value</td> <td></td> <td></td> <td>✔</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td scope="row" >Living Assistance</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td scope="row" >Medication</td> <td></td> <td></td> <td></td> <td></td> <td>✔</td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td scope="row" >Named Entities</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>   </tr>
  <tr><td scope="row" >Procedure</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td>✔</td> <td></td> <td></td> <td>✔</td>   </tr>
  <tr><td scope="row" >Symptom Disease</td> <td></td> <td>✔</td> <td></td> <td></td> <td></td> <td>✔</td> <td></td> <td>✔</td> <td>✔</td> <td>✔</td>   </tr>

  <tr><th scope="row" ></th></tr>
  <tr>
    <th scope="row" colspan="11"><b>Configurable Concept Annotators</b></th>
  </tr>
  <tr><td scope="row" >Attribute</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td>   </tr>
  <tr><td scope="row" >Concept (UMLS 2018AA+)</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td> <td>✔</td> <td></td> <td></td> <td>✔</td>   </tr>
  <tr><td scope="row" >Concept Value</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td>✔</td></tr>
  <tr><td scope="row" >Relation</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>

  <tr><th scope="row" ></th></tr>
  <tr>
    <th scope="row" colspan="11"><b>Cotextual Annotators</b></th>
  </tr>
  <tr><td scope="row" >Disambiguation</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>
  <tr><td scope="row" >Hypothetical</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>
  <tr><td scope="row" >Negation</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>
  <tr><td scope="row" >Section</td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td> <td></td>  <td></td></tr>

</table>
