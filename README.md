# macro_competition
## Background
Macros save users time by allowing them to automate a series of commands that can be triggered by different actions. Usually, macros are written in Visual Basic for Applications (VBA), a language developed by Microsoft and supported by all Microsoft Office products. Another way to create a macro is to record it within the Microsoft Office application. Macros are a powerful tool that gives users access and permissions to resources of the local system. Attackers use macros to modify files on the system and to execute the next stage of an attack.

The VBA code in malicious Microsoft Office files is frequently obfuscated, and it may look similar to the image below. Attackers will obfuscate a macro’s code to make it harder and more time-consuming for antiviruses and malware analysts to understand what the code is doing. Attackers use several techniques including:

- Encrypting strings and API calls (usually using Base64)
- Adding random characters to obfuscate strings and API functions
- Mangling the names of functions and variables
- Using shellcode to execute malicious functions
​​- Dynamically defining functions
- VBA stomping

After deobfuscating the code, you will have a better understanding of what the attacker is trying to achieve. Usually, they **start PowerShell** and **run commands to gather information about the system**, and **download a malicious payload** from a **remote host** to begin the next stage of the attack.

Obfuscated VBA macro shown in olevba output:
- ![image](https://github.com/TaliaSeada/macro_competition/assets/93203695/a0568fe4-59a2-46f2-b353-bd34199a3d90)


## Feature extarction Process

- **Done:** remove all the comments in the scripts and eliminate the special characters in the scripts
For example, multiple consecutive spaces in the scripts that are replaced with one, tabs and new-lines will be deleted directly.
After completing this step, the script will be converted to one line text, that each word is separated by a space and has no punctuation.

- **Done:** filter if there are URL/IP in the code - malicious scripts often download malware or malicious code from external websites to further attack the computer. real malicious behavior is hidden in the downloaded file.

- **Not a good filter:** filter if there are Malicious function using in the code

- **We chose not to use this filter:** filter Special variable names - the variable in malicious scripts is always named ”cmd”, ”Shell”, ”c”, etc. This is because hackers like to use scripts to call command lines in hacking.

- filter commands of execution - https://attack.mitre.org/datasources/DS0017/#Command%20Execution

- filter commands of file creation - https://attack.mitre.org/datasources/DS0022/#File%20Creation

- filter commands of file modification- https://attack.mitre.org/datasources/DS0022/#File%20Modification

- filter commands of Process Creation - https://attack.mitre.org/datasources/DS0009/#Process%20Creation

- **Pass for now:** filter commands of Windows Registry Key Creation - https://attack.mitre.org/datasources/DS0024/#Windows%20Registry%20Key%20Creation

- **Pass for now:** filter commands of Windows Registry Key Modification - https://attack.mitre.org/datasources/DS0024/#Windows%20Registry%20Key%20Modification

- **Done:** Note about length of the code: malicious scripts tend to use longer strings because the truly malicious code snippets are encoded into strings, then these malicious scripts can be obfuscated easily. the number of strings in the malicious script is longer than the benign samples. Therefore, we need to count the number of strings, the maximum length of the strings, and the average length of the strings as three features for each
script.

- Trying to reach these directories:
- C:\Windows\system32\drivers\etc\hosts
- C:\Windows\system32\drivers\etc\networks
- C:\Windows\system32\config\SAM
- C:\Windows\system32\config\SECURITY
- C:\Windows\system32\config\SOFTWARE
- C:\Windows\system32\config\SYSTEM
- C:\Windows\system32\config\winevt
- C:\Windows\repair\SAM
- C:\Documents and Settings\All Users\Start Menu\Programs\Startup
- C:\Documents and Settings\User\Start Menu\Programs\Startup
- C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup
- C:\Users\example\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
- C:\Windows\Prefetch
- C:\Windows\appcompat\Programs\Amcache.hve
- C:\Windows\Users*\NTUSER.dat

## References:
1. https://intezer.com/blog/malware-analysis/analyze-malicious-microsoft-office-files/
3. https://perception-point.io/blog/malicious-office-macros-detecting-similarity-in-the-wild-2/
4. https://www.logpoint.com/en/blog/detecting-malicious-macros-is-a-vital-tool-in-the-fight-against-malware/
5. https://appriver.com/blog/201606malicious-macros-and-ole-malware
7. https://www.sentinelone.com/cybersecurity-101/what-is-a-macro-virus/
8. https://medium.com/@sasikumarbibin/windows-common-directories-and-threat-actors-3ddcb3c9fad0
