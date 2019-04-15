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

# Concept Disambiguation
{: #concept_disambiguation}

Determines the contextual validity of previously detected medical concepts (such as those identified by <a data-scroll="" href="wh-acd?topic=wh-acd-concept_detection#concept_detection">Concepts</a> based on the immediate sentence and document-level context. Disambiguation can act on any annotation with a cui field, given that cui field's values are known to disambiguation by being defined either in UMLS or else in a concept override as defined in the Json configuration section below.
{:shortdesc}

For example, consider the text _<q>Rain-on-snow and thaw-freeze events leading to ice formation on the ground may increase both in frequency and spatial extent.</q>_ Based on UMLS surface forms, concept_detection returns two different concepts over the word "ice": C0020746 (frozen water), and C0025611 (methamphetamine). It is disambiguation's job to use contextual clues to decide that in this context the frozen water concept is valid, and the methamphetamine concept is invalid.

Disambiguation requires a sufficient amount of context in order to evaluate the contextual validity of medical concepts. Therefore, the disambiguation annotator will assign a validity of NO_DECISION to concepts in documents with fewer than roughly 15 words. If you are leveraging disambiguation and you are seeing NO_DECISION, please check whether the word count in your document exceeds the aforementioned word count.

<h4>Overview</h4>

The way that disambiguation understands concepts and evaluates concepts is highly configurable, but in order to use the configuration options effectively, it's necessary to have a basic understanding of how disambiguation works.
Disambiguation operates in three steps.

**Step 1 - Scoring**: Disambiguation scores and optionally filters concepts according to how well a textual representation of the concept--a word or short phrase--fits in context. Concepts are scored by two models:

* **topic** model: This model is not aware of syntax and simply decides whether the concept representation makes sense topically inside a large window of surrounding text (about a paragraph or two).
* **semtype** model: This model is syntax aware and decides whether the concept's semantic type fits within the same window used by the sentence model. This model currently knows only about UMLS semantic types, linked to in the <a data-scroll=""  href="wh-acd?topic=wh-acd-concept_detection#concept_detection">Concepts</a> section.

**Step 2 - Preliminary judgment**: After scoring, the service makes an overall judgment about the validity of a concept, concluding either VALID, INVALID, or NO_DECISION based on a set of internal heuristics combining and thresholding model scores.

**Step 3 - Filters**: Finally, the model enforces a number of configurable filters that each have the potential to change concept judgments to INVALID.

* **competition** filter: concepts annotated over the same span are clustered according to the similarity of their textual representations as well as the compatibility of their semantic types. If overlapping concepts appear incompatible, then the lower scoring clusters are downranked to INVALID.
* **part-of-speech** filter: some concepts don't make sense over words with a particular part of speech. For example, the concept for burn injuries should not be annotated over proper nouns like <q>Mr. Burns.</q> Concepts violating a pre-specified set of part-of-speech rules are downranked to INVALID.

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
<tr>
<th>URL Configuration</th>
<th>Values</th>
<th>Description</th>
</tread>
<tr>
<td>debug</td>
<td>true/false</td>
<td>When true, details are returned alongside each VALID/INVALID judgment, including model scores, any configuration overrides affecting the concept, as well as comments indicating which filter, if any, caused the concept to be INVALID.</td>
</tr>
<tr>
<td>remove_invalid</td>
<td>true/false</td>
<td>When true, concepts with an INVALID judgment are removed from the response. Default is false.</td>
</tr>
<tr>
<td>longest_span</td>
<td>true/false</td>
<td>When false, disambiguation expects to see overlapping concepts, and will do extra work to handle them. The same value should be passed to concept_detection, if disambiguation is acting on its output. Default is true.</td>
</tr>
</table>

In addition to the url config params listed above, disambiguation can accept detailed configuration in the json container itself:

```javascript
{
  "annotatorFlows": [
    {
      "flow": {
        "elements": [
          {
            "annotator": {
              "name": "concept_detection"
            }
          },
          {
            "annotator": {
              "name": "disambiguation",
              "configurations": [
                {
                  "disambiguationConfig": {
            				"debug": false,
            				"removeInvalid": false,
            				"longestSpan": true,
            				"scoring": {"mode": ["topic","sentence","semtype"]},
            				"unknownConceptOverrides": [],
            				"conceptOverrides": [],
            				"competitionOverrides": []
                  }
                }
              ]
            }
          }
        ],
       "async": false
      }
    }
  ],
  "unstructured": [
    {
      "text": "Patient has lung cancer, but did not smoke. She may consider chemotherapy as part of a treatment plan."
    }
  ]
}
```

The following table contains a breakdown and description of the config options that are stubbed out in the request above.

<table>
<caption>Config Options</caption>
<tr><th>__Json Configuration__</th><th>__Description__</th></tr>
</tr><td>debug</td><td>Same as the URL param.</td></tr>
<tr><td>removeInvalid</td><td>Same as the URL param.</td></tr>
<tr><td>longestSpan</td><td>Same as the URL param.</td></tr>
<tr><td>scoring</td><td><table role="presentation"><tbody>
  <tr><td>mode</td><td>An array containing a subset of [<q>topic</q>, <q>sentence</q>, <q>semtype</q>]. This determines which model scores are used to decide whether the cui is valid or not. For example, if you are disambiguating data that is similar to medline, you should use the default behavior of all available models ([<q>topic</q>, <q>sentence</q>, <q>semtype</q>]), but if you are running on data which is not organized into syntactically coherent sentences (e.g., lab result summaries), you may wish to omit the sentence and semtype models and just use [<q>topic</q>]. To inspect model scores, enable debug mode. Note: conceptOverrides are defined as a field is inside of disambiguation's json config (as seen above), so they do not affect any other annotator in the pipeline.</td></tr>
</tbody></table></td></tr>

<tr><td>conceptOverrides</td><td>An array of objects that override the text and semantic types that disambiguation uses to score concepts. Each concept override must have a cui. The other fields are optional.<table role="presentation"><tbody>
  <tr><td>comment</td><td>Comment describing the purpose of the override. You can include multiple comments in the same object for multi-line comments. This is ignored by the service.</td></tr>
  <tr><td>cui (_required_)</td><td>The CUI to which the override applies. This may override a predefined concept (from UMLS, for example) or define a new custom concept.</td></tr>
  <tr><td>textRepresentations</td><td>An array of strings that specifies one or more text representations that disambiguation's topic and sentence models should use to score this concept. This overrides any text scraped automatically for this CUI (currently only done for UMLS concepts).</td></tr>
  <tr><td>semtypeOverrides</td><td>An array of strings listing semantic types which override those defined for this CUI in the source (UMLS, etc). These semantic types are used by the semtype model to score how well a cui's semantic type belongs in a given context. If set to <q>ignore</q>, then semtype model is not used to score this concept.</td></tr>
  <tr><td>posRules</td><td>An array of strings that defines conditions for annotating this concept based on the part of speech determined by an internal pos-tagging model. Valid parts of speech tags are a subset of XSG's tagset: [cord, nadj, subconj, noun, qual, propn, adv, det, pron, verb, thatconj, infto, conj, forto, adj, prep, special]. You may specify either positive parts-of-speech (e.g., [<q>noun</q>,<q>propn</q>]) which are OR'ed together, or disallowed parts-of-speech (e.g., [<q>!verb</q>, <q>!adj</q>]) which are AND'ed together.</td></tr>
  <!-- Leave this option out for the time being since in the context of ACD it's probably not the right way to blacklist concepts -->
  <!-- <tr><td>scoring</td><td><table role="presentation"><tbody> -->
  <!--   <tr><td>mode</td><td>An array of strings that currently can only contain the value <q>invalid</q> (more modes may be added later). This indicates that you want to specify that disambiguation should ALWAYS consider a given cui invalid. This may be somewhat redundant with the filters in concept detection, depending on your use case.</td></tr> -->
  <!-- </tbody></table></td></tr> -->
</tbody></table></td></tr>

<tr><td>competitionOverrides</td><td>An optional array of objects that help disambiguation know which cuis ought to compete with one another when they are annotated over the same span, and how they should compete. When no overrides are specified between two cuis, our system uses its own internal heuristics to determine when co-annotated cui pairs are mutually exclusive. Either cuis or semtypes must be present.<table role="presentation"><tbody>
  <tr><td>comment</td><td>Comment describing the purpose of the override. You can include multiple comments in the same object for multi-line comments. This is ignored by the service.</td></tr>
  <tr><td>cuis</td><td>Groups of CUIs. Members of the same group will not compete, but members of different groups may depending on the competitionMode. For example, if cuis=[[<q>C1</q>,<q>C2</q>],[<q>C3</q>]], then cuis C1 and C2 will not compete with one another, but both may compete with C3. Required if semtypes is not present.</td></tr>
  <tr><td>semtypes</td><td>Groups of semtypes that may be forced into competition. If a pair of cuis is affected by both a semtype-level competition override and a cui-level competition override, the cui-level override takes precedence. Required if cuis is not present.</td></tr>
  <tr><td>competitionMode</td><td>A string, which can be either <q>default</q> or <q>mutuallyExclusive</q>. In the <q>default</q> mode, we use heuristics to decide whether the cuis look compatible (like they could refer to the same real-world object), and make incompatible cuis compete. In the <q>mutuallyExclusive</q> mode, these cuis will always be forced to compete (at most 1 will ever be considered valid over the same text).</td></tr>
  <tr><td>scoring</td><td><table role="presentation"><tbody>
    <tr><td>mode</td><td>An array of strings which can be a subset of [<q>topic</q>, <q>sentence</q>, <q>semtype</q>]. This determines which model scores are used to compare two cuis that are competing. For example, if you are disambiguating two cuis that are very topically different (the <q>mole</q> skin marking vs <q>mole</q> animal) then you might want to resolve competition just using topic score (by specifying [<q>topic</q>]) rather than the default scoring mode (which is [<q>sentence</q>, <q>semtype</q>]) at differentiating them. To inspect model scores, enable debug mode.</td></tr>
  </tbody></table></td></tr>
</tbody></table></td></tr>

<tr><td>unknownConceptOverrides</td><td>An array of objects that specify how to treat CUIs with no known internal representation. These can either be non-UMLS concepts that don't have concept override entries giving them a textRepresentation, or else UMLS concepts whose surface forms didn't map well to any words or phrases embedded in our vocabulary. Any unknown concepts without an UnknownConceptOverride are by given assigned the default validity <q>NO_DECISION</q>.<table role="presentation"><tbody>
  <tr><td>comment</td><td>Comment describing the purpose of the override. You can include multiple comments in the same object for multi-line comments. This is ignored by the service.</td></tr>
  <tr><td>source</td><td>A string that specifies which concept source the override applies to. For example, "umls" matches UMLS concepts. Set debug to true to see which override matched a given unknown concept.</td></tr>
  <tr><td>scoring</td><td><table role="presentation"><tbody>
    <tr><td>mode</td><td>An array of strings which can be one of [<q>valid</q>, <q>invalid</q>, <q>ignore</q>]. This determines the judgment that disambiguation will give to cuis for which it has no known text representation ('ignore' currently maps to NO_DECISION).</td></tr>
  </tbody></table></td></tr>
</tbody></table></td></tr>

</table>

<h4>Response Fields</h4>

Disambiguation augments concepts with a <q>disambiguationData</q> object. By default, the only field inside this object is <q>validity</q> indicating disambiguation's final decision. However, when debug is set to true, disambiguation populates this object with additional information about how it reached its decision.
```javascript
{
  "cui": "C0013404",
  "preferredName": "Dyspnea",
  ...
  "disambiguationData": {
    "validity": "VALID"
  }
},
```
<table>
<caption>Response Fields</caption>
<tr>
<th>Fields</th><th>Description</th>
</tr>
<tr>
<td>validity</td>
<td>Disambiguation's final judgment: VALID/INVALID/NO_DECISION</td>
</tr>
<tr>
<td>comment</td>
<td>A brief explanation of factors that affected disambiguation's judgment.</td>
</tr>
<tr>
<td>textRepresentation</td>
<td>The textual representation used by disambiguation to score this concept. This comes either from a conceptOverride, if one exists, or else is automatically harvested from UMLS surface forms.</td>
</tr>
<tr>
<td>documentTopicScore</td>
<td>How well the concept's textRepresentation scored according to the topic model.</td>
</tr>
<tr>
<td>sentenceScore</td>
<td>LEGACY - In earlier versions of the service, there was a separate sentence model that tried to decide how well a concept's lexical representation fit in a given window of the sentence.  The sentence model was supplanted by a newer variant of the semtype model, but we still return a sentence model score (which is currently always the same as the semtype score) for backward compatibility reasons.</td>
</tr>
<tr>
<td>semanticTypeScore</td>
<td>How well the concept's semantic type scored according to the semtype model.</td>
</tr>
<tr>
<td>semanticTypeWordScore</td>
<td>How well the concept's textRepresentation scored according to an internal model that predicts the semtype of a given textRepresentation. This model is used internally to govern threshold strictness for the semtype model (e.g., <q>Alprazolam</q> will score well as a drug according to this model and so its semanticTypeScore will be held to a lower standard, whereas an ambiguous trade name like <q>Perform</q> will not).</td>
</tr>
<tr>
<td>pos</td>
<td>The part of speech assigned to this concept's span by the internal part-of-speech tagger. Useful for formulating and debugging posRules.</td>
</tr>
<tr>
<td>activeOverrides</td>
<td>An object summarizing the configuration that affected disambiguation's decision for this concept.</td>
</tr>
</table>

#### Concept Disambiguation Examples

##### Example: Fixing a bad text representation

**Problem**: You see that disambiguation does a poor job of disambiguating a cui that seems like it should be relatively easy to get right based on simple topic or sentence clues. For example, the cui for the <q>Perform</q> brand of lidocaine over the word <q>perform.</q> You set debug to true and see that disambiguation is using an incorrect or ambiguous textRepresentation, such as the word <q>perform</q> to represent the lidocaine cui.

**Solution**: Create a concept override with unambiguous text words and phrases. It is not necessary that this text be exactly equivalent to the concept in question. More important is that the text would plausibly fit only in context where the concept itself would fit. When multiple text representations are given, disambiguation scores them all and uses the best scoring for downstream judgments. So giving a variety of text representations can help improve system recall at the expense of some extra computation.

```javascript
"conceptOverrides": [{
    "comment": "The drug called <q>Perform</q>.",
    "cui": "C2947996",
    "textRepresentations": ["lidocaine","local_anesthetic"]
}]
```

Note: disambiguation will complain if you give it text that is unknown to the word embedding that disambiguation is built on. This embedding is defined over a vocabulary of about 1 million words/phrases. The easiest way to search this vocabulary for a good text representation is by plugging potential words/phrases into the `word/most_similar` endpoint of the Medical Word Correlation service. This way you can ensure that the word is known and that its nearest neighbors in the embedding space seem sensible. One caveat is that disambiguation will ignore words/phrases that occurred too few times in the training corpus that was used to train the word embedding (medline plus wikipedia). So if you see that a word is known to the Medical Word Correlation service but disambiguation complains about it being unknown, then it is a low-count word which is likely to be poorly embedded, and you will need to find a different candidate.

##### Example: Fixing a bad semantic type

**Problem**: Disambiguation erroneously throws out a concept based on a low semantic type score. You notice that the semantic type assigned by UMLS is invalid, too specific, or too broad. For example, <q>nevus</q> (a type of skin marking) is in UMLS as a NeoplasticProcess. This is sometimes true, but not always.

**Solution**: Add a concept override with one or more corrected semtypes for disambiguation to use when scoring this concept. As with textRepresentations, when there are multiple semtypeOverrides, the highest scoring semtype is used.

```javascript
"conceptOverrides": [{
    "comment": "The skin marking <q>mole</q>.",
    "cui": "C0027960",
    "textRepresentations": ["nevi", "nevus", "birthmark", "skin_tag", "skin_lesion"],
    "semtypeOverrides": ["umls.Finding"]
}]
```

##### Example: Filtering with part-of-speech rules

**Problem**: A concept is incorrectly annotated over text whose part of speech is incompatible with the concept. For example, the concept for the injury <q>burns</q> is annotated over the proper noun <q>Dr. Burns</q>.

**Solution**: Create a concept override with a posRules element containing a list of part-of-speech tags (listed above). Parts of speech with the prefix <q>!</q> are disallowed. This override states that the concept for burns (injury) can be valid only over text that is not a proper noun or a verb.

```javascript
"conceptOverrides": [{
    "comment": "Burns (injury) should not match proper nouns (Mr. Burns) or verbs.",
    "cui": "C1812606",
    "posRules": ["!propn", "!verb"]
}]
```

##### Example: Filtering with competition

**Problem**: Incompatible concepts fail to compete. For example, the concepts <q>mole</q> (skin marking) and <q>mole</q> (animal) should never both be valid in the same context.

**Solution**: Create a competition override requiring that concepts compete.

```javascript
"competitionOverrides": [{
    "comment": "Mole skin marking (C0027960) vs animal (C0324740)",
    "cuis": [["C0027960"], ["C0324740"]],
    "competitionMode": "mutuallyExclusive"
}]
```

##### Example: Filtering with competition (Advanced)

**Problem**: Disambiguation fails to invalidate a concept that is overly specific. For example the UMLS concept for <q>dental assistant</q> is called valid over the word <q>assistant.</q> This can be a tricky distinction to make since overly specific concepts may be reasonably topical in many contexts. One of the problems here is that UMLS doesn't have a concept for the general concept of <q>assistant,</q> which would make the job easier.

**Solution**: Create a concept override to define the general concept of <q>assistant,</q> and then create a competition override requiring that <q>assistant</q> and <q>dental_assistant</q> compete.

```javascript
"conceptOverrides": [{
    "comment": "A general <q>assistant</q> concept (to compete with the overly-specific <q>dental assistant</q>",
    "cui": "A0000001",
    "textRepresentations": ["assistant"]
}],
"competitionOverrides": [{
    "comment": "Differentiate <q>assistant</q> from <q>dental assistant</q>",
    "cuis": [
        ["A0000001"],
        ["C0011327"]
    ],
    "competitionMode": "mutuallyExclusive"
}]
```
