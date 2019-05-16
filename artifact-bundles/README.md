# ESXi artifacts for ImageStreamer v4.2 release
## Note:
- All artifact bundles in this repo are compatible with ImageStreamer v4.2 release
- Click on 'Branch:' drop down menu on this page to get artifact bundles for other ImageStreamer releases
- The following ESXi versions are supported with HPE-ESXi-2019-04-10-v4.2.zip
	- ESXi 5.5
	- ESXi 6.0
	- ESXi 6.5
- For ESXi 6.7, artifact bundle to be used - HPE-ESXi-6.7-2019-04-09-v4.2

## Version History:

 HPE-ESXi-2019-04-10-v4.2
   - Modified script to handle HA for full blades - SY660 - with multiple CNA cards
   
 HPE-ESXi-6.7-2019-04-09-v4.2
   - Modified script to handle HA for full blades - SY660 - with multiple CNA cards - for ESXi 6.7
   
 HPE-ESXi-2018-07-31-v4.2
   - Not unique UUID issue fixed

 HPE-ESXi 6.7-2018-08-02-v4.2
   - Artifact Bundle for ESXi 6.7

## Golden Image Creation for ESXi 6.7:

1. Ensure that you have access to ESXi 6.7 ISO file.

1. Create a server profile with “HPE - Foundation 1.0 - create empty OS Volume” as OS Deployment plan and a server hardware of desired hardware type. Set an appropriate value for volume size in MiB units, say 20480 MiB. The HPE Synergy Server will be configured for access to this empty OS Volume.

1. Launch iLO Integrated Remote Console of this server and set the ESXi 6.7 ISO file as virtual CD-ROM/DVD image file. Power on the server.

1. Install ESXi 6.7.

1. Reboot the Compute Blade. [required for the OS to create the state.tgz folder]

1. To capture the ESXi 6.7 image:
  
    1.  Shutdown the server gracefully by pressing F12, and shutting it down, or by giving ‘poweroff’ command from SSH console, or by, clicking on the Momentary Press from iLO console of the server.

    1.  Perform an as-is capture using "HPE - Foundation 1.0 - capture OS Volume as is" build plan to create the "as-is" golden image of the OS. (NOTE: There are no generalization - capture scripts for ESXi 6.7)

    1.  Deploy another server with the golden image captured in previous step and build plan of your choice to boot the server.

1. To install VIBs or updates via virtual media and then capture ESXi 6.7 image:

    1. The golden Image should be captured only from an ESXi OS instance that is not personalized.
    
    1. Identify a compute blade to capture the ESXi image. Install the base ESXi ISO if required.
    
    1. Convert the ZIP file containing VIBs to be installed into an ISO, using any application available on internet or in linux using the command:
       - mkisofs –o /tmp/<FileName.iso> /tmp/directory/

    1. Select this ISO file as virtual CD-ROM/DVD image file. 
    
    1. SSH to the console and run following commands:
       - esxcfg-mpath –l | grep –i cd-rom
       - vmkload_mod iso9660
       - /sbin/vsish –e set /vmkModules/iso9660/mount <Device Display Name>

    1. To verify the contents:
       - ls /vmfs/volumes/<Device Display Name>

    1. To install VIB:
       - esxcli software vib install –d /vmfs/volumes/<.ISO file>
     
    1. Unmount CD ROM and unload module:
       - vsish –e set /vmkModules/iso9660/umount<Device Display Name>
       - vmkload_mod –u iso9660
	
    1. Reboot the Compute Blade.
    
    1. Verify the VIBs are installed:
       - esxcli software vib list

    1. Shutdown the server gracefully by pressing F12, and shutting it down, or by giving ‘poweroff’ command from SSH console, or by, clicking on the Momentary Press button.
    
    1. Perform an as-is capture using "HPE - Foundation 1.0 - capture OS Volume as is" build plan to create the "as-is" golden image of the OS. (NOTE: There are no generalization - capture scripts for ESXi 6.7)


## Known Issues:
- In case of ungraceful or forceful shutdown of the server (within an hour of the deployment), there may be a loss of personalization.
  Please refer to the VMware article for the same: https://kb.vmware.com/s/article/2001780
  

## Artifact Bundle Contents:

--------------------------------------------------------------------------------

	            File name: HPE-ESXi-2019-04-10-v4.2.zip
		Name (in manifest): HPE-ESXi-2019-04-10-v5.0
		       Description: ImageStreamer artifacts for ESXi 5.x and ESXi 6.x till 6.5. 
		             Dated: 2019-04-09 (22:07:29)

--------------------------------------------------------------------------------

Build Plans:

	       Name: HPE- ESXi - deploy in single frame non-HA config-autobackup- 2018-07-31 (Type:deploy)
	Description: Personalize ESXi 5.x - 6.5 image with single management NIC, hostname, domain name, root password and ssh settings. 

	       Name: HPE - ESXi - generalize full state -  2018-07-31 (Type:capture)
	Description: Remove personalization settings from ESXi 5.x - 6.5 images.

	       Name: HPE - ESXi - deploy with multiple management NIC HA config-autobackup- 2019-04-10 (Type:deploy)
	Description: Deploy ESXi 5.x - 6.5 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. 


