# Project 7 - WordPress Pentesting

Time spent: 5 hours spent in total

> Objective: Find, analyze, recreate, and document **three vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. (Required) Brute-Force User Enumeration
  - [X] Summary: It is possible to use enumeration to brute-force WordPress's username and password storage
    - Vulnerability types: User Enumeration
    - Tested in version: 4.2
    - Fixed in version: 4.5
  - [X] GIF Walkthrough: https://i.imgur.com/XtpaPpG.gifv
  - [X] Steps to recreate: 
	1. For this attack, a copy of the list of most common passwords rockyou-75.txt is needed - it can be downloaded from a number of places
	2. Go to the directory in which rockyou-75.txt is stored
	3. Call wpscan --enumerate u --url wpdistillery.local - this will present you with a list of usernames on the account
	4. Once you have the table of usernames, type in wpscan --url wpdistillery.local --wordlist '/root/Desktop/rockyou-75.txt' (substitute your directory for Desktop), and begin the attack
	5. The attack may take a while, but ultimately it will come back with a table of usernames and passwords 
  - [X] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
1. (Required) Authenticated Cross-Site Scripting
  - [X] Summary: The use of Javascript in comments can facilitate a XSS attack
    - Vulnerability types: XSS vulnerability
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - [X] GIF Walkthrough: https://i.imgur.com/kH7rEe8.gifv
  - [X] Steps to recreate: 
	1. Go to wpdistillery.local (wpdistillery.dev redirects there).
	2. Proceed to the comment box, and type in <a title='x onmouseover=alert(unescape(/hello%20world/.source))
	
	style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64 kb]..AAA'></a> (64 kbs of 'A's are necessary in order to put the length of the comment over the acceptable limit)
	3. The length of the comment will cause it to be truncated when inserted, which leads to malformed HTML displayed which is vulnerable to JavaScript insertion
	4. Submit the comment - upon viewing the page, the text box will appear with the malicious script (in this case, simply a "hello world" message)
  - [X] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
1. (Required) Cross-Site Scripting Vulnerability
  - [X] Summary: A vulnerability exists in WordPress 4.2 that allows for malicious Javascript to be used to facilitate an XSS attack
    - Vulnerability types: XSS vulnerability
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - [X] GIF Walkthrough: https://i.imgur.com/B3AlqzZ.gifv
  - [X] Steps to recreate: 
	1. Go to wpdistillery.local
	2. Proceed to the comment box on any post, and type in <script>alert('XSS')</script>
	3. Submit the comment - upon viewing the page the popup text box will appear
  - [X] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
 

## Assets

- rockyou-75.txt  (a list of the most commonly used passwords)

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Downloading and installing the necessary tools took an extremely long time and was very difficult. The vulnerabilities themselves were not overly difficult, but the setup took up most of my time and energy.

## License

    Copyright [2017] [Kelly Rose]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
