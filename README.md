# macro_competition

to do (for feature extarction)

- remove all the comments in the scripts
- eliminate the special characters in the scripts.
For example, multiple consecutive spaces in the scripts that are replaced with one, tabs and new-lines will be deleted directly.
After completing this step, the script will be converted to one line text, that each word is separated by a space and has no punctuation.
- filter if there are URL/IP in the code - malicious scripts often download malware or malicious code from external websites to further attack the computer. real malicious behavior is hidden in the downloaded file.
- filter if there are Malicious function using in the code
- filter Special variable names - the variable in malicious scripts is always named ”cmd”, ”Shell”, ”c”, etc. This is because hackers like to use scripts to call command lines in hacking.

- Note about length of the code: malicious scripts tend to use longer strings because the truly malicious code snippets are encoded into strings, then these malicious scripts can be obfuscated easily. the number of strings in the malicious script is longer than the benign samples.
- Therefore, we neet to count the number of strings, the maximum length of the strings, and the average length of the strings as three features for each
script.

References (read and keep those that help us, take ideas, delete irrelevent):
1. https://intezer.com/blog/malware-analysis/analyze-malicious-microsoft-office-files/
2. https://www.blumira.com/glossary/malicious-macro/
3. https://perception-point.io/blog/malicious-office-macros-detecting-similarity-in-the-wild-2/
4. https://www.logpoint.com/en/blog/detecting-malicious-macros-is-a-vital-tool-in-the-fight-against-malware/
5. https://appriver.com/blog/201606malicious-macros-and-ole-malware
6. https://www.techtarget.com/searchsecurity/definition/macro-virus
7. https://www.sentinelone.com/cybersecurity-101/what-is-a-macro-virus/
8. https://support.microsoft.com/en-us/office/protect-yourself-from-macro-viruses-a3f3576a-bfef-4d25-84dc-70d18bde5903