Plan Scripts:

	       Name: HPE - ESXi - remove system uuid - 2017-08-02 (capture)
	   FullName: 0313cfc7-1a60-4720-9a19-d3f5ee2811f4_planscript.json
	Description: remove system uuid from esx.conf


	       Name: HPE - ESXi - configure management 1st NIC- 2018-12-06 (deploy)
	   FullName: 27e2518e-60c9-4626-ad79-b3e1a30acfd9_planscript.json
	Description: Configure ESXi host management network


	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: 33b3501d-fde7-43d0-900b-3776cfd6e48b_planscript.json
	Description: Cleanup and unmount file systems


	       Name: HPE - ESXi - configure management 2nd NIC HA- 2018-12-06 (deploy)
	   FullName: 45c2d1a1-49d5-4ff3-a019-2cb306d24797_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA


	       Name: HPE - ESXi - unpack state - 2017-07-07 (general)
	   FullName: 554a6b51-e010-4056-bd22-009a2c19b30d_planscript.json
	Description: Copy out and unpack ESXi host state


	       Name: HPE - ESXi - mpio - configure iSCSI boot HA - 2019-04-10 (deploy)
	   FullName: 650b97bc-c8ed-4df9-bb3e-772ba0edbfb1_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi. 
	             This script can be used in multi frame environment containing a pair of ImageStreamer appliances.


	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: 6d0676fa-3590-43b7-b4a8-53a6c31d8607_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume


	       Name: HPE - ESXi - generalize onetime - 2017-09-27 (capture)
	   FullName: 964fd0e7-e3c7-480b-8dea-41c3a3b9cbfa_planscript.json
	Description: Clear the contents of local.sh in onetime.tgz and revert it to default contents


	       Name: HPE - ESXi - mount - 2018-12-03 (general)
	   FullName: b4641fca-8721-4120-be2e-e8c04f8eb37b_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: b5d91f26-926d-4652-8d1a-55357572e266_planscript.json
	Description: Configure host password


	       Name: HPE - ESXi - generalize host configuration - 2017-07-12 (capture)
	   FullName: eaece103-eb8c-4330-89f8-055307b157a7_planscript.json
	Description: Remove personalization settings from ESXi 5.x and 6.x images


	       Name: HPE - ESXi - configure ssh- 2018-12-04 (deploy)
	   FullName: ee23ca7e-83fa-4553-8afb-18451152c3d0_planscript.json
	Description: Configure ssh


--------------------------------------------------------------------------------

	            File name: HPE-ESXi-6.7-2019-04-09-v4.2.zip
		Name (in manifest): HPE-ESXi-6.7-2019-04-09-v5.0
		       Description: ImageStreamer artifacts for ESXi 6.7. 
		             Dated: 2019-04-09 (11:27:17)

--------------------------------------------------------------------------------

Build Plans:

	       Name: HPE - ESXi 6.7 - deploy with multiple management NIC HA config - 2019-04-09 (Type:deploy)
	Description: Deploy ESXi 6.7 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume.

	       Name: HPE - ESXi 6.7 - deploy in single frame non-HA config - 2018-08-02 (Type:deploy)
	Description: Deploy ESXi 6.7 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. 


Plan Scripts:

	       Name: HPE - ESXi - configure ssh - 2017-12-15 (deploy)
	   FullName: 1e0878b1-593f-440c-a20b-2a31b89e1ec5_planscript.json
	Description: Configure ssh


	       Name: HPE - ESXi 6.7 - generalize state - 2018-08-02 (general)
	   FullName: 28c3ed51-d526-4c50-8373-30b0e71941a0_planscript.json
	Description: Clear the contents of local.sh in state.tgz and revert it to default contents


	       Name: HPE - ESXi - mount - 2018-07-31 (general)
	   FullName: 2eb0658d-08a8-42f1-acf1-5829fe22de70_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: 327657f5-8e9c-4997-8039-3ef60486f979_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume


	       Name: HPE - ESXi - configure management 2nd NIC HA - 2017-07-07 (deploy)
	   FullName: 5b10582e-9688-46ea-971a-a74f6580393b_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA


	       Name: HPE - ESXi - mpio - configure iSCSI boot HA - 2019-04-09 (deploy)
	   FullName: 6495f244-c684-4d31-8e1b-5de2b4868f9d_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi. 
	             This script can be used in multi frame environment containing a pair of ImageStreamer appliances.


	       Name: HPE - ESXi 6.7 - replace initiator IP - 2018-08-02 (deploy)
	   FullName: 77a1ec7e-8d8d-42d2-8a73-6b74f88fb32a_planscript.json
	Description: Build script to replace initiator ip


	       Name: HPE - ESXi 6.7 - unpack state - 2018-08-02 (general)
	   FullName: a208cdba-0cae-414c-81e5-725a524bbf1a_planscript.json
	Description: Copy out and unpack ESXi host state


	       Name: HPE - ESXi 6.7 - clear local - 2018-08-02 (general)
	   FullName: a8aa951b-43d0-44af-b677-e15537595425_planscript.json
	Description: Clear the contents of local.sh post personalization


	       Name: HPE - ESXi - configure management 1st NIC - 2017-08-22 (deploy)
	   FullName: b8fbc509-ec5c-46c2-b385-26aa50053075_planscript.json
	Description: Configure ESXi host management network


	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: c0330c9c-fb2f-4cb5-8a68-8922963ebbee_planscript.json
	Description: Cleanup and unmount file systems


	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: e77cf8a3-f3c4-4e2d-9b01-bc59724ab5dc_planscript.json
	Description: Configure host password


	       Name: HPE - ESXi 6.7 - remove system uuid - 2018-08-02 (deploy)
	   FullName: f03aab7d-a410-4966-be65-1e7191485d14_planscript.json
	Description: Remove system uuid from esx.conf




