<h3 id="cartridges">Cartridges</h3>

Cartridges are containers used for the customization of ACD. Within a cartridge are domain-specific artifacts chosen by the consumer detailing ACD configuration information. Artifacts created by the consumer are restricted to be less then 2MB.  Cartridges are built using the [Domain Expert Tool (DET)](http://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/). Following the creation of a cartridge, the consumer will customize ACD by deploying a snapshot of the cartridge to ACD. The deployment of the cartridge snapshot will create <q>profile</q> and <q>flow</q> objects within the ACD service. These objects can then be referenced as part of the request when invoking ACD.

##### Cartridge deployment scenario:

1.  The consumer uses the [Domain Expert Tool (DET)](http://watsonpow01.rch.stglabs.ibm.com/services/cartridge_det/) to create a new cartridge (or modify an existing one) and customizes the contents (artifacts) of the cartridge to their domain.
2.  Next, using DET, the consumer will **Export** the cartridge in order to save a snapshot of the cartridge to their computer.
3.  Lastly, the consumer deploys the cartridge snapshot (a zip file) to ACD using _POST /v1/deploy_ API. In the following curl example, the consumer's cartridge file is `./my_cartridges/name_of_cartridge_file.zip`, and `update=false` means do not update the resource if it already exists with the ACD service.

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X POST --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" -F "archive_file=@./my_cartridges/name_of_cartridge_file.zip" "http://host/services/clinical_data_annotator/api/v1/deploy?update=false&version=2018-01-17"
```

* A successful cartridge deploy will result in <q>201 Created</q> if it is a new resource, or <q>200 OK</q> if `update=true` was specified and the existing resource was updated.

**Note:** some large cartridge deployments can exceed the request timeout thresholds defined in the DataPower gateways (usually after 2 mins). In that event, you may receive the following error response:

```javascript
{
  "httpCode":"500",
  "httpMessage":"Internal Server Error",
  "moreInformation":"Failed to establish a backside connection"
}
```

This timeout occurs outside of ACD and does not prevent your cartridge from being successfully deployed. You just won't get the itemized response confirming successful deployment of each individual artifact within your cartridge. If your cartridge deployment request times out, here are steps you can take to verify successful deployment after giving the process about 15 minutes to complete.

* For initial deployment of a cartridge, you can look for the creation of the annotator flow to determine whether deployment has completed. The annotator flow is the last artifact created during the deployment process and its existence signals completion of deployment in the initial deployment of a cartridge.

Sample request to retrieve flows for your tenant, for verifying completion of initial cartridge deployment:

```console
# X-IBM-Client-Id and X-IBM-Client-Secret headers are employed for ACD requests within the Watson Platform for Health
curl -X GET --header "Accept: application/json" --header "X-IBM-Client-Id: xxxxx" --header "X-IBM-Client-Secret: xxxxx" "http://host/services/clinical_data_annotator/api/v1/flows?version=2018-02-14"
```

* For updates to a previously deployed cartridge and to verify successful deployment of a cartridge in general upon a deployment request timeout, run some sample text through the _POST /v1/analyze_ API and verify that the response adheres to the configurations defined within your cartridge.
