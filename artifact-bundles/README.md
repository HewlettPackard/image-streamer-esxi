# ESXi 5.x and ESXi 6.x artifacts for ImageStreamer v4.0 release
## Note:
- All artifact bundles in this repo are compatible with ImageStreamer v4.0 release
- Click on 'Branch:' drop down menu on this page to get artifact bundles for other ImageStreamer releases

## Version History:

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

	            File name: HPE-ESXi-2018-05-10-v4.0.zip
		Name (in manifest): HPE-ESXi-2018-05-10-v4.0
		       Description: ImageStreamer artifacts for ESXi 5.x and ESXi 6.x.
		             Dated: 2018-05-20 (12:11:25)

--------------------------------------------------------------------------------

Build Plans:

	       Name: HPE- ESXi - deploy in single frame non-HA config- 2018-05-10 (Type:deploy)
	Description: Personalize ESXi 5.x, 6.x image with single management NIC, hostname, domain name, root password and ssh settings. 

	       Name: HPE - ESXi - generalize full state - 2018-04-24 (Type:capture)
	Description: Remove personalization settings from ESXi 5.x, 6.x images.
	             
	       Name: HPE - ESXi - deploy with multiple management NIC HA config- 2018-05-10 (Type:deploy)
	Description: Deploy ESXi 5.x or 6.x in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. 


Plan Scripts:

	       Name: HPE - ESXi - Disable SSH Keys - 2017-06-13 (deploy)
	   FullName: 019d0e71-e0be-49b3-8bbf-87b66f425f70_planscript.json
	Description: Disable use of SSH Keys to ESXi


	       Name: HPE - ESXi - Power Management - 2017-06-13 (deploy)
	   FullName: 03af79df-a0a0-42b4-9f61-66342975e963_planscript.json
	Description: Configure ESXi Power Management.
	             
	             PowerPolicy - Valid Values "High Performance" , Balanced , Lower Power or Custom


	       Name: HPE - ESXi - configure iSCSI boot HA - 2017-06-13 (deploy)
	   FullName: 2031b37c-895b-44e6-9e54-8634b1ad6d9d_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi


	       Name: HPE - ESXi - configure management 2nd NIC HA - 2017-07-07 (deploy)
	   FullName: 2b8c79d1-c61b-4bc0-8a29-7df37a4d386c_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA


	       Name: HPE - ESXi - Block VM Guest BPDU - 2017-06-13 (deploy)
	   FullName: 313f9b95-23e5-4b16-bb58-ff5ba3a9755a_planscript.json
	Description: BPDU Filter can be enabled on the ESXi host to drop any BPDU packets being sent to the physical switch.


	       Name: HPE - ESXi - Shell Timeouts - 2017-06-13 (deploy)
	   FullName: 38d004a3-6da3-4d53-a1d3-9d7d0f6e5453_planscript.json
	Description: Configure ESXi Shell Timeouts
	             
	             ESXiShellInteractiveTimeOut - Time before interactive shell is automatically logged out in seconds
	             
	             ESXiShellTimeOut - Time to disable local or remote shell access


	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: 3bb46e66-23c7-4d4b-a44a-c7d40fb29f36_planscript.json
	Description: Cleanup and unmount file systems


	       Name: HPE - ESXi - mount - 2018-04-24_updated (general)
	   FullName: 3f14c7fb-a323-4415-957a-fa5c16e0b97b_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - mount - 2018-04-24 (general)
	   FullName: 69bb5f62-dfd6-4f08-a484-9524f8b3ebf3_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: 7372612f-2fd4-43ef-8132-af0d8dbe8cfe_planscript.json
	Description: Configure host password


	       Name: HPE - ESXi - generalize host configuration - 2017-07-12 (capture)
	   FullName: 775e0de8-70d2-47ad-a4de-61a6c3300208_planscript.json
	Description: Remove personalization settings from ESXi 5.x and 6.x images


	       Name: HPE - ESXi - remove system uuid - 2017-08-02 (capture)
	   FullName: 7fa5a01f-c94c-4b66-978a-9f620534ba09_planscript.json
	Description: remove system uuid from esx.conf


	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: 8607f304-2fae-412d-a70c-be8aa22b1fe1_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume


	       Name: HPE - ESXi - Syslog Servers - 2017-04-05 (deploy)
	   FullName: 909ba102-2d4e-46f1-b655-96fbd7d9b25e_planscript.json
	Description: Configure ESXi Syslog servers


	       Name: HPE - ESXi - configure management 1st NIC - 2017-08-22 (deploy)
	   FullName: 916691b2-2bb6-48c2-a5e7-8624f213f3d5_planscript.json
	Description: Configure ESXi host management network


	       Name: HPE - ESXi - unpack state - 2017-07-07 (general)
	   FullName: 978989db-40bc-4c93-87f2-3a3effded45f_planscript.json
	Description: Copy out and unpack ESXi host state


	       Name: HPE - ESXi - 3PAR SATP Claim Rule - 2017-04-05 (deploy)
	   FullName: 987380f8-4fd3-45bf-9fce-1fbdfcde4589_planscript.json
	Description: Create 3PAR SATP Claim Rule as per HPE Best Practice


	       Name: HPE - ESXi  - Broadcom FCOE Discover - 2017-04-05 (deploy)
	   FullName: b107b16d-093a-4990-b0bd-ca75dfabe210_planscript.json
	Description: Enable Broadcom FCoE Offload on Broadcom NetXtreme II FCoE Offload Capable Ethernet Devices.


	       Name: HPE - ESXi - Logon Banner - 2017-12-05 (deploy)
	   FullName: b7a28d46-1d9c-4ecf-9641-f74cf38766f1_planscript.json
	Description: Configures ESXi Logon Banner


	       Name: HPE - ESXi - configure ssh - 2017-12-15 (deploy)
	   FullName: bcbf887c-e40d-4ff4-8724-63c8095110cc_planscript.json
	Description: Configure ssh


	       Name: HPE - ESXi - generalize onetime - 2017-09-27 (capture)
	   FullName: c31fd956-52b8-4ec4-b417-e3960c8a56f9_planscript.json
	Description: Clear the contents of local.sh in onetime.tgz and revert it to default contents


	       Name: HPE - ESXi - Maintenance Mode - 2017-04-05 (deploy)
	   FullName: eff8a1ef-f9be-44d7-b0fd-c1be73cc263b_planscript.json
	Description: Configure Maintenance Mode


	       Name: HPE - ESXi - Firewall Configuration - 2017-06-13 (deploy)
	   FullName: f0a2cc53-557b-4c9e-b18f-3a3f8f666fba_planscript.json
	Description: Default Firewall Configuration


	       Name: HPE - ESXi - NTP Server - 2017-06-13 (deploy)
	   FullName: fedb4cab-ee9c-4fab-9c0f-3211870ef0cc_planscript.json
	Description: Configure NTP Servers for ESXi hosts.
	             Enter ntp servers separated by a space




