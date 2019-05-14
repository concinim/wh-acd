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

# Known Limitations
{: #known_limitations}

## Text Size Limits

{{site.data.keyword.wh-acd_short}} imposes a 50K limit on text being analyzed per request. For json requests, the json metadata does not count towards the 50K threshold. The {{site.data.keyword.wh-acd_short}} /analyze APIs will return a 413 error if the input text exceeds the 50K threshold. 
