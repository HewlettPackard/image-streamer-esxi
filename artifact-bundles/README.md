# ESXi 6.5 and ESXi 6.7 to ESXi 7.0 artifacts for ImageStreamer v6.10 release
## Note:
- For versions of ESXi 6.5 Please use HPE-ESXi-xxxx-xx-xx-v6.10.zip Artifact Bundle
- For versions of ESXi 6.7 and onwards Please use HPE-ESXi-6.7-xxxx-xx-xx-v6.10.zip Artifact Bundle
- All artifact bundles in this repo are compatible with ImageStreamer v6.10 release
- Click on 'Branch:' drop down menu on this page to get artifact bundles for other ImageStreamer releases
- The following ESXi versions are supported
	- ESXi 6.5 (ESXi 6.5, ESXi 6.5 U1, ESXi 6.5 U2)
	- ESXi 6.7 (ESXi 6.7, ESXi 6.7 U1, ESXi 6.7 U2, ESXi 6.7 U3)
	- ESXi 7.0 (ESXi 7.0, ESXi 7 U1)

## Version History:
HPE-ESXi-2021-07-26-v6.10.zip
   - Modified MPIO script to remove default vmk0 - remove old MAC and portID
   - Plan script change to handle attributes when GI with multiple updates is used.
   - Modified iBFT script to handle iSCSI path DEAD issue when a non-HA build plan with one Deployment connection is used for deployment.
   - Modified "Clear - Network" script to handle/delete "iscsibootvswitch" creation in the Golden Image.

HPE-ESXi-6.7-2020-10-27-v6.10.zip
   - Modified script to remove default vSwitch and vmnic created on GI captured from i3s deployed node	
   - Has corrective action as per VMware knowledgebase 2148321 for remounting bootbank from /tmp to /sda

HPE-ESXi-7.0-2021-05-10-v6.10.zip
   - Use this Artifact for ESXi version 7.0 Update 2 and higher.
   
## Golden Image creation for ESXi 6.7/7.0:

An Image Streamer Golden Image for ESXi 6.7 is to be captured ‘as is’, without any generalization scripts. This also introduces a constraint that the ESXi 6.7 image to be captured, shouldn’t contain any personalization. 
Any personalization, if done on the host before capturing the image will be retained and should be overwritten during the subsequent deployments. 


1. Ensure that you have access to ESXi 6.7/7.0 ISO file.

1. Create a server profile with “HPE - Foundation 1.0 - create empty OS Volume” as OS Deployment plan and a server hardware of desired hardware type. Set an appropriate value for volume size in MiB units, say 20480 MiB. The HPE Synergy Server will be configured for access to this empty OS Volume.

1. Launch iLO Integrated Remote Console of this server and set the ESXi 6.7/7.0 ISO file as virtual CD-ROM/DVD image file. Power on the server.

1. Install ESXi 6.7/7.0.

1. Reboot the Compute Blade. [required for the OS to create the state.tgz folder]

1. To capture the ESXi 6.7/7.0 image:
  
    1.  Shutdown the server gracefully by pressing F12, and shutting it down, or by giving ‘poweroff’ command from SSH console, or by, clicking on the Momentary Press from iLO console of the server.

    1.  Perform an as-is capture using "HPE - Foundation 1.0 - capture OS Volume as is" build plan to create the "as-is" golden image of the OS. (NOTE: There are no generalization - capture scripts for ESXi 6.7). ESXi update using VUM is supported. Please make sure you set the minimum personalization required for the host to be added to vCenter. The personalization attributes set on the host will persist in the golden image and same should be overwritten during the subsequent deployments (using Plan Scripts).

    1.  Deploy another server with the golden image captured in previous step and build plan of your choice to boot the server.

1. To install VIBs or updates via virtual media and then capture ESXi 6.7/7.0 image:

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
    
    1. Perform an as-is capture using "HPE - Foundation 1.0 - capture OS Volume as is" build plan to create the "as-is" golden image of the OS. (NOTE: There are no generalization - capture scripts for ESXi 6.7/7.0)

Note: The ports on which the physical NICs are configured for various connections defined in sever-profile/ server-profile template, before capturing the image, will be retained. Please ensure to use the same ports for subsequent deployments.

## Known Issues:
- In case of ungraceful or forceful shutdown of the server (within an hour of the deployment), there may be a loss of personalization.
  Please refer to the VMware article for the same: https://kb.vmware.com/s/article/2001780
  
