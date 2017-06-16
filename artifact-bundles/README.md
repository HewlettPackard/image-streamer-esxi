# ImageStreamer artifacts for ESXi 5.x and ESXi 6.x

HPE-ESXi-2017-06-13
   - Added planscripts for additional ESXi configuration - FCoE enablement, 3PAR SATP claim rule, power management, syslog servers, logon banner, disable SSH keys, NTP servers, maintenance mode, block VM guest BPDU, firewall configuration, esxi shell timeout
   - These planscripts are not part of any build plan, but they can be used as build steps on need basis 

HPE-ESXi-2017-03-24
   - Simple ESXi host configuration with single management NIC, hostname, domain name, root password and ssh settings
   
## Artifact Bundle Contents:


--------------------------------------------------------------------------------

	            File name: HPE-ESXi-2017-06-13.zip
		Name (in manifest): HPE-ESXi-2017-06-13
		       Description: ImageStreamer artifacts for ESXi 5.x and ESXi 6.x.
		             Dated: 2017-06-13 (03:57:38)

--------------------------------------------------------------------------------


Build Plans:

	       Name: HPE - ESXi - deploy in single frame non-HA config- 2017-03-24 (Type:deploy)
	Description: Personalize ESXi 5.x, 6.x image with single management NIC, hostname, domain name, root password and ssh settings. 



	       Name: HPE - ESXi - generalize full state - 2017-03-24 (Type:capture)
	Description: Remove personalization settings from ESXi 5.x, 6.x images.
	             

	       Name: HPE - ESXi - deploy with multiple management NIC HA config- 2017-03-24 (Type:deploy)
	Description: Deploy ESXi 5.x or 6.x in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. 


Plan Scripts:


	       Name: HPE - ESXi - 3PAR SATP Claim Rule - 2017-04-05 (deploy)
	   FullName: 01164891-4449-481e-875c-41cf7a7f4828_planscript.json
	Description: Create 3PAR SATP Claim Rule as per HPE Best Practice



	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: 067e4f13-8e97-4511-8378-c7a4d2e146c4_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume



	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: 0f81737a-8b37-4dfb-b5ee-5be17e073cf0_planscript.json
	Description: Cleanup and unmount file systems



	       Name: HPE - ESXi  - Broadcom FCOE Discover - 2017-04-05 (deploy)
	   FullName: 1c6f94e5-50d4-494e-9b6b-fdaccd5212c9_planscript.json
	Description: Enable Broadcom FCoE Offload on Broadcom NetXtreme II FCoE Offload Capable Ethernet Devices.



	       Name: HPE - ESXi - unpack state - 2017-03-15 (general)
	   FullName: 1e8c77e6-f5e9-4ed2-94a3-a7d4f7e11840_planscript.json
	Description: Copy out and unpack ESXi host state



	       Name: HPE - ESXi - Maintenance Mode - 2017-04-05 (deploy)
	   FullName: 34949f39-22c7-4176-9e6b-d68772b6db2a_planscript.json
	Description: Configure ESXi Syslog servers



	       Name: HPE - ESXi - mount - 2017-03-15 (general)
	   FullName: 38c87b1b-91b7-4713-b4f1-d223198d1e2d_planscript.json
	Description: Mount ESXi /bootbank



	       Name: HPE - ESXi - Logon Banner - 2017-06-13 (deploy)
	   FullName: 4c0690e1-8fe9-4b76-954c-7bf04258a61c_planscript.json
	Description: Configures ESXi Logon Banner



	       Name: HPE - ESXi - configure ssh - 2017-03-15 (deploy)
	   FullName: 54f44fb2-3b1f-49e4-988d-330899f7278c_planscript.json
	Description: Configure ssh



	       Name: HPE - ESXi - Disable SSH Keys - 2017-06-13 (deploy)
	   FullName: 8b1f3c92-792b-4722-aacc-fb6e5ec8d236_planscript.json
	Description: Disable use of SSH Keys to ESXi



	       Name: HPE - ESXi - configure iSCSI boot HA - 2017-03-15 (deploy)
	   FullName: 947115ee-8193-4e25-9cd9-50e4ef2f2750_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi. 


	       Name: HPE - ESXi - Block VM Guest BPDU - 2017-06-13 (deploy)
	   FullName: b632cbd5-317e-4ba1-a6ee-48c0a300aaef_planscript.json
	Description: BPDU Filter can be enabled on the ESXi host to drop any BPDU packets being sent to the physical switch.



	       Name: HPE - ESXi - configure management 2nd NIC HA - 2017-03-15 (deploy)
	   FullName: d1efb93d-46f1-4215-84d0-15c2430b6634_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA



	       Name: HPE - ESXi - NTP Server - 2017-06-13 (deploy)
	   FullName: d3295205-6d6d-4e57-b6ca-6435ff7859ee_planscript.json
	Description: Configure NTP Servers for ESXi hosts.
	             Enter ntp servers separated by a space



	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: de027376-2976-44ac-9f4b-2f8a12fc45bc_planscript.json
	Description: Configure host password



	       Name: HPE - ESXi - Syslog Servers - 2017-04-05 (deploy)
	   FullName: e55ddde6-78cf-4d7e-bfc3-ed7b4113271b_planscript.json
	Description: Configure ESXi Syslog servers



	       Name: HPE - ESXi - generalize host configuration - 2017-03-15 (capture)
	   FullName: e7a651e8-a4dd-4f33-98b4-fa16dcf0a86b_planscript.json
	Description: Remove personalization settings from ESXi 5.x and 6.x images



	       Name: HPE - ESXi - Firewall Configuration - 2017-06-13 (deploy)
	   FullName: e7e72076-da19-46fb-a528-9cc46e101489_planscript.json
	Description: Default Firewall Configuration



	       Name: HPE - ESXi - Power Management - 2017-06-13 (deploy)
	   FullName: e985b897-24f5-487d-a585-71c7b0f552e1_planscript.json
	Description: Configure ESXi Power Management.
	             PowerPolicy - Valid Values "High Performance" , Balanced , Lower Power or Custom



	       Name: HPE - ESXi - configure management 1st NIC - 2017-03-16 (deploy)
	   FullName: f46bf9e9-e67d-418c-af57-49901a45f649_planscript.json
	Description: Configure ESXi host management network



	       Name: HPE - ESXi - Shell Timeouts - 2017-06-13 (deploy)
	   FullName: ff35fb87-0b54-45ba-8d0d-6eb4630c9041_planscript.json
	Description: Configure ESXi Shell Timeouts
	             ESXiShellInteractiveTimeOut - Time before interactive shell is automatically logged out in seconds
	             ESXiShellTimeOut - Time to disable local or remote shell access
