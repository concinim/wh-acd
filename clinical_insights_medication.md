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

# Clinical Insights Medication Model
{: #clinical_insights_medication}


The medication model provides information about how the medication applies to the patient and lifecycle events.

The usage section of the JSON response indicates how a medication applies to a patient.

<h4>usage</h4>

<table>
<tr><th>__Field__</th><th>__Description__</th></tr>
</tr><td>takenScore</td><td>Is there evidence that the given medication is currently being taken by the patient, has ever been taken by the patient, or there is a firm plan to put the patient on that medication.</td></tr>
<tr><td>consideringScore</td><td>Is the medication being considered as an option for the patient.</td></tr>
<tr><td>discussedScore</td><td>Other mentions of the medication that don't directly apply to the patient.</td></tr>
<tr><td>labMeasurementScore</td><td>The medication mention is a lab measurement and does not directly indicate a medication the patient is taking.</td></tr>
</table>

The medication model also provides information about lifecycle events - *start*, *stopped*, *dose changed*, and *adverse events*.

Each event has the following scores:

<table>
<tr><th>__Field__</th><th>__Description__</th></tr>
</tr><td>score</td><td>How strongly does the language around the candidate annotation look like it matches the given lifecycle event.</td></tr>
<tr><td>usage</td><td>The text that triggered the negation. For example, in the text <q>She denies pain</q>, the trigger is <q>denies</q>.
<table role="presentation"><tbody>
  <tr><td>explicitScore</td><td>Does the event directly apply to the patient</td></tr>
  <tr><td>consideringScore</td><td>Is the event something that may happen to the patient</td></tr>
  <tr><td>discussedScore</td><td>Does the event not apply to the patient</td></tr>
</tbody></table></td></tr>
</table>

Note that the lifecycle events only look at local clues and do not try to reason across extremely large spans or multiple documents.  

* startedEvent - Is there language that indicates a medication was started.
* stoppedEvent - Is there language that a medication was stopped.
* doseChangedEvent - Is there language that indicates the dosage of a medication was changed.
* adverseEvent - Does the medication mention have a causal relationship with any sort of bad outcome for the patient.  In addition to a *score* and *usage* section, adverseEvent also has an *allergyScore* that indicates if the given AE is just an allergy mention.

You can use the usage scores to carve very specific boundaries around the kinds of medication mentions that you surface in your application.  For example, depending on your use case, you may want to know about when a dose change occurred, but not when it was considered.

### Sample Response

Consider the following sample text.

_We will think about putting her on Metformin if her A1C remains high._

The clinical insight features for Metformin might look as follows:

```
"insightModelData": {
	"medication": {
		"usage": {
			"takenScore": 0.005,
			"consideringScore": 0.994,
			"discussedScore": 0,
			"labMeasurementScore": 0
		},
		"startedEvent": {
			"score": 0.998,
			"usage": {
				"explicitScore": 0.002,
				"consideringScore": 0.997,
				"discussedScore": 0
			}
		},
		"stoppedEvent": {
			"score": 0,
			"usage": {
				"explicitScore": 0,
				"consideringScore": 0,
				"discussedScore": 0
			}
		},
		"doseChangedEvent": {
			"score": 0,
			"usage": {
				"explicitScore": 0,
				"consideringScore": 0,
				"discussedScore": 0
			}
		},
		"adverseEvent": {
			"score": 0,
			"allergyScore": 0,
			"usage": {
				"explicitScore": 0,
				"consideringScore": 0,
				"discussedScore": 0
			}
		}
	}
}
```
