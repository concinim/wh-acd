<h3 id="section">Sections</h3>

The section annotator is used to identify the section of a document where unstructured text is found. For example, a patient's discharge summary may contain a <q>Family History</q> section identifying medical diagnoses of the patient's parents. In some instances, this information may not be relevant for a particular use case. Using the section annotator, annotations identified as belonging to the <q>Family History</q> section may be filtered out.

Like the hypothetical and negation annotators, the section annotator makes use of words or word phrases called <q>triggers.</q> An internal set of these triggers is built using LOINC (Logical Observation Identifiers Names and Codes).  The internal section trigger list can be viewed in the Domain Expert Tool (DET) by searching for the dictionary named **Section Triggers**. This dictionary would be helpful if you would like to filter out some of the internally found sections.  A custom dictionary for Section may be used to include additional section triggers and additional trigger spellings as necessary. For more information about custom dictionaries, see Whitelists section.

In addition to triggers, section headings are also identified based on a few simple formatting rules:
1. If a heading is in all uppercase letters followed by a <q>:</q>, such as <q>VACCINES:</q>, the heading will be treated as a section trigger whether or not it is in an internal trigger dictionary or a custom section trigger dictionary.
2. by default, if a section trigger term is found and is not at the beginning of a line, that term is not treated as a section trigger. This default functionality can be changed using the sections_can_start_anywhere configuration option detailed below.
3. If a term exists in either the internal section dictionary or a custom section dictionary, and it is followed or preceded by all uppercase letters (with <q>/</q> in between), both the term and the uppercase portion is considered the section trigger. If uppercase letters follow the dictionary entry, the uppercase portion may include parentheses. Examples include <q>RELEVANT/FamilyHistory:</q> and <q>Family History/(RELEVANT):</q>.

The section annotator needs to be placed in the flow before any annotators that you would like to contain section information.  The Domain Expert Tool (DET) will place the section annotator first in the flow by default. The individual annotators that run after the section annotator will then be augmented with the <q>sectionNormalizedName</q> and <q>sectionSurfaceForm</q> features for all annotations that fall within a section.  Filters can be added to the individual annotators to remove annotations based on the section features.

One common task with the section information would be to filter all of the annotations of a certain type out of the container.  For example, you may not want annotations in the Family History section to be processed.   The following example filter will remove any symptomDisease annotations in the Family history section.  It is important to note that you need to test for the existence of the section feature and for the section feature value.

```javascript
{
    "filters": [
        {
            "name": "myfilter",
            "target": "unstructured.data.SymptomDiseaseInd",
            "condition": {
                "type": "all",
                "conditions": [
                    {
                        "type": "any",
                        "label": "Include Conditions"
                    },
                    {
                        "type": "notAny",
                        "label": "Exclude Conditions",
                        "conditions": [
                            {
                                "type": "all",
                                "conditions": [
                                    {
                                        "type": "match",
                                        "field": "sectionNormalizedName",
                                        "not": false,
                                        "operator": "fieldExists",
                                        "values": [],
                                        "caseInsensitive": false
                                    },
                                    {
                                        "type": "match",
                                        "field": "sectionNormalizedName",
                                        "not": false,
                                        "operator": "equals",
                                        "values": [
                                            "family history"
                                        ],
                                        "caseInsensitive": false
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    ]
}
```

<h4>Annotation Types</h4>

* Section

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
<tr>
<th>Configuration</t>
<th>Values</th>
<th>Description</th>
</tr>
<tr>
<td>include_covered\_text</td>
<td>true/false</td>
<td>When true, the coveredText feature for the section annotation is returned. When false _(default)_, the coveredText feature is not returned.</td>
</tr>
<tr>
<td>turn_off_internal\_triggers</td>
<td>true/false</td>
<td>When true, the internal trigger dictionaries are not used. When false _(default)_, the internal dictionaries are used as base for finding sections.  Section Whitelists can be used in either scenario.</td>
</tr>
<tr>
<td>sections_can_start\_anywhere</td>
<td>true/false</td>
<td>When true, section triggers can be located in any portion of the text, not just at the beginning of a line. When false _(default)_, section triggers are only considered when beginning a line.</td>
</tr>
</table>

###### Section

<table>
<caption>Section</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>Annotation type for Section</td></tr>
<tr><td>trigger</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>coveredText</td><td>The text that initiated the section annotation.</td></tr>
  <tr><td>source</td><td>The name of the whitelist dictionary in which the trigger resides. The name will be <q>internal</q> if the trigger resides in the internally shipped dictionary.</td></tr>
</tbody></table></td></tr>
</table>
