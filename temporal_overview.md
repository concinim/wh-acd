---

copyright:
  years: 2020
lastupdated: "2020-10-28"

keywords: annotator clinical data, clinical data, annotation, temporal

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

# Temporal Overview (Experimental)
{: #temporal_overview}

{{site.data.keyword.wh-acd_short}} ships with an out-of-the-box capability for linking temporal mentions to concepts.  The temporal function is currently only exposed through [Clinical Insights](/docs/wh-acd?topic=wh-acd-clinical_insights_overview#clinical_insights_overview).  It will be made generally available for custom cartridges at a future date.

The {{site.data.keyword.wh-acd_short}} [demo application](https://acd-try-it-out.mybluemix.net/preview) allows you to see how temporal linking works.

![](images/demoAppTemporal.png)

At present, dates are linked to concepts surfaced by clinical insights by adding contextual features to the JSON for each linked concept.  Support for non-date temporal entities like durations and relative dates will be added later.


#### temporal

<table>
<tr><th>__Field__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The begin offset of the temporal trigger.</td></tr>
<tr><td>end</td><td>The end offset of the temporal trigger.</td></tr>
<tr><td>temporalType</td><td>Provides information about how temporal type the model things the temporal mention is.  Currently, _dateScore_ is the only score provided in this section.  Anything that scores sufficiently low as a date will not be surfaced.  For example, in the image above _2/10_ in the context of the patient's current pain level scores low as a date and is not surfaced. </td></tr>
</tr><td>relationType</td><td>Provides information about how the temporal mention relates to an entity.  Currently, _overlapsScore_ is the only relation type defined and it indicates how strongly the temporal mention is linked to the concept.</td></tr>
</table>


```
"begin": 585,
"end": 596,
"coveredText": "hip surgery",
"negated": false,
"insightModelData": {
     "procedure": {
         "usage": {
             "explicitScore": 0.999,
             "pendingScore": 0,
             "discussedScore": 0
         },
         "task": {
             "therapeuticScore": 1,
             "diagnosticScore": 0,
             "labTestScore": 0,
             "surgicalTaskScore": 0,
             "clinicalAssessmentScore": 0
         },
         "type": {
             "deviceScore": 0,
             "materialScore": 0,
             "medicationScore": 0,
             "procedureScore": 1,
             "conditionManagementScore": 0
         }
     }
 },
 "temporal": [
     {
         "begin": 600,
         "end": 604,
         "coveredText": "5/17",
         "temporalType": {
             "dateScore": 1
         },
         "relationTypes": {
             "overlapsScore": 0.996
         }
     }
 ]
```

Note that multiple temporal links can be created for a concept.  For example, given the following text:

_PMH: Patient had bariatric revision surgery in April 1999 and again in July 2003, knee replacement in 2011, and underwent arthroscopic surgery on her shoulder in 2016._

The temporal section for _revision surgery_ would have two associated dates.

```        
"temporal": [{
		"begin": 47,
		"end": 57,
		"coveredText": "April 1999",
		"temporalType": {
			"dateScore": 1
		},
		"relationTypes": {
			"overlapsScore": 0.988
		}
	},
	{
		"begin": 71,
		"end": 80,
		"coveredText": "July 2003",
		"temporalType": {
			"dateScore": 1
		},
		"relationTypes": {
			"overlapsScore": 0.923
		}
	}
]
```