- When "Virtual NIC" in iLO is enabled deployment will fail, the iLO Virtual NIC needs to be disabled for a successful deployment, which can be done from the UI of iLO page under Security tab -> Access Settings tab -> edit the Network section -> and remove the checkmark from the iLO Virtual NIC. Once this is done, select the “Reset iLO” button at the top of the page to allow this setting to take effect.

	The iLO virtual nic is discussed in the following customer advisory:
	https://support.hpe.com/hpesc/public/docDisplay?docLocale=en_US&docId=a00104665en_us

	Alternatively, the REST API call to disable this is: 
	
	PATCH /redfish/v1/Managers/{managerId}/

		{
		    "Oem": {
			"Hpe": {
			    "VirtualNICEnabled": false
			}	
		    }
		}
		
     Ref: https://hewlettpackard.github.io/ilo-rest-api-docs/ilo5/?shell#using-the-virtual-nic
  

## Artifact Bundle Contents:

--------------------------------------------------------------------------------

                    File name: HPE-ESXi-2021-07-26-v6.10.zip
                Name (in manifest): HPE-ESXi-2021-07-26-v6.10
                       Description: ImageStreamer artifacts for ESXi 6.5. (c) Copyright 2018-2021 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the \"License\");you may not use this file except in compliance with the License
                             Dated: 2021-09-13 (19:21:11)

--------------------------------------------------------------------------------

Build Plans:

               Name: HPE - ESXi - deploy with multiple management NIC HA config-2021-07-26 (Type:deploy)
        Description: Deploy ESXi 6.5 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. (c) Copyright 2018-2021 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0  (the "License");...


               Name: HPE- ESXi - deploy in single frame non-HA config-2021-07-26 (Type:deploy)
        Description: Personalize ESXi 6.5 image with single management NIC, hostname, domain name, root password and ssh settings. (c) Copyright 2018-2021 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0  (the "License");...


               Name: HPE - ESXi - generalize full state -  2020-12-10 (Type:capture)
        Description: Remove personalization settings from ESXi 6.5 images.
                     (c) Copyright 2018-2020 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the "License"); ...



Plan Scripts:

               Name: HPE - ESXi - repack state - 2017-03-15 (general)
           FullName: 00e3f9f6-502c-4c01-a15b-563c47514b11_planscript.json
        Description: Pack and replace ESXi host state into ESXi host OS Volume


               Name: HPE - ESXi - generalize host configuration - 2017-07-12 (capture)
           FullName: 230ba20e-24af-4b9b-b5f4-499a88bf99f2_planscript.json
        Description: Remove personalization settings from ESXi 6.5 images


               Name: HPE - ESXi - unpack state - 2017-07-07 (general)
           FullName: 3a1a5cfe-23b5-4997-b6fe-2249c1078db7_planscript.json
        Description: Copy out and unpack ESXi host state


               Name: HPE - ESXi - remove system uuid - 2017-08-02 (capture)
           FullName: 3ab9f073-844f-47e1-9cc0-e08041dc2c0d_planscript.json
        Description: remove system uuid from esx.conf


               Name: HPE - ESXi - umount - 2017-03-15 (general)
           FullName: 3cbd1366-8c6a-4a63-95a2-e9c0f0a200c9_planscript.json
        Description: Cleanup and unmount file systems


               Name: HPE - ESXi - configure ssh- 2017-12-15 (deploy)
           FullName: 47b431e3-456f-428e-ac3b-3dd0b4fa5500_planscript.json
        Description: Configure ssh


               Name: HPE - ESXi - Clear - Network - 2021-07-26 (deploy)
           FullName: 64e91f8b-8cf4-4d64-8d6c-e9484f2d8502_planscript.json
        Description: Clear Old vSwitches and VMK's on the imagestreamer captured GI


               Name: HPE - ESXi - configure management 2nd NIC HA- 2017-07-07 (deploy)
           FullName: 6887b69b-b581-4654-8953-c36cda6ad480_planscript.json
        Description: Configure ESXi host management 2nd NIC for HA


               Name: HPE - ESXi - generalize onetime - 2017-09-27 (capture)
           FullName: a5f22eb6-e23f-4210-af79-98981f2eca3f_planscript.json
        Description: Clear the contents of local.sh in onetime.tgz and revert it to default contents


               Name: HPE - ESXi - mount - 2020-12-10 (general)
           FullName: b71c5005-7004-45ca-a2ef-6d8b069dd0d2_planscript.json
        Description: Mount ESXi /bootbank


               Name: HPE - ESXi - configure management 1st NIC- 2017-08-22 (deploy)
           FullName: bd629b0e-c0e0-423f-8eaf-2386421f9885_planscript.json
        Description: Configure ESXi host management network


               Name: HPE - ESXi - set password - 2017-03-15 (deploy)
           FullName: c48fe9f0-7111-4cbd-9cc6-445b77f6f5ab_planscript.json
        Description: Configure host password


               Name: HPE - ESXi - mpio - configure iSCSI boot HA - 2019-08-26 (deploy)
           FullName: fc2101e0-f677-4d50-84ef-d22d7b3a7f2f_planscript.json
        Description: Configures HA for iSCSI boot path for ESXi.
                     This script can be used in multi frame environment containing a pair of ImageStreamer appliances.




