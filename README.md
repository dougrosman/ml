# ml
Guides, tips and resources for machine learning

## Removing Linux from Windows 10 Dual Boot
1. Remove partition using diskmgmt
2. Insert Windows 10 USB Install media
3. Restart computer and boot into the USB Install Media
4. Click through until you see 'Repair your computer'
5. Select 'Troubleshoot'
6. Select 'Advanced Options'
7. Select 'Command Prompt'
8. Type: 
    ```
    bootrec.exe /fixmbr
    ```
9. Restart and check to make sure the linux bootloader is gone

## Installing Linux
1. Insert Ubuntu 20.04 USB Media
2. Boot into the USB Media (make sure to select the UEFI version)
3. Select 'Install Ubuntu'
4. Select keyboard layout
5. Make sure **Normal Installation** is selected
6. Check off **Download updates while installing Ubuntu** and **Install 3rd party software...**
7. Select **Something else**
8. Select the Free Space partition
9. Press '+'
   1.  Size: 100% the size of the partition
   2.  **Logical** partition
   3.  **Beginning of the space**
   4.  Use as **Ext4 journaling file system**
   5.  Mount point: **/** (root)
10. Select Linux drive for the boot loader installation
11. Select **Install Now**
12. Credentials Example:
    1.  Your name: ```ATS-401-03-ubuntu20.04```
    2.  computer name: ```ats-401-03-ubuntu20.04```
    3.  username: ```ats-401-03```
    4.  password: ********
13. Finish the installation

## Installing dependencies for Stylegan2
