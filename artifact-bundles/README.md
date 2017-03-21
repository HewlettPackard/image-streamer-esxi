#ImageStreamer artifacts for ESXi 5.x and ESXi 6.x

#Artifact Bundle Contents:


--------------------------------------------------------------------------------
	File name	  : HPE-ESXi-2017-03-16.zip
	Name (in manifest): HPE-ESXi-2017-03-1
	Description	  : Artifact bundle for ESXi 5.x and ESXi 6.x deployment and generalization
	Dated		  : 2017-03-16 (18:54:45)
--------------------------------------------------------------------------------

Build Plans:

	       Name: HPE - ESXi - deploy in multi frame config - 2017-03-16 (Type:deploy)
	Description: Deploy ESXi 5.x or 6.x in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume.


	       Name: HPE - ESXi - simple host configuration with NIC HA - 2017-03-16 (Type:deploy)
	Description: Personalize ESXi 5.x, 6.x image with two management NICs for HA, hostname, domain name, root password and ssh settings


	       Name: HPE - ESXi - generalize full state - 2017-03-15 (Type:capture)
	Description: Remove personalization settings from ESXi 5.x, 6.x images


	       Name: HPE - ESXi - simple host configuration - 2017-03-16 (Type:deploy)
	Description: Personalize ESXi 5.x, 6.x image with single management NIC, hostname, domain name, root password and ssh settings



Plan Scripts:

	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: 1761ffe4-2443-4cc0-9acd-de526a62d598_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume


	       Name: HPE - ESXi - mount - 2017-03-15 (general)
	   FullName: 1a14ce5e-f692-4924-bdf4-ec98a615b531_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - configure management 2nd NIC HA - 2017-03-15 (deploy)
	   FullName: 1eb536f3-02fa-4dc1-87f9-75f052c623f0_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA


	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: 23fad7a8-2a3f-4357-95af-388b2b687c4c_planscript.json
	Description: Cleanup and unmount file systems


	       Name: HPE - ESXi - unpack state - 2017-03-15 (general)
	   FullName: 25bb27bd-91d0-4556-9f14-1ebf00962205_planscript.json
	Description: Copy out and unpack ESXi host state


	       Name: HPE - ESXi - configure iSCSI boot HA - 2017-03-15 (deploy)
	   FullName: b8142814-0603-4071-9656-630ffbbe1601_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi. 
	             This script can be used in multi frame environment containing a pair of ImageStreamer appliances.


	       Name: HPE - ESXi - configure management 1st NIC - 2017-03-16 (deploy)
	   FullName: c4be7f02-b3c3-442f-a12c-f6424a140093_planscript.json
	Description: Configure ESXi host management network


	       Name: HPE - ESXi - configure ssh - 2017-03-15 (deploy)
	   FullName: d218206e-c7e6-4d59-9c32-0b6d0e576ad2_planscript.json
	Description: Configure ssh


	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: dfbf5f2f-b428-455f-92c1-b627b575ed61_planscript.json
	Description: Configure host password


	       Name: HPE - ESXi - generalize host configuration - 2017-03-15 (capture)
	   FullName: ec589299-c261-45b1-bd09-323bf3149aad_planscript.json
	Description: Remove personalization settings from ESXi 5.x and 6.x images


