# ESXi 6.5 and ESXi 6.7 to ESXi 7.0 artifacts for ImageStreamer v6.10 release
## Note:
- For versions of ESXi 6.5 Please use HPE-ESXi-xxxx-xx-xx-v6.10.zip Artifact Bundle
- For versions of ESXi 6.7 and onwards Please use HPE-ESXi-6.7-xxxx-xx-xx-v6.10.zip Artifact Bundle
- For versions of ESXi 7.0 Update 2 and onwards Please use HPE-ESXi-7.0-xxxx-xx-xx-v6.10.zip Artifact Bundle
- All artifact bundles in this repo are compatible with ImageStreamer v6.10 release
- Click on 'Branch:' drop down menu on this page to get artifact bundles for other ImageStreamer releases
- The following ESXi versions are supported
	- ESXi 6.5 (ESXi 6.5, ESXi 6.5 U1, ESXi 6.5 U2)
	- ESXi 6.7 (ESXi 6.7, ESXi 6.7 U1, ESXi 6.7 U2, ESXi 6.7 U3)
	- ESXi 7.0 (ESXi 7.0, ESXi 7.0 U1, ESXi 7.0 U2)

## Version History:
HPE-ESXi-2020-12-10-v6.10.zip
   - Modified MPIO script to remove default vmk0 - remove old MAC and portID
   - Plan script change to handle attributes when GI with multiple updates is used.

HPE-ESXi-6.7-2020-10-27-v6.10.zip
   - Modified script to remove default vSwitch and vmnic created on GI captured from i3s deployed node	
   - Has corrective action as per VMware knowledgebase 2148321 for remounting bootbank from /tmp to /sda

HPE-ESXi-6.7-2021-01-21-v6.10.zip
   - Modified iBFT script to handle iSCSI path DEAD issue when a non-HA build plan with one Deployment connection is used for deployment.

HPE-ESXi-7.0-2021-05-10-v6.10.zip
   - Use this Artifact for ESXi version 7.0 Update 2 and higher.

## Golden Image creation for ESXi 6.7/7.0:

An Image Streamer Golden Image for ESXi 6.7 is to be captured ‘as is’, without any generalization scripts. This also introduces a constraint that the ESXi 6.7 image to be captured, shouldn’t contain any personalization. 
Any personalization, if done on the host before capturing the image will be retained and should be overwritten during the subsequent deployments. 


1. Ensure that you have access to ESXi 6.7/7.0 ISO file.

1. Create a server profile with “HPE - Foundation 1.0 - create empty OS Volume” as OS Deployment plan and a server hardware of desired hardware type. Set an appropriate value for volume size in MiB units, say 20480 MiB for ESXi 6.7 and below. The HPE Synergy Server will be configured for access to this empty OS Volume.

1. Installing ESXi 7.0 and above versions requires a boot device that is a minimum of 8 GB for USB or SD devices, and 32 GB for other device types. When booting from a local disk, SAN or iSCSI LUN, a 32 GB disk is required to allow for the creation of system storage volumes, which include a boot partition, boot banks, and a VMFS-L based ESX-OSData volume.

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

                    File name: HPE-ESXi-2020-12-10-v6.10.zip
                Name (in manifest): HPE-ESXi-2020-12-10-v6.10
                       Description: ImageStreamer artifacts for ESXi 6.5. (c) Copyright 2018-2020 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the \"License\");you may not use this file except in compliance with the License
                             Dated: 2020-12-10 (15:28:13)

--------------------------------------------------------------------------------

Build Plans:

               Name: HPE- ESXi - deploy in single frame non-HA config-2020-12-10 (Type:deploy)
        Description: Personalize ESXi 6.5 image with single management NIC, hostname, domain name, root password and ssh settings. (c) Copyright 2018-2020 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0  (the "License");...


               Name: HPE - ESXi - generalize full state -  2020-12-10 (Type:capture)
        Description: Remove personalization settings from ESXi 6.5 images.
                     (c) Copyright 2018-2020 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the "License"); ...


               Name: HPE - ESXi - deploy with multiple management NIC HA config-2020-12-10 (Type:deploy)
        Description: Deploy ESXi 
	6.5 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. (c) Copyright 2018-2020 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0  (the "License");...



