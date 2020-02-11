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

# Clinical Insights
{: #clinical_insights}

The {{site.data.keyword.wh-acd_short}} provides an out of the box capability to extract contextual information about key concept types in clinical notes about a patient.  The clinical insights function is composed of two core capabilities:

1. A set of models that provide contextual features for key clinical types (medication, diagnosis, and procedure).
2. An out of the box cartridge uses those features to answer a simple question - does this entity apply to the patient?

<h4>Models</h4>

Each of the models provides specific contextual information that is important to the given annotation type.  The models can operate on existing annotations and add additional type specific contextual features.  The annotations the models operate on can either come from annotators that ship with {{site.data.keyword.wh-acd_short}} or with custom annotations you create using the {{site.data.keyword.wh-acd_short}} Configuration Editor.  There are currently models for the following:

1. Medication
2. Diagnosis
3. Procedure
<br>
<h4>Medication</h4>

The medication model provides information about medication usage and lifecycle events.

The usage section of the JSON response indicates how a medication applies to a patient.

<h4>usage</h4>

<table>
<tr><th>__Field__</th><th>__Description__</th></tr>
</tr><td>takenScore</td><td>Is there evidence that the given medication is currently being taken by the patient, has ever been taken by the patient, or there is a firm plan to put the patient on that medication.</td></tr>
<tr><td>consideringScore</td><td>Is the medication being considered as an option for the patient.</td></tr>
<tr><td>discussedScore</td><td>Other mentions of the medication that don't directly apply to the patient</td></tr>
<tr><td>labMeasurementScore</td><td>The medication mention is a lab measure</td></tr>
</table>

The medication model also provides information about lifecycle events - start, stopped, dose changed, and adverse events.

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

startedEvent - Is there language that indicates a medication was started.
stoppedEvent - Is there language that a medication was stopped.
doseChangedEvent - Is there language that indicates the dosage of a medication was changed.
adverseEvent - Does the medication mention have a causal relationship with any sort of bad outcome for the patient.  In addition to a *score* and *usage* section, adverseEvent also has an *allergyScore* that indicates if the given AE is just a simple allergy mention.

You can use the usage scores to carve very specific boundaries around the kinds of medication mentions that you surface in your application.  For example, depending on your use case, you may want to know about when a dose change occurred, but not when it was considered.

<h4>Diagnosis</h4>

The diagnosis model provides usage information and other features that let you decide which diagnosis mentions matter the most.

<h4>usage</h4>

<table>
<tr><th>__Field__</th><th>__Description__</th></tr>
<tr><td>usage</td><td>The text that triggered the negation. For example, in the text <q>She denies pain</q>, the trigger is <q>denies</q>.
<table role="presentation"><tbody>
</tr><td>explicitScore</td><td>The diagnosis applies to the patient and the doctor is stating it.</td></tr>
<tr><td>implicitScore</td><td>The language around the diagnosis applies to the patient, but is being reported by the patient instead of the physician.</td></tr>
<tr><td>discussedScore</td><td>Any other diagnosis mention that does not apply to the patient</td></tr>
</tbody></table></td></tr>

</tr><td>suspectedScore</td><td>Does the language around the diagnosis indicate that it is probable, but not necessarily confirmed.  Using this score in tandem with scores from the *usage* section allows you to calibrate how much certainty you want around a diagnosis mention.  </td></tr>
</tr><td>symtpomScore</td><td>Is the diagnosis mention a symptom versus a primary condition</td></tr>
</tr><td>traumaScore</td><td>Does the diagnosis mention look like physical trauma</td></tr>
</tr><td>familyHistoryScore</td><td>Is the diagnosis mention a family history event that does not apply to the patient.</td></tr>

</table>
