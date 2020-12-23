---
title: "How to Create a Legal Windows XP Virtual Machine in 2020"
date: 2020-12-22
Description: "Create a Legal Windows XP Virtual Machine in 2020"
categories:
  - blog
tags:
  - windowsxp
  - windowsxp
  - exploit development
  - vulnserver
  - infosec
---

While there is no reason to be using Windows XP in 2020 and beyond, it is still a great learning platform for older x86 exploit development concepts. Specifically, Offensive Securty's [Cracking the Perimeter][ctp] course focuses heavily on Windows XP and Windows Server 2003. Here is a brief walkthrough for creating an XP virtual machine without pirating sketchy software.

The BLUF: Extract the Windows XP virtual hard disk from the XP mode package, which can be downloaded directly from Microsoft. Import the VHD as a new VM. Fix stuff. Profit.


### STEP 0: Download the XP mode package from [Microsoft][xp-mode-download]
![Download00](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-2_00_download_00.png)
![Download01](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-22_00_download_01.png)


### STEP 1: Extract the necessary files from the XP Mode package.

+ Using 7-Zip, right click on the file > open archive > select `cab`
![Extract00](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-22_02_extract_files.png)

+ Within 7-Zip, there will be a `sources` directory. This contains the files of interest. Double-click it
![Extract01](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-22_03_extract_files.png)

+ Within `sources`, there will be another file called `xpm`. Double-click it to extract the contents.
![Extract02](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-22_04_extract_files.png)

+ Within `xpm`, there will be several files. Extract these files to some directory.
![Extract03](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-22_05_extract_files.png)

+ The file of interest is VirtualXPVHD. Rename this file to `VirtualXP.vhd`. This is the virtual hard disk (VHD) file containing Windows XP.
![Extract04](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-22_06_extract_files.png)

### STEP 2: Import the VHD to a new Virtual Machine.

This step is trivial, so I won't go into too much detail here. I am using VMware Fusion on MacOS, but the process is similar for Virtual Box and other VMware platforms.

Select Import and navigate to the VHD file that we just extracted.
![Import00](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-22_07_import.png)

### STEP 3: OS and VMware Tools Install.

Continue through the steps until the VM is ready then power it on. Go through the Windows XP setup and VMware tools installation. The cursor won't be working at this stage. You will have to use `tab` and `arrow` keys to navigate the installation. Once VMware tools installs, the display may be black. Reboot the VM and you should be able to log into XP as normal.

### STEP 4: Fix Stuff.

In my experience, the cursor was broken. Clicking seemed to work, but it was as if the cursor was stuck in the top left corner of the display, thus making it impossible to use. In order to fix this issue, we must uninstall `Virtual PC Integration Components`.

First, open a cmd shell by pressing `win + r` and typing `cmd` then selecting `run`.
![run00](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-22_08_run_cmd.png)

Next, in the cmd shell, run `wmic`.
![wmic00](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-22_09_wmic.png)

Within WMIC, execute `product get name` to list installed programs. Our target is `Virtual PC Integration Components`.

![wmic01](https://github.com/subat0mik/personal_site/raw/master/_posts/images/2020-12-22_10_wmic_list.png)

In order to uninstall this, execute `product where name="Virtual PC Integration Components" call uninstall /nointeractive`. Upon completion, a reboot should be triggered. After rebooting, the cursor should be fully functional again.



[ctp]: https://web.archive.org/web/20200805102103/https://www.offensive-security.com/ctp-osce/
[xp-mode-download]: https://www.microsoft.com/en-us/download/details.aspx?id=8002
