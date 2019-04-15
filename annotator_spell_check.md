<h3 id="spell_check">Spell Check (Experimental)</h3>

This annotator identifies misspelled words and phrases in a document and suggests corrections.

<h4>Configurations</h4>
<table>
  <caption>Configurations</caption>
  <tr>
    <th>Configuration</th>
    <th>Values</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>debug</td>
    <td>true/false</td>
    <td>When true, the spell check annotator will provide an additional field with a human-readable rendering of the corrections that were applied to the source document.</td>
  </tr>
</table>

<h4>Sample Spelling Corrections Returned in Response</h4>

```javascript
{
  "spellCorrectedText": [
    {
      "correctedText": "The patient has high blood pressure",
      "debugText": "The patient has >>>high blood presure->high blood pressure(0.98)<<<"
    }
  ],
  "spellingCorrections": [
    {
      "begin": 16,
      "end": 34,
      "coveredText": "high blood presure",
      "suggestions": [
        {
          "applied": true,
          "confidence": 0.98,
          "semtypes": [
            "umls.DiseaseOrSyndrome",
            "umls.ClinicalAttribute"
          ],
          "text": "high blood pressure"
        }
      ]
    }
  ]
}
```

<h4>Annotation Types</h4>

<li>spellCorrectedText</li>
<li>spellingCorrections</li>
<li>suggestions</li>

###### spellCorrectedText

<table>
  <caption>spellCorrectedText</caption>
  <tr>
    <th>Fields</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>correctedText</td>
    <td>The document text with spelling corrections applied.</td>
  </tr>
  <tr>
    <td>debugText</td>
    <td>A debug version of the spell corrected document text.</td>
  </tr>
</table>

###### spellingCorrections

<table>
  <caption>spellingCorrections</caption>
  <tr>
    <th>Fields</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>begin</td>
    <td>The start position of the misspelled word as a character offset into the text.  The smallest possible start position is 0.</td>
  </tr>
  <tr>
    <td>end</td>
    <td>The end position of the misspelled word as a character offset into the text.  The end position points to the first character after the spelling correction, such that end-begin equals the length of the coveredText.</td>
  </tr>
  <tr>
    <td>coveredText</td>
    <td>The text of the misspelled word.</td>
  </tr>
</table>

###### suggestions

<table>
  <tr>
    <caption>suggestions</caption>
  </tr>
  <tr>
    <th>Fields</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>applied</td>
    <td>When true, this indicates that this correction was applied in the _correctedText_ version of the document.</td>
  </tr>
  <tr>
    <td>confidence</td>
    <td>A measure of how confident the annotator is that this suggestion is correct.</td>
  </tr>
  <tr>
    <td>semtypes</td>
    <td>A list of UMLS semantic types that apply to the given suggestion (if any exist).</td>
  </tr>
  <tr>
    <td>text</td>
    <td>The text of the spelling suggestion.</td>
  </tr>
</table>
