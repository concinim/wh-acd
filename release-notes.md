---

copyright:
  years: 2019
lastupdated: "2019-05-01"

keywords: annotator clinical data, clinical data, annotation

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

# Release notes
{: #release-notes}

The following sections document the new features and changes that were included for each release of the {{site.data.keyword.wh-acd_short}} service.
{: shortdesc}

## Service API versioning
{: #service-api-versioning}

API requests require a version parameter that takes the date in the format version=YYYY-MM-DD. Send the version parameter with every API request.

When we change the API in a backwards-incompatible way, we release a new minor version. To take advantage of the changes in a new version, change the value of the version parameter to the new date. If you're not ready to update to that version, don't change your version date.

### August 2020
{: #august-2020}
- Initial release of normality models for clinical insights.

### July 2020
{: #july-2020}

- Added support for UMLS 2020AA. UMLS 2017AA has been removed and 2018AA is now deprecated _(will be removed in 2021 when we add support for UMLS 2021AA)._

### April 2020
{: #april-2020}
- Initial release of clinical insight models for Diagnosis, Medication, and Procedure

### October 2019
{: #october-2019}

- Asynchronous (non-blocking) cartridge deployment APIs with persisted deployment status.

### September 2019
{: #september-2019}

- Ability to apply spelling corrections from the spell check annotator for use by all service annotators.

### August 2019
{: #august-2019}

- Added support for UMLS 2019AA. UMLS 2016AB has been truncated and UMLS 2017AA is now deprecated _(will be removed in 2020 when we add support for UMLS 2020AA)._

### June 2019
{: #june-2019}

- When spelling corrections from the spell check annotator are present, the concept detection annotator will leverage those spelling corrections for entity detection.
- The {{site.data.keyword.wh-acd_full}} is now available in the {{site.data.keyword.cloud}} US South location for approved internal IBM solution providers.
- Support for attribute detection over derived concepts with longest span.
