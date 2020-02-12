---

copyright:
  years: 2020
lastupdated: "2020-02-11"

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

# Clinical Insights Procedure Model
{: #clinical_insights_procedure}

The procedure model provides information about how the procedure applies to the the patient and other features that let you focus on the procedure annotations that matter most to your application.

<h4>usage</h4>

<table>
<tr><th>__Field__</th><th>__Description__</th></tr>
</tr><td>explicitScore</td><td>There is evidence that the a procedure has been done or there is a firm plan to do it.</td></tr>
<tr><td>pendingScore</td><td>Language around the procedure indicates that is has been scheduled or is highly recommended by a physician.</td></tr>
<tr><td>discussedScore</td><td>Other mentions of the procedure that do not directly apply to the patient</td></tr>
</table>


<h4>task</h4>

<table>
<tr><th>__Field__</th><th>__Description__</th></tr>
</tr><td>therapeuticScore</td><td>Is this a therapeutic procedure</td></tr>
<tr><td>diagnosticScore</td><td>Is this a diagnostic procedure</td></tr>
<tr><td>surgicalTaskScore</td><td>Is this a subtask as part of a larger surgical process</td></tr>
<tr><td>clinicalAssessmentScore</td><td>Is this a physical evaluation of a patient</td></tr>
</table>

<h4>type</h4>

<table>
<tr><th>__Field__</th><th>__Description__</th></tr>
</tr><td>deviceScore</td><td>Does the procedure involve an implanted device</td></tr>
<tr><td>materialScore</td><td>Does the procedure involve grafts or other material implants</td></tr>
<tr><td>medicationScore</td><td>Does the procedure primarily involve administration of a medication </td></tr>
<tr><td>conditionManagementScore</td><td>Is this an ongoing procedure to manage a long term condition</td></tr>
<tr><td>procedureScore</td><td>Catchall score for everything else</td></tr>
</table>

### Sample Response

Consider the following sample text.

_Chemotherapy with Cisplatin was not an option for his type of cancer._

```
"insightModelData": {
	"procedure": {
		"usage": {
			"explicitScore": 0.097,
			"pendingScore": 0.043,
			"discussedScore": 0.859
		},
		"task": {
			"therapeuticScore": 0.999,
			"diagnosticScore": 0,
			"surgicalTaskScore": 0.001,
			"clinicalAssessmentScore": 0
		},
		"type": {
			"deviceScore": 0,
			"materialScore": 0,
			"medicationScore": 0.994,
			"procedureScore": 0.005,
			"conditionManagementScore": 0
		}
	}
}
```
