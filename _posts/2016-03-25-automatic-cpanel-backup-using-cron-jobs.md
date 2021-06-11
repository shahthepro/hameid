---
id: 20
title: Automatic cPanel Backup Using Cron Jobs
date: 2016-03-25T15:10:00+00:00
author: Shah
layout: post
guid: http://hameid.net/2016/03/25/automatic-cpanel-backup-using-cron-jobs/
permalink: /automatic-cpanel-backup-using-cron-jobs/
categories:
  - Uncategorized
tags:
  - Backup
  - cPanel
  - Cron Job
  - MySQL
  - SQL
  - UNIX
published: false
---
Being a website owner, It is really important to have a recent backup of your website. [cPanel](https://en.wikipedia.org/wiki/CPanel), the most popular web hosting control panel, provides a powerful _Full Backup_ feature. Generating a full website backup with cPanel’s _Full Backup_ can be simple but not completely automated.

If you’re someone who adds new content to your website regularly, You probably don’t want to login into your cPanel each time just to take a backup. Instead you can set up _Cron jobs_ on your cPanel account to take a backup of all your file and databases.

> Cron jobs allow you to automate certain commands or scripts in your cPanel account. You can set a command or script to run at a specific time at a specified interval.

Sounds cool, right? Let me show you how to set up _Cron jobs_ to automatically take backup of your data. Basically, We will set up two _Cron jobs_. One for archiving the files and the other one for generating a backup of the databases.

* * *

### Setting Up Cron Job To Backup The Databases {#settingupcronjobtobackupthedatabases}

  1. Login to your cPanel account. In the Advanced section, click _Cron jobs_.

  2. Under “Add New Cron Job”, Set the Common Settings to Once Per Day.

  3. Now, to backup all the databases in your cPanel account, [`mysqldump`](https://dev.mysql.com/doc/refman/5.5/en/mysqldump.html) command can be used. Copy-Paste the following command in the Command field.  
  ```mysqldump --opt -Q -u YOUR_CPANEL_USERNAME -p'YOUR_CPANEL_PASSWORD' --all-databases > /home/YOUR_CPANEL_USERNAME/backup/databases.sql```  
  Make sure to replace _YOUR\_CPANEL\_USERNAME_ and _YOUR\_CPANEL\_PASSWORD_ with your actual cPanel credentials.

  4. Click on **Add New Cron Job** button to create the Cron job.

* * *
  

### Setting Up Cron Job To Backup The Files {#settingupcronjobtobackupthefiles}

  1. Login to your cPanel account. In the Advanced section, click _Cron jobs_.

  2. Under “Add New Cron Job”, Set the Common Settings to Once Per Day.

  3. The [`tar`](http://linuxcommand.org/man_pages/tar1.html) UNIX command can be used to archive all the files in your cPanel account. Copy-Paste the following command in the Command field.  
  ```tar -cvpzf /home/YOUR_CPANEL_USERNAME/backup/files.tar.gz /home/YOUR_CPANEL_USERNAME/public_html```  
  Make sure to replace _YOUR\_CPANEL\_USERNAME_ and _YOUR\_CPANEL\_PASSWORD_ with your actual cPanel credentials.

  4. Click on **Add New Cron Job** button to create the Cron job.

Once you have set up both the _Cron jobs_, A backup of your databases and files will be automatically generated every day. You can, of course, change the time interval for the _Cron jobs_. The backup files will be available for you to download from the “backup” directory in your cPanel account’s root directory.