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

# Negation
{: #negation_detection}

Identifies the spans of text that are the object of a negation and also identifies the text that triggered the negation. When this annotator is run it updates annotations that currently exist in the unstructured container with a negated flag either <q>negated=true</q> or <q>negated=false</q> based on span of the annotation in the container and the span of the identified NegatedSpans. You should run this annotator after all annotators that you would like to be processed for negation.
{:shortdesc}

Note: Due to the nature of how the Negation annotator works, see Hypothetical and Negation Annotator Filtering section below for information on how best to use filtering functionality with this annotator.

<h4>Annotation Types</h4>

* NegatedSpan

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
<tr>
<th>Configuration</th>
<th>Values</th>
<th>Description</th>
</tr>
<tr>
<td>fully_covered</td>
<td>true/false</td>
<td>When true <i>(default)</i>, an annotation must be fully covered by a negated span to be marked negated. If false, the annotation will be considered negated if any part of it overlaps with a negated span.</td>
</tr>
<tr>
<td>remove_negated</td>
<td>true/false</td>
<td>When false <i>(default)</i>, an annotation will be kept although they are detected to be negated. If true, the negated annotation will be removed</td>
</tr>
</table>

<h4>NegatedSpan</h4>


<table>
<caption>NegatedSpan</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>NegatedSpan</td></tr>
<tr><td>trigger</td><td><table role="presentation"><tbody>
  <tr><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
  <tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
  <tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
  <tr><td>type</td><td>trigger</td></tr>
</tbody></table></td></tr>
</table>
