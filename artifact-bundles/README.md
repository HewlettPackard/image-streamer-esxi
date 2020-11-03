# ESXi 5.x to ESXi 6.5 and ESXi 6.7 to ESXi 7.0 artifacts for ImageStreamer v5.4 release
## Note:
- For versions of ESXi 5.x to ESXi 6.5 Please use HPE-ESXi-xxxx-xx-xx-v5.4.zip Artifact Bundle
- For versions of ESXi 6.7 and onwards Please use HPE-ESXi-6.7-xxxx-xx-xx-v5.4.zip Artifact Bundle
- All artifact bundles in this repo are compatible with ImageStreamer v5.4 release
- Click on 'Branch:' drop down menu on this page to get artifact bundles for other ImageStreamer releases
- The following ESXi versions are supported
	- ESXi 6.0 (ESXi 6.0 U2, ESXi 6.0 U3) 
	- ESXi 6.5 (ESXi 6.5, ESXi 6.5 U1, ESXi 6.5 U2)
	- ESXi 6.7 (ESXi 6.7, ESXi 6.7 U1, ESXi 6.7 U2, ESXi 6.7 U3)
	- ESXi 7.0 (ESXi 7.0)

## Version History:
HPE-ESXi-2019-08-26-v5.4.zip
   - Modified MPIO script to remove default vmk0 - remove old MAC and portID

HPE-ESXi-6.7-2020-10-27-v5.4.zip
   - Modified script to remove default vSwitch and vmnic created on GI captured from i3s deployed node	
   - Has corrective action as per VMware knowledgebase 2148321 for remounting bootbank from /tmp to /sda

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
  

## Artifact Bundle Contents:

--------------------------------------------------------------------------------

	            File name: HPE-ESXi-2019-08-26-v5.4.zip
		Name (in manifest): HPE-ESXi-2019-08-26-v5.4
		       Description: ImageStreamer artifacts for ESXi 5.x and ESXi 6.x till 6.5. 
		             Dated: 2020-10-21 

--------------------------------------------------------------------------------

Build Plans:

	       Name: HPE - ESXi - deploy with multiple management NIC HA config-2019-08-26 (Type:deploy)
	Description: Deploy ESXi 5.x - 6.5 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. 


	       Name: HPE - ESXi - generalize full state -  2018-12-03 (Type:capture)
	Description: Remove personalization settings from ESXi 5.x - 6.5 images.
	             

	       Name: HPE- ESXi - deploy in single frame non-HA config-2019-07-05 (Type:deploy)
	Description: Personalize ESXi 5.x - 6.5 image with single management NIC, hostname, domain name, root password and ssh settings. 


Plan Scripts:

	       Name: HPE - ESXi - unpack state - 2017-07-07 (general)
	   FullName: 081ea74c-e79c-41df-a2e3-e0c7cbcb3eb6_planscript.json
	Description: Copy out and unpack ESXi host state


	       Name: HPE - ESXi - generalize host configuration - 2017-07-12 (capture)
	   FullName: 1d0e78c2-b006-4745-b300-ec5d7dad3238_planscript.json
	Description: Remove personalization settings from ESXi 5.x and 6.x images


	       Name: HPE - ESXi - configure management 2nd NIC HA- 2017-07-07 (deploy)
	   FullName: 2347ec3d-a1fd-48a1-82b1-f67cae3a9a28_planscript.json
	Description: Configure ESXi host management 2nd NIC for HA


	       Name: HPE - ESXi - mpio - configure iSCSI boot HA - 2019-08-26 (deploy)
	   FullName: 529d45a3-be0d-436b-825e-c8a48036b17d_planscript.json
	Description: Configures HA for iSCSI boot path for ESXi. 
	             This script can be used in multi frame environment containing a pair of ImageStreamer appliances.


	       Name: HPE - ESXi - configure ssh- 2017-12-15 (deploy)
	   FullName: 574b189b-2816-46f2-ae82-fb00c7d8ab6f_planscript.json
	Description: Configure ssh


	       Name: HPE - ESXi - set password - 2017-03-15 (deploy)
	   FullName: 5b19e75e-33a9-4749-9215-9f5ce0af9879_planscript.json
	Description: Configure host password


	       Name: HPE - ESXi - umount - 2017-03-15 (general)
	   FullName: 9c9883d2-d3b7-4b89-a690-49c1ae5e1ae5_planscript.json
	Description: Cleanup and unmount file systems


	       Name: HPE - ESXi - mount - 2018-12-03 (general)
	   FullName: a1b7de18-60f1-404b-9582-af6006b08d8e_planscript.json
	Description: Mount ESXi /bootbank


	       Name: HPE - ESXi - generalize onetime - 2017-09-27 (capture)
	   FullName: a4ab8199-e43e-475f-806c-4f49e49a6f5d_planscript.json
	Description: Clear the contents of local.sh in onetime.tgz and revert it to default contents


	       Name: HPE - ESXi - remove system uuid - 2017-08-02 (capture)
	   FullName: bf023817-086e-4070-98bc-de0149278796_planscript.json
	Description: remove system uuid from esx.conf


	       Name: HPE - ESXi - configure management 1st NIC- 2017-08-22 (deploy)
	   FullName: cb245a2c-789a-45a2-b856-e2abbbb25f3e_planscript.json
	Description: Configure ESXi host management network


	       Name: HPE - ESXi - repack state - 2017-03-15 (general)
	   FullName: dd49651c-69bf-40a4-8001-f2c1911eab2b_planscript.json
	Description: Pack and replace ESXi host state into ESXi host OS Volume





