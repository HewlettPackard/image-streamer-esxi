# ESXi artifacts for ImageStreamer v4.1 release
## Note:
- All artifact bundles in this repo are compatible with ImageStreamer v4.1 release
- Click on 'Branch:' drop down menu on this page to get artifact bundles for other ImageStreamer releases
- The following ESXi versions are supported
	- ESXi 5.5
	- ESXi 6.0
	- ESXi 6.5

## Version History:

HPE-ESXi-2018-07-31-v4.1
   - Not unique UUID issue fixed

HPE-ESXi-2018-06-27-v4.1
   - MPIO has been enabled
   - Notified users of UEFI secure boot deployment not supported

## Artifact Bundle Contents:

--------------------------------------------------------------------------------
  
  	File name: HPE-ESXi-2018-07-31-v4.1.zip
  	Name (in manifest): HPE - ESXi - 2018-07-31 - v4.1
  	Description: ImageStreamer artifacts for ESXi 5.x and ESXi 6.x till 6.5. 
  	Dated: 2018-08-13 (14:49:04)
	
--------------------------------------------------------------------------------

Build Plans:

	       Name: HPE - ESXi - deploy with multiple management NIC HA config- 2018-07-31 (Type:deploy)
	Description: Deploy ESXi 5.x - 6.5 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. (c) Copyright 2018 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0  (the "License");...


	       Name: HPE - ESXi - generalize full state - 2018-07-31 (Type:capture)
	Description: Remove personalization settings from ESXi 5.x - 6.5 images.
	             (c) Copyright 2018 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the "License"); ...


	       Name: HPE- ESXi - deploy in single frame non-HA config- 2018-07-31 (Type:deploy)
	Description: Personalize ESXi 5.x - 6.5 image with single management NIC, hostname, domain name, root password and ssh settings. (c) Copyright 2018 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0  (the "License");...



Plan Scripts:

	       Name: HPE - ESXi - mount - 2018-07-31 (general)
	   FullName: 2497b14d-d9b9-459c-bb45-401d457dc1d6_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - unpack state - 2017-07-07 (general)
	   FullName: 291851b3-224a-4267-ae71-cad8ce5c805b_planscript.json
	Description: Copy out and unpack ESXi host state


	       Name: HPE - ESXi - mpio - configure iSCSI boot HA - 2018-06-27 (deploy)
	   FullName: 2b093c6e-2a24-42f7-a017-21eaaa754aad_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi. 
	             This script can be used in multi frame environment containing a pair of ImageStreamer appliances.


	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: 35cf64d4-f241-49c0-93e3-b68c6e9df2cd_planscript.json
	Description: Configure host password


	       Name: HPE - ESXi - configure management 1st NIC - 2017-08-22 (deploy)
	   FullName: 4aef4d00-0606-4658-8437-891c677350db_planscript.json
	Description: Configure ESXi host management network


	       Name: HPE - ESXi - configure management 2nd NIC HA - 2017-07-07 (deploy)
	   FullName: 6b65ed11-d3cd-4c70-be26-3d55c8bdddad_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA


	       Name: HPE - ESXi - generalize host configuration - 2017-07-12 (capture)
	   FullName: 7cd73ee8-54b2-48f9-abec-790b214378e3_planscript.json
	Description: Remove personalization settings from ESXi 5.x and 6.x images


	       Name: HPE - ESXi - configure ssh - 2017-12-15 (deploy)
	   FullName: 9226e3ab-a233-408b-a73c-d366f5a996d0_planscript.json
	Description: Configure ssh


	       Name: HPE - ESXi - remove system uuid - 2017-08-02 (capture)
	   FullName: a8a346fb-c52d-464e-a019-b0edde46fb36_planscript.json
	Description: remove system uuid from esx.conf


	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: b30faefe-50a8-4637-9fcb-ad6931499795_planscript.json
	Description: Cleanup and unmount file systems


	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: ce1a6bb8-5899-4c7c-bde4-0d1142751189_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume


	       Name: HPE - ESXi - generalize onetime - 2017-09-27 (capture)
	   FullName: d7fc8b12-c802-458c-879f-76ed4360b979_planscript.json
	Description: Clear the contents of local.sh in onetime.tgz and revert it to default contents

