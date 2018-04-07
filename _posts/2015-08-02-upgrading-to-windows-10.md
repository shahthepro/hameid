---
id: 11
title: Upgrading to Windows 10
date: 2015-08-02T06:30:00+00:00
author: Shah
layout: post
guid: http://hameid.net/2015/08/02/upgrading-to-windows-10/
permalink: /upgrading-to-windows-10/
categories:
  - Uncategorized
tags:
  - Microsoft
  - Windows
  - Windows 10
---
If you happen to have reserved your copy of [Windows 10](/tag/windows-10/) and haven’t received any notification of the update, You might have to wait a few days or even weeks before upgrading to Windows 10.

If you don’t have the patience to wait for the update to show up, Here’s how to upgrade to Windows 10 manually.

  1. Download the ESD image for Windows 10 from [here](https://www.reddit.com/r/Windows10/comments/3ee1gx/windows_10_10240_esd_download_here/). Make sure that the edition and language matches your current Windows 7 or Windows 8.1 installation.

  2. Download ESD Decrypter v6.7 from [this link](http://1drv.ms/1VRZDo4) and then extract it to the same directory where the downloaded the ESD image exists.

  3. Now, right click on **“decrypt.cmd”** and select **“Run as administrator“**.
    
    ![Upgrading to Windows 10 - Run as administrator](/content/images/2015/08/upgrade-to-windows-10-1.png)

  4. On the console window that appears, Press 1 to decrypt the ESD image file into an ISO image file.
    
    ![Upgrading to Windows 10 - ESD Decrypter](/content/images/2015/08/upgrade-to-windows-10-2.png)

  5. ESD Decrypter will now start processing. It should take a few minutes to decrypt the ESD image.
    
    ![Upgrading to Windows 10 - ESD Decrypter](/content/images/2015/08/upgrade-to-windows-10-3.png)

  6. After ESD Decrypter has finished processing, You should see an ISO image in the same folder. Now, Mount the ISO image and run the **“setup.exe”** in that mounted drive.

  7. That’s it. Now, you should see the **“Windows 10 Setup”** wizard. Go ahead and update to Windows 10.
    
    ![Upgrading to Windows 10 - Setup](/content/images/2015/08/upgrade-to-windows-10-4.png)

In case you want a clean install, do a clean install of Windows 7 or Windows 8.1 and then upgrade to Windows 10. Otherwise, your Windows 10 won’t be activated with your old key.