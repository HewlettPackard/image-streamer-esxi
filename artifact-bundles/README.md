# ESXi 5.x and ESXi 6.x artifacts for ImageStreamer v4.0 release
## Note:
- All artifact bundles in this repo are compatible with ImageStreamer v4.0 release
- Click on 'Branch:' drop down menu on this page to get artifact bundles for other ImageStreamer releases

## Version History:

HPE-ESXi-2017-12-15-v3.1
   - defect fixes for 4.0 release

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

	            File name: HPE-ESXi-2017-12-15-v3.1.zip
		Name (in manifest): HPE-ESXi-2017-12-15-v3.1
		       Description: ImageStreamer artifacts for ESXi 5.x and ESXi 6.x
		             Dated: 2017-12-15 (14:21:00)

--------------------------------------------------------------------------------

Build Plans:

	       Name: HPE - ESXi - generalize full state - 2017-09-27 (Type:capture)
	Description: Remove personalization settings from ESXi 5.x, 6.x images.
	             


	       Name: HPE - ESXi - deploy with multiple management NIC HA config- 2017-12-15 (Type:deploy)
	Description: Deploy ESXi 5.x or 6.x in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. 

	       Name: HPE- ESXi - deploy in single frame non-HA config- 2017-12-15 (Type:deploy)
	Description: Personalize ESXi 5.x, 6.x image with single management NIC, hostname, domain name, root password and ssh settings. 


Plan Scripts:

	       Name: HPE - ESXi - Logon Banner - 2017-12-05 (deploy)
	   FullName: 0aec7ef7-b0c0-4a0e-b6be-617f159c3e1a_planscript.json
	Description: Configures ESXi Logon Banner


	       Name: HPE - ESXi - mount - 2017-03-15 (general)
	   FullName: 17d07ad8-f726-439e-ba4f-06beea04b16f_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - Firewall Configuration - 2017-06-13 (deploy)
	   FullName: 256082a8-197e-4178-9f27-7afb2f23ddd5_planscript.json
	Description: Default Firewall Configuration


	       Name: HPE - ESXi - generalize onetime - 2017-09-27 (capture)
	   FullName: 2bb62f52-3c47-456f-bb89-eedfd18133fd_planscript.json
	Description: Clear the contents of local.sh in onetime.tgz and revert it to default contents


	       Name: HPE - ESXi - unpack state - 2017-07-07 (general)
	   FullName: 33ca5038-2dc5-4923-9eab-8e3d3d7462da_planscript.json
	Description: Copy out and unpack ESXi host state


	       Name: HPE - ESXi - Disable SSH Keys - 2017-06-13 (deploy)
	   FullName: 5a31d18b-3bb0-4357-8f65-57af4816702d_planscript.json
	Description: Disable use of SSH Keys to ESXi


	       Name: HPE - ESXi - configure management 2nd NIC HA - 2017-07-07 (deploy)
	   FullName: 619dc799-4e55-4c4f-aebf-f962243591e5_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA


	       Name: HPE - ESXi - remove system uuid - 2017-08-02 (capture)
	   FullName: 8502c16d-4842-4965-a9fb-6cc0f31b3dec_planscript.json
	Description: remove system uuid from esx.conf


	       Name: HPE - ESXi - Maintenance Mode - 2017-04-05 (deploy)
	   FullName: 8abd1b04-86a4-4f1d-b072-0e0b56e15061_planscript.json
	Description: Configure Maintenance Mode


	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: 8b929764-b718-498e-9d19-5cebb7f18537_planscript.json
	Description: Cleanup and unmount file systems


	       Name: HPE - ESXi  - Broadcom FCOE Discover - 2017-04-05 (deploy)
	   FullName: 8c35306b-a471-4d22-871f-8875d303f60d_planscript.json
	Description: Enable Broadcom FCoE Offload on Broadcom NetXtreme II FCoE Offload Capable Ethernet Devices.


	       Name: HPE - ESXi - configure ssh - 2017-12-15 (deploy)
	   FullName: 8f69d429-30f9-47d1-ab37-50d9113d1a9e_planscript.json
	Description: Configure ssh


	       Name: HPE - ESXi - Syslog Servers - 2017-04-05 (deploy)
	   FullName: a5f2b6a1-45a1-420b-8976-1a09c675e27a_planscript.json
	Description: Configure ESXi Syslog servers


	       Name: HPE - ESXi - generalize host configuration - 2017-07-12 (capture)
	   FullName: a820913f-6f71-4227-9175-36adc1879fab_planscript.json
	Description: Remove personalization settings from ESXi 5.x and 6.x images


	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: ab95f0ce-98a7-4ae3-b186-615fb530f429_planscript.json
	Description: Configure host password


	       Name: HPE - ESXi - Shell Timeouts - 2017-06-13 (deploy)
	   FullName: b437c34b-d441-4b9d-9949-322b76b2a29a_planscript.json
	Description: Configure ESXi Shell Timeouts
	             
	             ESXiShellInteractiveTimeOut - Time before interactive shell is automatically logged out in seconds
	             
	             ESXiShellTimeOut - Time to disable local or remote shell access


	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: ca352fcf-0120-432b-a3e4-1aeda82f1055_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume


	       Name: HPE - ESXi - configure management 1st NIC - 2017-08-22 (deploy)
	   FullName: cd78caf1-e96d-4b68-8875-b30e2cd4a81b_planscript.json
	Description: Configure ESXi host management network


	       Name: HPE - ESXi - Block VM Guest BPDU - 2017-06-13 (deploy)
	   FullName: d54e2204-2976-45be-90a6-0abbfecdce5f_planscript.json
	Description: BPDU Filter can be enabled on the ESXi host to drop any BPDU packets being sent to the physical switch.


	       Name: HPE - ESXi - NTP Server - 2017-06-13 (deploy)
	   FullName: e27465bb-dbc6-4cdf-a562-39e59ef02fc2_planscript.json
	Description: Configure NTP Servers for ESXi hosts.
	             Enter ntp servers separated by a space


	       Name: HPE - ESXi - configure iSCSI boot HA - 2017-06-13 (deploy)
	   FullName: ee9e060a-5a4c-494e-a1ff-8e6f3156314f_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi


	       Name: HPE - ESXi - Power Management - 2017-06-13 (deploy)
	   FullName: f8d88cdf-f8f0-4f9b-8fb1-a65841abc19c_planscript.json
	Description: Configure ESXi Power Management.
	             
	             PowerPolicy - Valid Values "High Performance" , Balanced , Lower Power or Custom


	       Name: HPE - ESXi - 3PAR SATP Claim Rule - 2017-04-05 (deploy)
	   FullName: fe5f16ce-5350-4d74-b2b0-8c178c548e76_planscript.json
	Description: Create 3PAR SATP Claim Rule as per HPE Best Practice



