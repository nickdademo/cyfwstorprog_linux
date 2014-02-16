cyfwstorprog_linux
==================

Linux command-line tool to write firmware to SD/eMMC media connected to the Cypress FX3S.

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