--------------------------------------------------------------------------------

                    File name: HPE-ESXi-6.7-2020-10-27-v5.4.zip
                Name (in manifest): HPE-ESXi-6.7-2020-10-27-v5.4
                       Description: ImageStreamer artifacts for ESXi 6.7. (c) Copyright 2018-2020 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the \"License\");you may not use this file except in compliance with the License
                             Dated: 2020-09-08 (09:13:34)

--------------------------------------------------------------------------------

Build Plans:

               Name: HPE - ESXi 6.7 - deploy in single frame non-HA config - 2020-03-27 (Type:deploy)
        Description: Deploy ESXi 6.7 in a single-frame environment containing one ImageStreamer appliance. This buildplan does not configure HA for iSCSI boot connections to ESXi volume. (c) Copyright 2018-2020 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the "License"); ...


               Name: HPE - ESXi 6.7 - deploy with multiple management NIC HA config - 2020-03-27 (Type:deploy)
        Description: Deploy ESXi 6.7 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. (c) Copyright 2018-2020 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the "License"); ...



Plan Scripts:

               Name: HPE - ESXi 6.7 - remove host-server IP - 2019-07-19 (deploy)
           FullName: 0ea4b06b-df67-48b2-98a7-811b6dfba632_planscript.json
        Description: Removing the host IP, server IP and the host key


               Name: HPE - ESXi - configure management 1st NIC - 2017-08-22 (deploy)
           FullName: 296a98a0-1a35-4475-829f-5d97b4b0e8d6_planscript.json
        Description: Configure ESXi host management network


               Name: HPE - ESXi - umount - 2017-03-15 (general)
           FullName: 401ac40b-bbcb-4ef0-8f5c-21a81a006d51_planscript.json
        Description: Cleanup and unmount file systems


               Name: HPE - ESXi 6.7 - remove system uuid - 2018-08-02 (deploy)
           FullName: 444f97ba-0a77-4a7e-837d-55d9c45647d8_planscript.json
        Description: Remove system uuid from esx.conf


               Name: HPE - ESXi - configure management 2nd NIC HA - 2017-07-07 (deploy)
           FullName: 5e8fdb72-35de-48f8-b23d-cd5ddeb5d81f_planscript.json
        Description: Configure ESXi host management 2nd NIC for HA


               Name: HPE - ESXi - mount - 2018-12-03 (general)
           FullName: 80b0564c-2569-42ed-aabf-9b51ffd72e0d_planscript.json
        Description: Mount ESXi /bootbank


               Name: HPE - ESXi 6.7 - generalize state - 2020-03-27 (general)
           FullName: 84b2b367-418b-4038-9a92-a4751f30f411_planscript.json
        Description: Clear the contents of local.sh in state.tgz and revert it to default contents. Check /tmp/hpe.log for all the deleted entries


               Name: HPE - ESXi - repack state - 2017-03-15 (general)
           FullName: 862bc3d5-e068-44cc-a3f5-704957340753_planscript.json
        Description: Pack and replace ESXi host state into ESXi host OS Volume


               Name: HPE - ESXi - mpio - configure iSCSI boot HA - 2020-03-27 (deploy)
           FullName: 88fb759e-a5b0-4e4a-81f7-be2ae4a1f77a_planscript.json
        Description: Configures HA for iSCSI boot path for ESXi.
                     This script can be used in multi frame environment containing a pair of ImageStreamer appliances.


               Name: HPE - ESXi - set password - 2017-03-15 (deploy)
           FullName: 8c1229c8-d378-48b9-9fc6-e04f316bb940_planscript.json
        Description: Configure host password


               Name: HPE - ESXi 6.7 - replace initiator IP - 2018-08-02 (deploy)
           FullName: 9bc882bf-7c7b-4903-87fc-a44c28ab492e_planscript.json
        Description: Build script to replace initiator ip


               Name: HPE - ESXi 6.7 - unpack state - 2018-08-02 (general)
           FullName: b71c7601-8d2d-4e40-87ee-78e505b4b0ed_planscript.json
        Description: Copy out and unpack ESXi host state


               Name: HPE - ESXi 6.7 - clear local - 2020-03-27 (general)
           FullName: c074ee7e-244e-4c4f-bd58-69ad605d9b3f_planscript.json
        Description: Clear the contents of local.sh post personalization. Corrects the mount point. Refer VMware knowledgebase 2148321 for details


               Name: HPE - ESXi - configure ssh - 2017-12-15 (deploy)
           FullName: f655cdae-c6b1-4df0-be73-f554043be7bf_planscript.json
        Description: Configure ssh
