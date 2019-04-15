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

# Ejection Fraction
{: #ejection_fraction}

The purpose of the Ejection Fraction annotator is to annotate ejection fraction test results. Ejection fraction is a measurement of the percentage of blood leaving your heart each time it contracts. The Ejection Fraction annotation is generally used as input into calculations or models that predict various heart related scenarios.
{:shortdesc}

During each heartbeat pumping cycle, the heart contracts and relaxes. When your heart contracts, it ejects blood from the two pumping chambers (ventricles). When your heart relaxes, the ventricles refill with blood. No matter how forceful the contraction, it never is able to pump all of the blood out of a ventricle. The term <q>ejection fraction</q> refers to the percentage of blood that's pumped out of a filled ventricle with each heartbeat.

The left ventricle is the heart's main pumping chamber that pumps oxygenated blood through the ascending (upward) aorta to the rest of the body, so ejection fraction is usually measured only in the left ventricle (LV). An LV ejection fraction of 55 percent or higher is considered normal. An LV ejection fraction of 50 percent or lower is considered reduced.

The span of the EjectionFractionInd annotation includes all the associated terms, numeric percent value(s) and the token words between them.

Examples:

* low EF.
* 20% EF.
* EF is low.
* EF is 20%.
* EF is 20-35%.
* LVEF was normal
* ejection fraction was normal.
* ejection fraction of 20%-25%.
* EF has to be measured at approximately 30%-50%.
* 47% EF recent report of echo.
* ef of between 0 and 25% by echocardiogram.
* ejection fraction of 10 - 25 percent by echocardiogram.
* 25 percent to 30 percent ejection fraction.

<h4>Configurations</h4>

<table>
<caption>Configurations</caption>
<tr>
<th>Configuration</t>
<th>Values</th>
<th>Description</th>
</tr>
<tr>
<td>library</td>
<td>
<ul>
  <li>umls.2016AA <i>(deprecated - will be removed in 2019)</i></li>
  <li>umls.2017AA</li>
  <li>umls.2018AA</li>
  <li>umls.latest</li>
</ul>
</td>
<td>Defines the version of the UMLS library that is used when annotating unstructured data.  The value <q>umls.latest</q> is used to indicate the latest version of the available UMLS libraries (2018AA).  It is also the default value for the <b>library</b> configuration.</td>
</tr>
</table>

<h4>Annotation Types</h4>

* aci.EjectionFractionInd

###### aci.EjectionFractionInd

<table>
<caption>aci.EjectionFractionInd</caption>
<tr><th>__Feature__</th><th>__Description__</th></tr>
</thd><td>begin</td><td>The start position of the annotation as a character offset into the text. The smallest possible start position is 0.</td></tr>
<tr><td>end</td><td>The end position of the annotation as character offset into the text. The end position points at the first character after the annotation, such that end-begin equals the length of the coveredText.</td></tr>
<tr><td>coveredText</td><td>The text covered by an annotation as a string.</td></tr>
<tr><td>type</td><td>aci.EjectionFractionInd</td></tr>
<tr><td>firstValue</td><td>The first value of percentage.  For example, in the text “echocardiogram demonstrated ejection fraction of 30 to 35%”, the firstValue is 30.</td></tr>
<tr><td>secondValue</td><td>The second value of percentage.  For example, in the text “echocardiogram demonstrated ejection fraction of 30 to 35%”, the secondValue is 35.  If the value is not specified as a range then the value of this feature is not retuned.</td></tr>
<tr><td>isRange</td><td>Determines if the ejection fraction phrase contains a range of values.  For example, in the text “echocardiogram demonstrated ejection fraction of 30 to 35%”, the isRange is true.</td></tr>
<tr><td>measurementMethod</td><td>Method by which the Ejection/Fraction percentage or ratio is measured.  The measurementMethod will be <q>echo</q> if the method by which the ejection fraction was take was an echocardiogram, otherwise, the measurementMethod  feature will not be present.</td></tr>
<tr><td>efAlphabeticValueNormalizedName</td><td>Normalized name for the appliied value that is word form.</td></tr>
<tr><td>efAlphabeticValueSurfaceForm</td><td>Covered text that represents applied value in word form.   For example, in the text <q>EF was severely depressed at 28%</q>, the efAlphabeticValueSurfaceForm is <q>severely depressed</q>.  Examples include:   <q>low</q>, <q>normal</q>, <q>reduced</q>, and <q>improvement</q>.</td></tr>
<tr><td>efTermNormalizedName</td><td>Normalized name for ejection fraction.   For example, in the text <q>Echocardiogram at the outside hospital demonstrated EF of approximately 60%</q>, the efTermNormalizedName is <q>ejection fraction</q>.</td></tr>
<tr><td>efTermSurfaceForm</td><td>Covered text that represents the ejection fraction.   For example, in the text <q>Echocardiogram at the outside hospital demonstrated EF of approximately 60%</q>, the efTermSurfaceForm is <q>EF</q>.  Examples include:  <q>EF</q>, <q>LVEF</q>, <q>left ventricular ejection fraction</q>, <q>RVEF</q>,  and <q>ejection fraction</q>.</td></tr>
<tr><td>efSuffixSurfaceForm</td><td>Covered text that represents the suffix to the measurement.  For example, in the text <q>Echocardiogram demonstrated EF of approximately 60%</q>, the efSuffixSurfaceForm is <q>%</q>.  Examples include: <q>%</q>, <q>percent</q>,  and <q>percentile</q>,</td></tr>
<tr><td>efSuffixNormalizedName</td><td>Normalized name for suffix measurement fraction.</td></tr>
<tr><td>echocardiogramNormalizedName</td><td>The normalized name for the echocardiogram.</td></tr>
<tr><td>echocardiogramSurfaceForm</td><td>Covered text that represents the echocardiogram.  Examples include:   <q>echo</q>, <q>echocardiogram</q>, and  "echocardiographic".</td></tr>
</table>