Plan Scripts:

               Name: HPE - ESXi - unpack state - 2017-07-07 (general)
           FullName: 5de97971-8250-4a80-aa47-bbd7b406cd03_planscript.json
        Description: Copy out and unpack ESXi host state


               Name: HPE - ESXi - configure ssh- 2017-12-15 (deploy)
           FullName: 65e348e1-08a4-4c11-be4b-4c234e5d3ebb_planscript.json
        Description: Configure ssh


               Name: HPE - ESXi - generalize host configuration - 2017-07-12 (capture)
           FullName: 7e2df5f6-339b-4e2d-8ecf-c6d138340d63_planscript.json
        Description: Remove personalization settings from ESXi 6.x images


               Name: HPE - ESXi - generalize onetime - 2017-09-27 (capture)
           FullName: 8bf19979-e7a1-4bbe-a41a-7ea2db9dc947_planscript.json
        Description: Clear the contents of local.sh in onetime.tgz and revert it to default contents


               Name: HPE - ESXi - configure management 2nd NIC HA- 2017-07-07 (deploy)
           FullName: afc18462-19a1-4104-a273-4a4aebc8efa6_planscript.json
        Description: Configure ESXi host management 2nd NIC for HA


               Name: HPE - ESXi - umount - 2017-03-15 (general)
           FullName: b748d031-d5fe-40af-8f93-9f659d057742_planscript.json
        Description: Cleanup and unmount file systems


               Name: HPE - ESXi - configure management 1st NIC- 2017-08-22 (deploy)
           FullName: cf595471-4a6b-42d5-911d-d4b4bdd574bb_planscript.json
        Description: Configure ESXi host management network


               Name: HPE - ESXi - repack state - 2017-03-15 (general)
           FullName: e1bfec77-cc64-4a04-8965-e597d4efc7ed_planscript.json
        Description: Pack and replace ESXi host state into ESXi host OS Volume


               Name: HPE - ESXi - mount - 2020-12-10 (general)
           FullName: e6d9922b-6e29-4e64-9a8d-17cae868a2a9_planscript.json
        Description: Mount ESXi /bootbank


               Name: HPE - ESXi - set password - 2017-03-15 (deploy)
           FullName: e9ff41db-e548-4959-8ac1-cd41b7fb48a1_planscript.json
        Description: Configure host password


               Name: HPE - ESXi - mpio - configure iSCSI boot HA - 2019-08-26 (deploy)
           FullName: f1b68384-cb9d-49a5-bded-7d9a7944e093_planscript.json
        Description: Configures HA for iSCSI boot path for ESXi.
                     This script can be used in multi frame environment containing a pair of ImageStreamer appliances.


               Name: HPE - ESXi - remove system uuid - 2017-08-02 (capture)
           FullName: f2018b6c-9f02-469a-983b-9853d054d1de_planscript.json
        Description: remove system uuid from esx.conf




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
	
	
	
--------------------------------------------------------------------------------

                    File name: HPE-ESXi-7.0-2021-05-10-v6.10.zip
                Name (in manifest): HPE-ESXi-7.0-2021-05-10-v6.1v0
                       Description: Artifacts to verify Image Streamer installation and configuration. (c) Copyright 2021 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the \"License\");you may not use this file except in compliance
                             Dated: 2021-06-07 (19:53:53)

--------------------------------------------------------------------------------

Build Plans:

               Name: HPE - ESXi 7.0 - deploy in single frame non-HA config - 2021-05-10 (Type:deploy)
        Description: Deploy ESXi 7.0 in a single-frame environment containing one ImageStreamer appliance. This buildplan does not configure HA for iSCSI boot connections to ESXi volume. (c) Copyright 2018-2021 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the "License"); ...


               Name: HPE - ESXi 7.0 - deploy with multiple management NIC HA config - 2020-05-10 (Type:deploy)
        Description: Deploy ESXi 7.0 in a multi-frame environment containing a pair of ImageStreamer appliances. This buildplan configures HA for iSCSI boot connections to ESXi volume. (c) Copyright 2018-2021 Hewlett Packard Enterprise Development LP. Licensed under the Apache License, Version 2.0 (the "License"); ...



