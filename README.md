# ml
Guides, tips and resources for machine learning

## Removing Linux from Windows 10 Dual Boot
1. Remove partition using diskmgmt
1. Insert Windows 10 USB Install media
1. Restart computer and boot into the USB Install Media
1. Click through until you see 'Repair your computer'
1. Select 'Troubleshoot'
1. Select 'Advanced Options'
1. Select 'Command Prompt'
1. Type: ```bootrec.exe /fixmbr```