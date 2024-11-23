# Scenario
You are a level one security operations center (SOC) analyst at a financial services company. You have received an alert about a suspicious file being downloaded on an employee's computer.

You investigate this alert and discover that the employee received an email containing an attachment. The attachment was a password-protected spreadsheet file. The spreadsheet's password was provided in the email. The employee downloaded the file, then entered the password to open the file. When the employee opened the file, a malicious payload was then executed on their computer.

You retrieve the malicious file and create a SHA256 hash of the file. Now that you have the file hash, you will use VirusTotal to uncover additional IoCs that are associated with the file.

## 1. Details of the alert
- SHA256 file hash: 54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b
- Here is a timeline of the events leading up to this alert:
  - 1:11 p.m.: An employee receives an email containing a file attachment.
  - 1:13 p.m.: The employee successfully downloads and opens the file.
  - 1:15 p.m.: Multiple unauthorized executable files are created on the employee's computer.
  - 1:20 p.m.: An intrusion detection system detects the executable files and sends out an alert to the SOC.

  ## 2. VirusTotal scan
  - Detection:<br>
  ![VirusTotal_Detection](https://github.com/Cr1msonPho3nix/Asset_Management/blob/main/img/Decrypt%20an%20encrypted%20message/2.decrypting_caesar.PNG)<br><br>
- Details
  ![VirusTotal_Details](https://github.com/Cr1msonPho3nix/Asset_Management/blob/main/img/Decrypt%20an%20encrypted%20message/2.decrypting_caesar.PNG)<br><br>
  - Behaviour
  ![VirusTotal_Behaviour](https://github.com/Cr1msonPho3nix/Asset_Management/blob/main/img/Decrypt%20an%20encrypted%20message/2.decrypting_caesar.PNG)<br><br>
  - Associations
  ![VirusTotal_Associations](https://github.com/Cr1msonPho3nix/Asset_Management/blob/main/img/Decrypt%20an%20encrypted%20message/2.decrypting_caesar.PNG)<br><br>

## 3. Determine whether the file is malicious
- At the "Detection" tab most of the security vendor's analysis tags this program as a trojan.flagpro, something that has some importance later.
- As an executable file it should be considered dangerous due to the implications of execute unknown orders when you click on it.
- Most of sandbox reports flags the file as Malware.
- The "Behaviour" tab gives us some real important information, cause this "flagpro" seems to be a malware used by a blackhat group attacking Japanese companies called "BlackTech".
- With all this information we can assume the file is a proper malware, specifically a trojan.