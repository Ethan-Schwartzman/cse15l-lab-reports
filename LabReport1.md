# cse15l-lab-reports
### Commands
- ##### cd
	- *No arguments*
		```bash
		[user@sahara ~/lecture1/messages]$ cd
		[user@sahara ~]$
		```
		The working directory is `/lecture1/messages`. The working directory was changed to the home directory. The output is not an error.
	- *Path to directory*
		```bash
		[user@sahara ~]$ cd lecture1/messages
		[user@sahara ~/lecture1/messages]$
		```
		The working directory is the home directory. The working directory was changed to the specified path `/lecture1/messages`. The output is not an error. 
	- *Path to file*
		```bash
		[user@sahara ~/lecture1/messages]$ cd en-us.txt
		bash: cd: en-us.txt: Not a directory
		```
		The working directory is `/lecture1/messages`. The output is an error because cd changes the directory and a file is not a valid directory.
- ##### ls
	- *No arguments*
		```bash
		[user@sahara ~/lecture1/messages]$ ls
		en-us.txt  es-mx.txt  zh-cn.txt
		```
		The working directory is `/lecture1/messages`. All the files in the working directory are listed. The output is not an error.
	- *Path to directory*
		```bash
		[user@sahara ~]$ ls lecture1/messages
		en-us.txt  es-mx.txt  zh-cn.txt
		```
		The working directory is the home directory. All the files in the directory specified by the path `lecture1/messages` are listed. The output is not an error.
	- *Path to file*
		```bash
		[user@sahara ~]$ ls lecture1/messages/en-us.txt
		lecture1/messages/en-us.txt
		```
		The working directory is the home directory. The output is the path to the file, `lecture1/messages/en-us.txt`. If a different path is used then the output will change to reflect that filepath. The output is not an error.
- ##### cat
	- *No arguments*
		```bash
		[user@sahara ~]$ cat
		hello world
		hello world
		^C
		[user@sahara ~]$
		```
		The working directory is the home directory. Anything typed after this command is repeated back by the command line. In the example above, `hello world` was typed only once, the second occurrence was output by the command line. There is no error but this continues until the command line is interrupted.
	- *Path to directory*
		```bash
		[user@sahara ~]$ cat lecture1/messages
		cat: lecture1/messages: Is a directory
		```
		The working directory is the home directory. The console states that the path `lecture1/messages` is a directory. The output is an error.
	- *Path to file*
		```bash
		[user@sahara ~]$ cat lecture1/messages/en-us.txt
		Hello World!
		```
		The working directory is the home directory. The output is the contents of the specified file. The output is not an error.