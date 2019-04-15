<h3 id="hypothetical">Hypothetical</h3>

Identifies the spans of text that are the object of a hypothetical statement. For example, a patient's record may include the statement <q>The doctor discussed the benefits of having an MRI performed.</q> It would be incorrect to say the patient has had an MRI since the sentence indicates the patient and doctor only talked about having an MRI. This statement would be identified as a hypothetical statement, therefore, the user of the hypothetical annotator could choose to process annotations within that span differently. Another example could be <q>the patient's father had diabetes.</q> This isn't stating the patient has diabetes, just that his father did have it. This is an example of a family history hypothetical span.

In simple terms, the hypothetical annotator makes use of words or word phrases called <q>triggers.</q> When a trigger is found in text being analyzed, the phrase is tagged as being a potential hypothetical span. In the two examples above, the trigger terms are <q>discussed</q> and <q>father,</q> respectively. Internal to the hypothetical annotator are two dictionaries of these trigger words: hypothetical triggers and family history triggers. Examples from the hypothetical triggers dictionary include <q>suspected,</q> <q>talked about,</q> and <q>scheduled for.</q> Likewise, the internal family history triggers dictionary contains familial terms such as <q>sister,</q> <q>mother,</q> <q>brother,</q> etc. Using custom dictionaries (whitelists), either of these dictionaries may be augmented to include alternate spellings, additional terms, and regional colloquialisms as necessary. See the section on Whitelists for more information.

When the hypothetical annotator is used, it updates annotations that currently exist in the unstructured container with a hypothetical flag either <q>hypothetical=true</q> or <q>hypothetical=false</q> based on span of the annotation in the container and the span of the identified HypotheticalSpans. When hypothetical=true, an additional feature, <q>hypotheticalType,</q> is added to indicate that the hypothetical span is a <q>HypotheticalSpan</q> or a <q>FamilyHistorySpan.</q> Run the hypothetical annotator after all other annotators to be processed in order to generate hypothetical spans.

Note: Due to the nature of how the Hypothetical annotator works, see Hypothetical and Negation Annotator Filtering section below for information on how best to use filtering functionality with this annotator.

<h4>Annotation Types</h4>

* HypotheticalSpan

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
<tr>
<th>Configuration</t>
<th>Values</th>
<th>Description</th>
</tr>
<tr>
<td>remove_hypothetical</td>
<td>true/false</td>
<td>When true, any medical concepts deemed hypothetical from the surrounding context will be truncated from the response. When false _(default)_, medical concepts deemed hypothetical will not be truncated from the response.</td>
</tr>
<tr>
<td>include_family_history</td>
<td>true/false</td>
<td>When true, the family history annotations will be included as part of hypothetical spans in the response. When false _(default)_, family history annotations will not be included in the response. For example, <q>his father has diabetes</q> will be annotated and included in the hypothetical span in the response when true.</td>
</tr>
</table>

###### HypotheticalSpan

<table>
<caption>HypotheticalSpan</caption>
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
