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

## Must-do things once Ubuntu is installed:
1. re-boot
2. Install Teamviewer and assign to account/set up passwords
3. Make sure computer won't auto-suspend. Make sure you can log in with Teamviewer if computer logs out.

## Installing dependencies for Stylegan2
#### Watch: [StyleGAN2 on Ubuntu 20.04 - tutorial](https://www.youtube.com/watch?v=ZMQfHC3O7eY)
#### Note: At this point, no restart is required for things to work. For the sake of time, you can move on to installing Ubuntu and Teamviewer on other machines, and install dependencies at any time by remote access through Teamviewer.
1. Check **Software and Updates** to make sure latest Nvidia drivers are installed
2. Open Terminal
    ```
    sudo apt update
    sudo apt install build-essential
    sudo apt install nvidia-cuda-toolkit
    nvcc -V
    ```
3. [Download cuDNN Runtime Library for Ubuntu 18.04 (Deb)](https://developer.nvidia.com/rdp/cudnn-download) for Cuda 10.1
    ```
    cd Downloads
    sudo dpkg -i ./libcudnn7_7.6.5.32-1+cuda10.1_amd64.deb
    ```
4. [Download](https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh) and Install Anaconda with Python Version 3.7
    ```
    chmod +x ./Anaconda3-2020.02-Linux-x86_64.sh
    ./Anaconda3-2020.02-Linux-x86_64.sh
    ```
5. Follow the command prompts (yes to everything, basically)
6. Close and reopen Terminal
7. Create a Conda virtual environment using the Anaconda Navigator
    ```
    anaconda-navigator
    ```
8. Create a new environment called **stylegan2**
9. Refresh the index for all + installed packages
10. Add These packages/libraries. To change any of the versions from the default, right-click on the check box next to the package name and change the version from there.
    1. Python 3.6.10 (if anaconda doesn't allow you to pick 3.6 at first, select 3.7 for now, then change it to 3.6.10 from the installed packages index later.)
    2. tensorflow-gpu version 1.15 (make sure)
    3. pillow
    4. requests
11. Close the navigator
    ```
    conda activate stylegan2
    ```
12. ```cd``` into the StyleGAN2 folder
13. Test your Cuda installation
    ```
    nvcc test_nvcc.cu -o test_nvcc -run
    ```
14. I don't know what this does but you should do it.
    ```
    ln -s /usr/bin/ptxas ./bin/
    ```
15. There's a bug where some of the code in the original stylegan2 repo doesn't work with config-b through f. Open up: `dnnlib/tflib/custom_ops.py` and change line 127 to:
    ```
    compile_opts += ' --compiler-options \'-fPIC -D_GLIBCXX_USE_CXX11_ABI=1 \''
    ```
    (essentially, you're just changing the ABI=0 to `ABI=1` at the end of the line)
16. Test to make sure it works by generating some images. You can generate images based on any of the pretrained models from the official NVLabs Google Drive, but this StyleGAN2 folder already has downloaded pretrained models (**FFHQ 1024x1024 config-f** and **FFHQ 512x512 config-f**)
    ```
    python run_generator.py generate-images --network=pretrained_models/your_pickle_file.pkl --seeds=6600-6625 --truncation-psi=0.5
    ```