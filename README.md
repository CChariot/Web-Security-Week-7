# Web-Security-Week-7 WordPress vs. Kali

Time spent: **3** hours spent in total

> Objective: Find, analyze, recreate, and document **three vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. Unauthenticated Stored Cross-Site Scripting (XSS)
  - Summary: If the comment text is long enough, it will be truncated when inserted in the database. The MySQL TEXT type size limit is 64 kilobytes, so the comment has to be long. 
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - Steps to recreate: comment a post with >64kb plus the following command:
			"&lt;a title='x onmouseover=alert(unescape(/hello%20world/.source)) 	style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64 kb]..AAA' &gt;&lt;/a&gt;"
  - GIF Walkthrough: <img src="https://github.com/sengfung27/Web-Security-Week-7/blob/master/1.gif" width="800">

2. Authenticated Stored Cross-Site Scripting (XSS)
  - Summary: Under default configuration, the attack requires a Contributor or Author level account. The attacker would insert specially formatted HTML containing JavaScript on a WordPress page or post. Some special configurations may allow posting or editing page content for unauthenticated users. 
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.3
  - GIF Walkthrough: <img src="https://github.com/sengfung27/Web-Security-Week-7/blob/master/2.gif" width="800">
  - Steps to recreate: insert a script command and package it as a mp3 file and upload it to wordpress, refresh the page after upload and the script should be triggered.
  - Affected source code:
    - [Link 1](https://github.com/WordPress/WordPress/commit/28f838ca3ee205b6f39cd2bf23eb4e5f52796bd7)
    
3. (Required) Two XSS in Media Upload when file too large
  - Summary: An attacker can inject a malicious script in to the filename which a victim tries to upload leading to XSS inside the administrators control panel. Two different "file to large" cases end up in interpolating the file name and appending it into DOM unsanitized leading to XSS.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.15
  - Steps to recreate: Create a 20MB file called "Dinosaurs secret life\<img src=x onerror=alert(1)\>\.png", and upload to the media manager, refresh the page after upload and the script should be triggered.
  - Affected source code: 
    - [Link 1](https://github.com/WordPress/WordPress/commit/8c7ea71edbbffca5d9766b7bea7c7f3722ffafa6)
  - GIF Walkthrough: <img src="https://github.com/sengfung27/Web-Security-Week-7/blob/master/3.gif" width="800">
