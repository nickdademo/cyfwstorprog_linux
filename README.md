cyfwstorprog_linux
==================

Linux command-line tool to write a bootable firmware binary to SD/eMMC media connected to the S0 port of the Cypress FX3S.

##Background
Cypress Semiconductor provides a Windows-only tool to write firmware to SD/eMMC media connected to the FX3S as a part of the EZ-USB FX3 SDK (http://www.cypress.com/?rID=57990). However, unfortunately, no Linux version of this tool is provided.

*cyfwstorprog_linux* is a Linux port of this tool and was created using the source code of the Windows tool (kindly provided by Cypress) as a guide.

There are a number of slight differences between *cyfwstorprog_linux* and the original Windows version of the tool:  
* *cyfwstorprog_linux* does not have the feature to program the Cypress BootWriter image (CyStorBootWriter.img) to the FX3S RAM. **Therefore, before using this tool, CyStorBootWriter.img must be pre-programmed to the FX3S.**
* Firmware image size check (against the target partition size) has been included.
* The target Cypress device is specified using the Linux device path (e.g. /dev/sdb) instead of a VID/PID.

**This tool has been tested with Cypress BootWriter v0.01 as provided in EZ-USB FX3 SDK v1.3.1.**


##Compiling
Simply run the make command from the source directory:   
`$ make`

_Note: Tool has been tested using GCC 4.6.3._

##Usage
A) Write firmware:  
`$ cyfwstorprog -img:<FW_Image> -dev:<Device_Path> [-bootp:<Boot_Part_Location>] [-nuserp:<Num_UserArea_Partitions>] [-psizes:<PartitionSizes>]`

B) Display partition information:  
`$ cyfwstorprog -dev:<Device_Path> -disponly`

C) Delete partition:  
`$ cyfwstorprog -dev:<Device_Path> -delpart`

###Parameters
####Required:
**-img:** FX3S firmware image file path (.img)  
**-dev:** FX3S Linux device path (e.g. /dev/sdb)  
####Optional:
**-bootp:**  Target boot partition location for firmware programming: *user, boot1, boot2* (**Default=user**)  
**-nuserp:**  Number of non-boot User partitions to create: *1, 2, 3* (**Default=1**)  
**-psizes:**  Specify User partition sizes in number of blocks: *user1_size#user2_size#user3_size* (**Default=Allocate evenly**)  

**-disponly:**  Display partition information only (no firmware writing will be performed)  
**-delpart:**  Delete all User partitions only (no firmware writing will be performed)

*Please refer to the document (cyfwstorprog_usage.txt) supplied with the original tool (contained in the Cypress EZ-USB FX3 SDK) for further usage information.*
