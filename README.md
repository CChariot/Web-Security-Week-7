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

