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

# Hypothetical
{: #hypothetical_detection}

Identifies the spans of text that are the object of a hypothetical statement. For example, a patient's record may include the statement `The doctor discussed the benefits of having an MRI performed`. It would be incorrect to say the patient has had an MRI since the sentence indicates the patient and doctor only talked about having an MRI. This statement would be identified as a hypothetical statement, therefore, the user of the hypothetical annotator could choose to process annotations within that span differently. Another example could be `the patient's father had diabetes`. This isn't stating the patient has diabetes, just that his father did have it. This is an example of a family history hypothetical span.
{:shortdesc}

The hypothetical annotator makes use of words or word phrases called <q>triggers.</q> When a trigger is found in text being analyzed, the phrase is tagged as being a potential hypothetical span. In the two examples above, the trigger terms are `discussed` and `father`.  Internal to the hypothetical annotator are two dictionaries of these trigger words: hypothetical triggers and family history triggers. Examples from the hypothetical triggers dictionary include `suspected`, `talked about`, and `scheduled for`. Likewise, the internal family history triggers dictionary contains familial terms such as `sister`, `mother`, `brother`, etc.  Either of these dictionaries can be customized using the Domain Expert Tool.  See the [Customizing](wh-acd?topic=wh-acd-customizing#customizing) section for more information.

When the hypothetical annotator is used, it updates annotations that currently exist in the unstructured container with a hypothetical field either `hypothetical=true` or `hypothetical=false` based on span of the annotation in the container and the span of the identified HypotheticalSpans. When `hypothetical=true`, an additional feature, *hypotheticalType*, is added to indicate the type hypothetical span - `HypotheticalSpan` or `FamilyHistorySpan`. Run the hypothetical annotator after all other annotators to be processed in order to generate hypothetical spans.

#### Annotation Types

* HypotheticalSpan

#### Configurations

<table>
<tr>
<th>Configuration</t>
<th>Values</th>
<th>Description</th>
</tr>
<tr>
<td>remove_hypothetical</td>
<td>true/false</td>
<td>When true, any medical concepts deemed hypothetical from the surrounding context will be truncated from the response. When false <i>(default)</i>, medical concepts deemed hypothetical will not be truncated from the response.</td>
</tr>
<tr>
<td>include_family_history</td>
<td>true/false</td>
<td>When true, the family history annotations will be included as part of hypothetical spans in the response. When false <i>(default)</i>, family history annotations will not be included in the response. For example, <q>his father has diabetes</q> will be annotated and included in the hypothetical span in the response when true.</td>
</tr>
</table>

#### HypotheticalSpan

<table>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>HypotheticalSpan or FamilyHistorySpan</td></tr>
<tr><td>trigger</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>coveredText</td><td>The text that initiated the hypothetical clause.</td></tr>
  <tr><td>source</td><td>The name of the whitelist dictionary in which the trigger resides. The name will be <q>internal</q> if the trigger resides in the internally shipped dictionary.</td></tr>
</tbody></table></td></tr>
</table>

### Sample Response

Sample response from the hypothetical annotator for the text: `We discussed the pros and cons of chemotherapy.`

```{
  "unstructured": [
    {
      "text": "We discussed the pros and cons of chemotherapy.",
      "data": {
        "concepts": [

          ...

          {
            "cui": "C3665472",
            "preferredName": "Chemotherapy",
            "semanticType": "topp",
            "source": "umls",
            "sourceVersion": "2018AA",
            "type": "umls.TherapeuticOrPreventiveProcedure",
            "begin": 34,
            "end": 46,
            "coveredText": "chemotherapy",
            "hypothetical": true,
            "hypotheticalType": "HypotheticalSpan",
            "loincId": "LA6172-6,MTHU010425",
            "nciCode": "C15632",
            "snomedConceptId": "367336001,363688001",
            "vocabs": "LNC,MTH,CSP,NCI_NCI-GLOSS,LCH,CHV,CCS,MEDLINEPLUS,LCH_NW,NCI,AOD,SNOMEDCT_US,PDQ"
          }
        ],
        "hypotheticalSpans": [
          {
            "type": "HypotheticalSpan",
            "begin": 0,
            "end": 46,
            "coveredText": "We discussed the pros and cons of chemotherapy",
            "trigger": [
              {
                "begin": 3,
                "end": 12,
                "coveredText": "discussed",
                "source": "internal"
              }
            ]
          }
        ]
      }
    }
  ]
}```
