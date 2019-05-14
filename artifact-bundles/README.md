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
  
  	File name: HPE-ESXi-2018-07-31-v4.2.zip
  	Name (in manifest): HPE - ESXi - 2018-07-31 - v4.2
  	Description: ImageStreamer artifacts for ESXi 5.x and ESXi 6.x till 6.5. 
  	Dated: 2018-08-13 (14:49:04)
	
--------------------------------------------------------------------------------

Build Plans:

	       Name: HPE - ESXi - deploy with multiple management NIC HA config- 2018-07-31 (Type:deploy)
	Description: Deploy ESXi 5.x - 6.5 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. 


	       Name: HPE - ESXi - generalize full state - 2018-07-31 (Type:capture)
	Description: Remove personalization settings from ESXi 5.x - 6.5 images.
	             

	       Name: HPE- ESXi - deploy in single frame non-HA config- 2018-07-31 (Type:deploy)
	Description: Personalize ESXi 5.x - 6.5 image with single management NIC, hostname, domain name, root password and ssh settings. 


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
	
	

--------------------------------------------------------------------------------

	            File name: HPE-ESXi-6.7-2018-08-02-v4.2.zip
		Name (in manifest): HPE - ESXi 6.7-2018-08-02-v4.2
		       Description: ImageStreamer artifacts for ESXi 6.7. 

--------------------------------------------------------------------------------

Build Plans:

	       Name: HPE - ESXi 6.7 - deploy in single frame non-HA config - 2018-08-02 (Type:deploy)
	Description: Deploy ESXi 6.7 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. 

	       Name: HPE - ESXi 6.7 - deploy with multiple management NIC HA config - 2018-08-02 (Type:deploy)
	Description: Deploy ESXi 6.7 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume.


Plan Scripts:

	       Name: HPE - ESXi 6.7 - replace initiator IP - 2018-08-02 (deploy)
	   FullName: 02030147-7d99-4c9d-89b7-625d26576591_planscript.json
	Description: Build script to replace initiator ip


	       Name: HPE - ESXi - mount - 2018-07-31 (general)
	   FullName: 291b5cd1-f765-4ca6-b3ec-925f58245581_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - configure management 2nd NIC HA - 2017-07-07 (deploy)
	   FullName: 3e191459-78f6-469f-8b79-28755e6f7b4c_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA


	       Name: HPE - ESXi - configure management 1st NIC - 2017-08-22 (deploy)
	   FullName: 5d2bd2f0-849e-4af7-a884-cdd6685f13c6_planscript.json
	Description: Configure ESXi host management network


	       Name: HPE - ESXi - mpio - configure iSCSI boot HA - 2018-06-27 (deploy)
	   FullName: 6c11827d-a130-43ba-be19-4e467a496c58_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi. 
	             This script can be used in multi frame environment containing a pair of ImageStreamer appliances.


	       Name: HPE - ESXi 6.7 - unpack state - 2018-08-02 (general)
	   FullName: 720c3ca3-74f4-4c7c-9999-65a5eeac2830_planscript.json
	Description: Copy out and unpack ESXi host state


	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: 8bcc6e27-756e-473d-92e5-e49912a5bb0a_planscript.json
	Description: Cleanup and unmount file systems


	       Name: HPE - ESXi 6.7 - remove system uuid - 2018-08-02 (deploy)
	   FullName: 9a4c3ccd-7bbf-4dc4-b718-a0fe62dfddcf_planscript.json
	Description: Remove system uuid from esx.conf


	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: a5a9ac43-6397-4e14-9b26-5e1490fc2fa1_planscript.json
	Description: Configure host password


	       Name: HPE - ESXi 6.7 - clear local - 2018-08-02 (general)
	   FullName: bd05c371-8647-4044-b5d6-a78a9b86177a_planscript.json
	Description: Clear the contents of local.sh post personalization


	       Name: HPE - ESXi 6.7 - generalize state - 2018-08-02 (general)
	   FullName: c816f14a-35da-4b70-a68e-d899a7fc2532_planscript.json
	Description: Clear the contents of local.sh in state.tgz and revert it to default contents


	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: d4206076-8bd3-4050-a0d1-7f103361e13a_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume


	       Name: HPE - ESXi - configure ssh - 2017-12-15 (deploy)
	   FullName: fcfb2525-1e13-475a-a68b-a9abe17a4971_planscript.json
	Description: Configure ssh




