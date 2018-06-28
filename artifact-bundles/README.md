# ESXi 5.x and ESXi 6.x artifacts for ImageStreamer v4.0 release
## Note:
- All artifact bundles in this repo are compatible with ImageStreamer v4.0 release
- Click on 'Branch:' drop down menu on this page to get artifact bundles for other ImageStreamer releases
- The following ESXi versions are supported
	- ESXi 5.5
	- ESXi 6.0
	- ESXi 6.5
## Version History:

HPE-ESXi-2018-06-27-v4.0
   - MPIO enabled
   - defect fixes

HPE-ESXi-2017-05-10-v4.0
   - changes to handle correct bootbank after an ESXi patch update
   - defect fixes

HPE-ESXi-2017-08-22-v3.0
   - Removed UUID from esx.conf during generalization
   - Removed contents of local.sh in onetime.tgz during generalization
   - Fixed issue with "Management" tag not getting set sometimes on network interface
   - Added vlanid attribute to support network sets   
   - Commented echo of local.sh since it can contain the password

HPE-ESXi-2017-06-13
   - Added planscripts for additional ESXi configuration - FCoE enablement, 3PAR SATP claim rule, power management, syslog servers, logon banner, disable SSH keys, NTP servers, maintenance mode, block VM guest BPDU, firewall configuration, esxi shell timeout
   - These planscripts are not part of any build plan, but they can be used as build steps on need basis 

HPE-ESXi-2017-03-24
   - Simple ESXi host configuration with single management NIC, hostname, domain name, root password and ssh settings
   

## Artifact Bundle Contents:

--------------------------------------------------------------------------------

	            File name: HPE-ESXi-2018-06-27-v4.0.zip
		Name (in manifest): HPE-ESXi-2018-06-27-v4.0
		       Description: ImageStreamer artifacts for ESXi 5.x and ESXi 6.x till 6.5.
		             Dated: 2018-05-20 (12:11:25)

--------------------------------------------------------------------------------

Build Plans:

	       Name: HPE - ESXi - deploy with multiple management NIC HA config- 2018-06-27 (Type:deploy)
	Description: Deploy ESXi 5.x - 6.5 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. 

	       Name: HPE - ESXi - generalize full state - 2018-06-27 (Type:capture)
	Description: Remove personalization settings from ESXi 5.x - 6.5 images.
	            
	       Name: HPE- ESXi - deploy in single frame non-HA config- 2018-06-27 (Type:deploy)
	Description: Personalize ESXi 5.x - 6.5 image with single management NIC, hostname, domain name, root password and ssh settings. 


Plan Scripts:

	       Name: HPE - ESXi - configure management 1st NIC - 2017-08-22 (deploy)
	   FullName: 1e64262e-483d-48c4-8384-b26ccd804f3b_planscript.json
	Description: Configure ESXi host management network


	       Name: HPE - ESXi - generalize host configuration - 2017-07-12 (capture)
	   FullName: 28ccbbc5-76e4-4ab3-a60b-7cc6aba93367_planscript.json
	Description: Remove personalization settings from ESXi 5.x and 6.x images


	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: 35e9c556-ade9-488c-83da-929db0d4b57e_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume


	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: 626d0f69-832c-4591-89ba-50f8a593aef6_planscript.json
	Description: Cleanup and unmount file systems


	       Name: HPE - ESXi - mpio - configure iSCI boot HA - 2018-06-27 (deploy)
	   FullName: 65cdd322-7bfb-46b8-aeb2-c065a88e504d_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi. 
	             This script can be used in multi frame environment containing a pair of ImageStreamer appliances.


	       Name: HPE - ESXi - unpack state - 2017-07-07 (general)
	   FullName: 713508f4-fa93-46f0-ae31-54829e09116f_planscript.json
	Description: Copy out and unpack ESXi host state


	       Name: HPE - ESXi - mount - 2018-06-27 (general)
	   FullName: 7a0b3af0-59ab-4cc9-8072-5bb68e61a867_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - configure management 2nd NIC HA - 2017-07-07 (deploy)
	   FullName: a8239680-8c4d-44ae-ac00-d6dde0cae5a1_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA


	       Name: HPE - ESXi - generalize onetime - 2017-09-27 (capture)
	   FullName: e2fb01bb-cc30-4613-918b-3306646f9344_planscript.json
	Description: Clear the contents of local.sh in onetime.tgz and revert it to default contents


	       Name: HPE - ESXi - remove system uuid - 2017-08-02 (capture)
	   FullName: ef688745-e9ba-41f2-bcd2-db4c2c183f3e_planscript.json
	Description: remove system uuid from esx.conf


	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: f1705470-645a-4f46-a63b-607395ff0945_planscript.json
	Description: Configure host password


	       Name: HPE - ESXi - configure ssh - 2017-12-15 (deploy)
	   FullName: f2c1d2a5-1aae-432c-ac90-3a3d7fc8c7c0_planscript.json
	Description: Configure ssh





