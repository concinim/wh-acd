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

# Current Procedural Terminology (CPT) Code Support
{: #cpt_codes}

Support for reporting Current Procedural Terminology (CPT) codes is available in both the Concepts and Procedures annotators, however CPT codes are not provided without additional configuration due to additional license requirements by the American Medical Association (AMA). After obtaining a license to use CPT codes, the codes can be added to the Concepts and/or Procedures annotators.
{:shortdesc}

CPT codes are considered to be a non-level 0 data set in the Unified Medical Language System (UMLS), meaning that the codes are included in their tooling, but licensed separately. Download the UMLS MetamorphoSys tool from the following location. Choose <q>Full Release</q>: http://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html

Once you have downloaded the latest UMLS MetamorphoSys release, use the following instructions to install MetamorphoSys and obtain the proper data file containing the CPT codes:

1.  Extract mmsys.zip and .nlm (compressed Metathesaurus data) files to the same location.
2.  Run the utility by launching run.bat, or your environment equivalent, in the folder in which you extracted mmsys.zip.
3.  Click <q>Install UMLS</q> when the utility launches.
4.  Choose appropriate source and destination folders for your system and click OK. Note the destination folder name for use in a later step.
5.  Acknowledge the Validation Log dialog when it appears by selecting Continue.
6.  Click <q>New Configuration...</q> on the new dialog that appears.
7.  Click <q>Accept</q> to accept the terms displayed on the new window that appears.
8.  Select <q>Level 0 + SNOMEDCT_US</q> in the table. This includes all Level 0 sources plus SNOMEDCT_US. This forms the basis of the subset to which you will add CPT data in the following steps. Click OK.
9.  On the next dialog that appears, click on the Source List tab at the top, and click the Source Family column heading in the table to sort the list.
10. By default, the tool treats items selected as items to excluded from the subset. In order to add CPT codes to the subset, deselect it. To do this, hold down the Ctrl key and click “Current Procedural Terminology, 2017” in the table. A new window appears. Click OK to allow the tool to expand the selection to include all CPT sources (HCPCS Version and Physicians' Spanish Translation).
11. Select the Done menu-item from the window, then choose <q>Begin Subset</q>. If prompted to save your configuration, you may save a configuration file on your system if desired. The subsetting process will take a long time to complete. Depending on hardware configuration, this process can take a few hours.
12. When the installation and extraction process is complete, acknowledge the MetamorphoSys Subset Log dialog, close the MetamorphoSys install window, and find the MRCONSO.RRF file containing CPT codes data in the /META folder of your destination folder.

After creating the MRCONSO.RRF data file, use the Watson Health [Domain Expert Tool](https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/) to generate a valid CPT codes properties file. The CPT codes properties file is then added to a Cartridge which can then be used with ACD.

1.  Open Watson Health [Domain Expert Tool](https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/). In the Cartridge Catalog, click <q>New</q> to create a new Cartridge.
2.  On the New Cartridge dialog, enter values for <q>Name,</q> <q>Author,</q> <q>Email,</q> and <q>Description.</q> Since CPT codes require additional licensing from the AMA, choose the <q>Private</q> option for the <q>Public or Private</q> combo box. Provide a comma-delimited list of authorized users for the Cartridge in the <q>Authorized Users</q> field. Then select the <q>Create</q> button.
3.  After the new Cartridge has been created, ensure it is selected and choose the <q>Edit</q> button. This brings you to the Cartridge Editor view.
4.  Click the <q>Create</q> button and choose <q>New CPT Code Mapping</q> from the options available.
5.  On the New CPT Code Mapping dialog, enter values for <q>Name</q>, <q>Owner</q>, and <q>Description</q> fields. In the <q>Authorized Users</q> field, enter the IDs for only those users that are licensed to use the CPT codes generated. Select the <q>Browse</q> button and navigate to the MRCONSO.RRF file to use. Choose <q>Open</q> and then choose <q>Import</q>.
6.  Acknowledge the pop-up dialog indicating the estimated time required to generate the CPT codes properties file.
7.  Once the CPT code mapping file has successfully completed processing, it will be added to your cartridge automatically and appear in your cartridge's artifact list.

An alternative to using the AMA's MRCONSO.RRF file and working through the steps listed above to create a valid CPT Codes Mapping file is to provide your own file (using the <q>.properties</q> filetype extension) structured in the following manner:

```console
CUI=CPT Code
```

For example:

```console
C0002393=41874
C0002500=80150
C0002627=1008945,59000
C0002691=27590,1014580
```
Note: A CUI can map to multiple CPT Codes, simply comma-delimit them as in the example provided above.

You are now ready to use your CPT Code Mapping file. Following is a sample request using the CPT Code Mapping file just created. Note the use of the _profile_ element. Using the [Domain Expert Tool](https://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/), navigate to the Deploy Cartridge Panel for the cartridge you created in step 2 above. The value to use for the profile can be found in the ACD Profile field on that panel.

```javascript
{
  "annotatorFlows": [
    {
      "profile" : "mytest_profile",
      "flow": {
        "elements": [
          {
            "annotator": {
              "name": "procedure"
             }
           }
        ],
       "async": true
      }
    }
  ],
  "unstructured": [
    {
      "text": "Patient is covered for total knee replacement."
    }
  ]
}
```
