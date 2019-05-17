---

copyright:
  years: 2019
lastupdated: "2019-02-20"

keywords: annotator clinical data, clinical data, annotation

subcollection: wh-acd

---


{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}


# FAQs
{: #wh-acd-faqs}

## How can I add my own terms to match for a medical concept?
{: #faq-custom-dictionary}
{: faq}

Using the <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html" target="_blank">Domain Expert Tool (DET)</a>, you can create a custom dictionary to detect your unique medical concepts. The type of dictionary will vary based on the annotator you are using. The DET also allows you to derived concepts by discovering one or more related concepts in the surrounding text.  See the DET <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/help/DET_GettingStartedGuide.pdf">Getting Started Guide</a> for more information.

## How can I remove concept matches that are not useful for my application?
{: #faq-filter}
{: faq}

Using the <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html" target="_blank">Domain Expert Tool (DET)</a>, you can create a filter to remove unwanted concepts. The type of filter will vary based on the annotator you are using. See the DET <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/help/DET_GettingStartedGuide.pdf">Getting Started Guide</a> for more information.

## What is a cartridge?
{: #faq-cartridge}
{: faq}

A cartridge is a collection of artifacts that provide [customizations](wh-acd?topic=wh-acd-customizing#customizing) for  {{site.data.keyword.wh-acd_short}}
 for a given solution domain. A cartridge is built using the <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html" target="_blank">Domain Expert Tool (DET)</a> and is [deployed](wh-acd?topic=wh-acd-deploy_cartridge#deploy_cartridge) to  {{site.data.keyword.wh-acd_short}}
 to be used when [analyzing text](wh-acd?topic=wh-acd-analyze_text#analyze_text).

## What is an attribute?
{: #faq-attribute}
{: faq}

Clinical Attributes are a customized set of clinical findings that are pertinent to a particular disease domain or engagement that represents the user's view of the solution domain. Clinical Attributes can be linked to external classification codes such as ICD9 or CPT. A clinical attribute has a name that is unique for that domain. Attributes are defined using the <a href="https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/cartridge-main.html" target="_blank">Domain Expert Tool (DET)</a>. A clinical attribute also has an associated value. The values can be discovered from the surrounding text, enumerated during definition of the attribute, derived from other attributes, or it can merely indicate that the attribute was mentioned in the text. The definition of the attribute also includes which medical concepts should be mapped to the attribute.
