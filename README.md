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