Plan Scripts:

               Name: HPE - ESXi 7.0 - set password - 2021-05-10 (deploy)
           FullName: 0d2d722b-2242-42b8-96a5-a0c636462825_planscript.json
        Description: Configure host password


               Name: HPE - ESXi 7.0 - configure management 1st NIC - 2021-05-10 (deploy)
           FullName: 10e9b0b1-e604-428a-aaa2-f6ddd8c16fe7_planscript.json
        Description: Configure ESXi host management network and removes hard coded entries from esx.conf file


               Name: HPE - ESXi 7.0 - configure ssh - 2021-05-10 (deploy)
           FullName: 17c2efbb-ff29-4000-9ac0-a0aa162c19eb_planscript.json
        Description: Configure ssh


               Name: HPE - ESXi 7.0 - clear local - 2021-05-10 (general)
           FullName: 2a637461-c9e3-4d6d-9523-91b8d1442d5c_planscript.json
        Description: Clear the contents of local.sh post personalization. Corrects the mount point. Refer VMware knowledgebase 2148321 for details


               Name: HPE - ESXi 7.0 - configure iSCSI connection non-HA - 2021-05-10 (deploy)
           FullName: 6593303e-815b-4164-9ff6-327693f92d05_planscript.json
        Description: Configures non-HA iSCSI boot path for ESXi. This script can be used in single frame environment containing one ImageStreamer appliance.


               Name: HPE - ESXi 7.0 - create custom.tgz custom module - 2021-05-10 (general)
           FullName: 678e5e23-0d88-4bf3-a6c4-24e4ff1bcef1_planscript.json
        Description: Create 999.local.sh file inside /etc/rc.local.d/ and compress in to custom.tgz module


               Name: HPE - ESXi 7.0 - add custom.tgz module to boot.conf  - 2021-05-10 (general)
           FullName: 779947fa-e7c8-4e92-abd2-0fe1fb4c315e_planscript.json
        Description: add custom.tgz module to boot.cfg file in BOOTBANK1


               Name: HPE - ESXi 7.0 - configure management 2nd NIC HA - 2021-05-10 (deploy)
           FullName: 80e77a84-7ea2-4902-a4af-3da96b52c685_planscript.json
        Description: Configure ESXi host management 2nd NIC for HA


               Name: HPE - ESXi 7.0 - repack custom.tgz module - 2021-05-10 (general)
           FullName: a23a609a-46fb-4199-bbae-0d48016f85c1_planscript.json
        Description: repack custom.tgz


               Name: HPE - ESXi 7.0 - mount - 2021-05-10 (general)
           FullName: d32af1aa-1ad4-466c-b288-3eeec0ddbc9a_planscript.json
        Description: Mount ESXi /bootbank


               Name: HPE - ESXi 7.0 - generalize Host - 2021-05-10 (general)
           FullName: e3026a77-4494-42e5-bf59-39bed4bd21c0_planscript.json
        Description: Deletes all ols vSwitches, VMKs and Portgroup from GI. Check /tmp/hpe.log for all the deleted entries


               Name: HPE - ESXi 7.0 - umount - 2021-05-10 (general)
           FullName: e6f00650-27b6-4ce5-b062-5766689c84cd_planscript.json
        Description: Cleanup and unmount file systems


               Name: HPE - ESXi 7.0 - mpio - configure iSCSI boot HA - 2021-05-10 (deploy)
           FullName: ff081a5b-2d33-4ef2-b3f6-6815feb64f0d_planscript.json
        Description: Configures HA for iSCSI boot path for ESXi.
                     This script can be used in multi frame environment containing a pair of ImageStreamer appliances.
