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

# Clinical Insights Diagnosis Model
{: #clinical_insights_diagnosis}


The diagnosis model provides usage information and other features that let you decide which diagnosis mentions matter the most.

The usage section of the JSON response indicates how a diagnosis applies to the patient.

<h4>usage</h4>

<table>
<tr><th>__Field__</th><th>__Description__</th></tr>

</tr><td>explicitScore</td><td>The physician is stating that the diagnosis applies to the patient.</td></tr>
<tr><td>implicitScore</td><td>The diagnosis applies to the patient but is reported by the patient instead of the physician.</td></tr>
<tr><td>discussedScore</td><td>Any other diagnosis mention that does not apply to the patient</td></tr>
</table>

<h4>Other diagnosis features</h4>
<table>
<tr><th>__Field__</th><th>__Description__</th></tr>
</tr><td>suspectedScore</td><td>Does the language around the diagnosis indicate that it is probable, but not necessarily confirmed.  Using this score in tandem with scores from the *usage* section allows you to calibrate how much certainty you want around a diagnosis mention.  </td></tr>
</tr><td>symtpomScore</td><td>Is the diagnosis mention a symptom versus a primary condition</td></tr>
</tr><td>traumaScore</td><td>Does the diagnosis mention look like physical trauma</td></tr>
</tr><td>familyHistoryScore</td><td>Is the diagnosis mention a family history event that does not apply to the patient.</td></tr>
</table>
