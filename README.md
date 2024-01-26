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
