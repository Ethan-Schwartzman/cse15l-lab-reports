# cse15l-lab-reports
### Commands
- ##### cd
	- *No arguments*
		```bash
		[user@sahara ~/lecture1/messages]$ cd
		[user@sahara ~]$
		```
		The working directory was changed to the home directory. The output is not an error.
	- *Path to directory*
		```bash
		[user@sahara ~]$ cd lecture1/messages
		[user@sahara ~/lecture1/messages]$
		```
		The working directory was changed to the specified path. The output is not an error. 
	- *Path to file*
		```bash
		[user@sahara ~/lecture1/messages]$ cd en-us.txt
		bash: cd: en-us.txt: Not a directory
		```
		The output is an error because cd changes the directory and a file is not a valid directory.
- ##### ls
	- *No arguments*
		```bash
		[user@sahara ~/lecture1/messages]$ ls
		en-us.txt  es-mx.txt  zh-cn.txt
		```
		All the files in the working directory are listed. The output is not an error.
	- *Path to directory*
		```bash
		[user@sahara ~]$ ls lecture1/messages
		en-us.txt  es-mx.txt  zh-cn.txt
		```
		All the files in the directory specified by the path are listed. The output is not an error.
	- *Path to file*
		```bash
		[user@sahara ~]$ ls lecture1/messages/en-us.txt
		lecture1/messages/en-us.txt
		```
		The output is the path to the file. The output is not an error.
- ##### cat
	- *No arguments*
		```bash
		[user@sahara ~]$ cat
		^C
		[user@sahara ~]$ 
		```
		There is no output and the command line is unresponsive until it is interrupted. While there is no error message, the output is undesirable.
	- *Path to directory*
		```bash
		[user@sahara ~]$ cat lecture1/messages
		cat: lecture1/messages: Is a directory
		```
		The console affirms that the path is a directory. The output is not an error.
	- *Path to file*
		```bash
		[user@sahara ~]$ cat lecture1/messages/en-us.txt
		Hello World!
		```
		The output is the contents of the specified file. The output is not an error.