--------------------------------------------------------------------------------

                    File name: HPE-ESXi-6.7-2021-01-21-v6.10.zip
                Name (in manifest): HPE-ESXi-6.7-2021-01-21-v6.10
                       Description: Artifacts to verify Image Streamer installation and configuration. (c) Copyright 2017 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the \"License\");you may not use this file except in compliance.
                             Dated: 2021-02-19 (07:16:57)

--------------------------------------------------------------------------------

Build Plans:

               Name: HPE - ESXi 6.7 - deploy with multiple management NIC HA config - 2020-03-27 (Type:deploy)
        Description: Deploy ESXi 6.7 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. (c) Copyright 2018-2020 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the "License"); ...


               Name: HPE - ESXi 6.7 - deploy in single frame non-HA config - 2021-01-21 (Type:deploy)
        Description: Deploy ESXi 6.7 in a single-frame environment containing one ImageStreamer appliance. This buildplan does not configure HA for iSCSI boot connections to ESXi volume. (c) Copyright 2018-2020 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the "License"); ...



Plan Scripts:

               Name: HPE - ESXi - repack state - 2017-03-15 (general)
           FullName: 0782a5de-9e0a-4c2d-b9f5-ac70284af377_planscript.json
        Description: Pack and replace ESXi host state into ESXi host OS Volume


               Name: HPE - ESXi - umount - 2017-03-15 (general)
           FullName: 0bc7c183-4054-4a31-a09e-932c46ca6d8c_planscript.json
        Description: Cleanup and unmount file systems


               Name: HPE - ESXi 6.7 - generalize state - 2020-03-27 (general)
           FullName: 118a02cd-528a-401b-ad98-36b72614b287_planscript.json
        Description: Clear the contents of local.sh in state.tgz and revert it to default contents. Check /tmp/hpe.log for all the deleted entries


               Name: HPE - ESXi 6.7 - remove system uuid - 2018-08-02 (deploy)
           FullName: 14193a80-58e9-44d9-ab48-0d73c703ea73_planscript.json
        Description: Remove system uuid from esx.conf


               Name: HPE - ESXi 6.7 - clear local - 2020-03-27 (general)
           FullName: 3488054a-1951-422a-ba79-92f46907edc4_planscript.json
        Description: Clear the contents of local.sh post personalization. Corrects the mount point. Refer VMware knowledgebase 2148321 for details


               Name: HPE - ESXi - configure ssh - 2017-12-15 (deploy)
           FullName: 3d52cef4-f33a-4d03-a7f9-96c364d72bf7_planscript.json
        Description: Configure ssh


               Name: HPE - ESXi 6.7 - unpack state - 2018-08-02 (general)
           FullName: 4c6decf9-448b-44af-8cd1-76ed6157e3be_planscript.json
        Description: Copy out and unpack ESXi host state


               Name: HPE - ESXi  - configure iSCSI connection non-HA - 2021-01-21 (deploy)
           FullName: 74d18598-0105-4a4b-94b7-a846019d0a9b_planscript.json
        Description: Configures non-HA iSCSI boot path for ESXi. This script can be used in single frame environment containing one ImageStreamer appliance.


               Name: HPE - ESXi 6.7 - replace initiator IP - 2018-08-02 (deploy)
           FullName: 7544865e-b768-4886-82ae-5ad3186a7f8f_planscript.json
        Description: Build script to replace initiator ip


               Name: HPE - ESXi 6.7 - remove host-server IP - 2019-07-19 (deploy)
           FullName: 76ad5e0b-f272-4de1-930d-6a91fa10f429_planscript.json
        Description: Removing the host IP, server IP and the host key


               Name: HPE - ESXi - set password - 2017-03-15 (deploy)
           FullName: 7c2a7ad5-48b9-4b4b-986a-36bb57fea3f3_planscript.json
        Description: Configure host password


               Name: HPE - ESXi - mount - 2018-12-03 (general)
           FullName: 8600aeab-f365-4ace-8863-e17f250b6b89_planscript.json
        Description: Mount ESXi /bootbank


               Name: HPE - ESXi - configure management 1st NIC - 2017-08-22 (deploy)
           FullName: 8a67408f-b4db-479c-a229-5d7aa2920707_planscript.json
        Description: Configure ESXi host management network


               Name: HPE - ESXi - mpio - configure iSCSI boot HA - 2020-03-27 (deploy)
           FullName: b8c0699a-dfdc-49df-9746-a5f39ad350b5_planscript.json
        Description: Configures HA for iSCSI boot path for ESXi.
                     This script can be used in multi frame environment containing a pair of ImageStreamer appliances.


               Name: HPE - ESXi - configure management 2nd NIC HA - 2017-07-07 (deploy)
           FullName: c95da095-047e-430e-94c9-283ae34d18bb_planscript.json
        Description: Configure ESXi host management 2nd NIC for HA
