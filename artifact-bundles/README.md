# ESXi 5.x and ESXi 6.x artifacts for ImageStreamer v3.1 release
## Note:
- All artifact bundles in this repo are compatible with ImageStreamer v3.1 release
- Click on 'Branch:' drop down menu on this page to get artifact bundles for other ImageStreamer releases

## Version History:

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

	            File name: HPE-ESXi-2017-08-22-v3.0.zip
		Name (in manifest): HPE-ESXi-2017-08-22
		       Description: ImageStreamer artifacts for ESXi 5.x and ESXi 6.x.
		             Dated: 2017-08-22 (07:01:36)

--------------------------------------------------------------------------------


Build Plans:

	       Name: HPE - ESXi - deploy with multiple management NIC HA config- 2017-08-22 (Type:deploy)
	Description: Deploy ESXi 5.x or 6.x in a multi-frame environment containing a pair of ImageStreamer appliances. 
	             This buildplan configures HA for iSCSI boot connections to ESXi volume. 


	       Name: HPE - ESXi - generalize full state - 2017-08-02 (Type:capture)
	Description: Remove personalization settings from ESXi 5.x, 6.x images.


	       Name: HPE- ESXi - deploy in single frame non-HA config- 2017-08-22 (Type:deploy)
	Description: Personalize ESXi 5.x, 6.x image with single management NIC, hostname, domain name, root password and ssh settings.


Plan Scripts:

	       Name: HPE - ESXi - configure management 2nd NIC HA - 2017-07-07 (deploy)
	   FullName: 02f5b663-125c-4ebd-a8a9-30890a362fa9_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA


	       Name: HPE - ESXi - Block VM Guest BPDU - 2017-06-13 (deploy)
	   FullName: 24829699-5139-461d-ae01-738a3a716ba8_planscript.json
	Description: BPDU Filter can be enabled on the ESXi host to drop any BPDU packets being sent to the physical switch.


	       Name: HPE - ESXi - Power Management - 2017-06-13 (deploy)
	   FullName: 2522bf3c-cd5c-4803-befc-d25dd408cc2f_planscript.json
	Description: Configure ESXi Power Management.
	             
	             PowerPolicy - Valid Values "High Performance" , Balanced , Lower Power or Custom


	       Name: HPE - ESXi - 3PAR SATP Claim Rule - 2017-04-05 (deploy)
	   FullName: 2af3bdbc-2a8b-4141-8356-c57b1f59dcab_planscript.json
	Description: Create 3PAR SATP Claim Rule as per HPE Best Practice


	       Name: HPE - ESXi - remove system uuid - 2017-08-02 (capture)
	   FullName: 3740593d-039c-4488-b0c2-4cce5e720144_planscript.json
	Description: remove system uuid from esx.conf


	       Name: HPE - ESXi - NTP Server - 2017-06-13 (deploy)
	   FullName: 4ef04278-ffdb-4624-b5af-9b88eb675100_planscript.json
	Description: Configure NTP Servers for ESXi hosts.
	             Enter ntp servers separated by a space


	       Name: HPE - ESXi - generalize host configuration - 2017-07-12 (capture)
	   FullName: 50ba8363-6153-4ea0-8735-52f9cff1194a_planscript.json
	Description: Remove personalization settings from ESXi 5.x and 6.x images


	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: 68693322-12e9-4a09-b5f6-00bd88bb8d1e_planscript.json
	Description: Configure host password


	       Name: HPE - ESXi - unpack state - 2017-07-07 (general)
	   FullName: 6912d4ed-1dd8-4738-ab9f-5329206b078f_planscript.json
	Description: Copy out and unpack ESXi host state


	       Name: HPE - ESXi  - Broadcom FCOE Discover - 2017-04-05 (deploy)
	   FullName: 76e0fd95-5705-47d1-af93-14187b7a5c67_planscript.json
	Description: Enable Broadcom FCoE Offload on Broadcom NetXtreme II FCoE Offload Capable Ethernet Devices.


	       Name: HPE - ESXi - Syslog Servers - 2017-04-05 (deploy)
	   FullName: 807a7917-a060-43cc-86ce-97421b96679f_planscript.json
	Description: Configure ESXi Syslog servers


	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: 812d64ba-302c-414e-ab4a-d4c21fa8f5bf_planscript.json
	Description: Cleanup and unmount file systems


	       Name: HPE - ESXi - configure management 1st NIC - 2017-08-22 (deploy)
	   FullName: 94d24a92-01bc-4421-8b71-0cb38868171c_planscript.json
	Description: Configure ESXi host management network


	       Name: HPE - ESXi - Maintenance Mode - 2017-04-05 (deploy)
	   FullName: 9da5e86c-1e9e-4ff9-8e1e-b153f3d8eec2_planscript.json
	Description: Configure Maintenance Mode


	       Name: HPE - ESXi - Logon Banner - 2017-06-13 (deploy)
	   FullName: ab29178f-ecbf-45b4-b771-b80bdd09365f_planscript.json
	Description: Configures ESXi Logon Banner


	       Name: HPE - ESXi - configure iSCSI boot HA - 2017-06-13 (deploy)
	   FullName: c0ba7305-87aa-401b-bc85-f3f6f7921ab3_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi


	       Name: HPE - ESXi - Disable SSH Keys - 2017-06-13 (deploy)
	   FullName: c944ebdc-eea1-455c-953b-3412c63c0704_planscript.json
	Description: Disable use of SSH Keys to ESXi


	       Name: HPE - ESXi - Shell Timeouts - 2017-06-13 (deploy)
	   FullName: ccbe4770-6027-4e82-9b67-363bdca8a4d6_planscript.json
	Description: Configure ESXi Shell Timeouts
	             
	             ESXiShellInteractiveTimeOut - Time before interactive shell is automatically logged out in seconds
	             
	             ESXiShellTimeOut - Time to disable local or remote shell access


	       Name: HPE - ESXi - Firewall Configuration - 2017-06-13 (deploy)
	   FullName: d2bb3952-420c-43a3-ab3c-3eabf5f21008_planscript.json
	Description: Default Firewall Configuration


	       Name: HPE - ESXi - generalize onetime - 2017-08-02 (capture)
	   FullName: d6bd17a7-589e-4cb1-8747-e98539f44b68_planscript.json
	Description: Clear the contents of local.sh in onetime.tgz and revert it to default contents


	       Name: HPE - ESXi - mount - 2017-03-15 (general)
	   FullName: dbac2e82-e19c-4e49-bad0-d174b569a0b7_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: de074e5c-3303-4518-87e5-cb854739ab9b_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume


	       Name: HPE - ESXi - configure ssh - 2017-03-15 (deploy)
	   FullName: ffa8d1cc-e831-4486-8a62-fa6bcfd59bf2_planscript.json
	Description: Configure ssh
