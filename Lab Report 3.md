### Part 1 - Bugs

Choose one of the bugs from lab 4.
- I have chosen the bug in the append method from LinkedListExample.java.

Provide:
- A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)
```java
@Test
public void AppendTest() {
    LinkedList ll = new LinkedList();
    ll.append(3);
    ll.append(4);
    ll.append(5);
    assertEquals("3 4 5 ", ll.toString());
}
```
- An input that _doesn’t_ induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)
```java
@Test
public void AppendOnce() {
    LinkedList ll = new LinkedList();
    ll.append(3);
    assertEquals("3 ", ll.toString());
}
```
- The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)
![[lab-report-3-1.png]]
![[lab-report-3-2.png]]
- The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)
	- Before
```java
public void append(int value) {
    if(this.root == null) {
        this.root = new Node(value, null);
        return;
    }
        
    // If it's just one element, add if after that one
    Node n = this.root;
    if(n.next == null) {
        n.next = new Node(value, null);
        return;
    }
        
    // Otherwise, loop until the end and add at the end with a null
    while(n.next != null) {
        n = n.next;
        n.next = new Node(value, null);
    }
}
```
	-  After
```java
public void append(int value) {
    if(this.root == null) {
        this.root = new Node(value, null);
        return;
    }
        
    // If it's just one element, add if after that one
    Node n = this.root;
    if(n.next == null) {
        n.next = new Node(value, null);
        return;
    }
        
    // Otherwise, loop until the end and add at the end with a null
    while(n.next != null) {
        n = n.next;
    }
    n.next = new Node(value, null); // This line was moved outside the loop
}
```

Briefly describe why the fix addresses the issue.
- The fix was to move a line of code from inside the while loop to the outside. This is because the loop continues as long as the node has a null next, but the buggy append method always adds a node with a null next before the loop ends so it will continue infinitely (in reality, until there is a memory error). By moving the line outside the loop, the desired outcome of appending the node still happens, but the loop has already terminated so it does not see the new null next and loop again.

### Part 2 - Researching Commands

Consider the commands `less`, `find`, and `grep`. Choose _one_ of them. Online, find 4 interesting command-line options or alternate ways to use the command you chose. To find information about the commands, a simple Web search like “find command-line options” will probably give decent results. There is also a built-in command on many systems called `man` (short for “manual”) that displays information about commands; you can use `man grep`, for example, to see a long listing of information about how `grep` works. Also consider asking ChatGPT!

For example, we saw the `-name` option for `find` in class. For each of those options, give 2 examples of using it on files and directories from `./technical`. Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.

That makes 8 total examples, all focused on a single command. There should be two examples each for four different command-line options. Many commands like these have pretty sophisticated behavior possible – it can take years to be exposed to and learn all of the possible tricks and inner workings.

Along with each option/mode you show, **cite your source** for how you found out about it as a URL or a description of where you found it. See the [syllabus](https://ucsd-cse15l-f23.github.io/syllabus/#skill-demonstrations-and-academic-integrity) on Academic Integrity and how to cite sources like ChatGPT for this class.

Command: `grep`
- - c option [source](https://en.wikibooks.org/wiki/Grep)
	- Example 1
		```bash
		ethan@Ethans-Laptop MINGW64 ~/Documents/VSCode/Classes/CSE15L/Lab5/docsearch (main)
		$ grep -c "nucleotides" ./technical/biomed/1471-2164-3-33.txt
		4
		```
		- The -c indicates that only the count should be the output. Instead of listing the contents of all the lines with the term "nucleotides", it lists the number of lines with the term "nucleotides".
	- Example 2
	```bash
	ethan@Ethans-Laptop MINGW64 ~/Documents/VSCode/Classes/CSE15L/Lab5/docsearch (main)
	$ grep -c "monopoly" ./technical/government/Post_Rate_Comm/*.txt
	./technical/government/Post_Rate_Comm/Cohenetal_comparison.txt:7
	./technical/government/Post_Rate_Comm/Cohenetal_Cost_Function.txt:0
	./technical/government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt:16
	./technical/government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt:1
	./technical/government/Post_Rate_Comm/Cohenetal_RuralDelivery.txt:1
	./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:26
	./technical/government/Post_Rate_Comm/Gleiman_EMASpeech.txt:0
	./technical/government/Post_Rate_Comm/Gleiman_gca2000.txt:0
	./technical/government/Post_Rate_Comm/Mitchell_6-17-Mit.txt:1
	./technical/government/Post_Rate_Comm/Mitchell_RMVancouver.txt:7
	./technical/government/Post_Rate_Comm/Mitchell_spyros-first-class.txt:2
	./technical/government/Post_Rate_Comm/Redacted_Study.txt:0
	./technical/government/Post_Rate_Comm/ReportToCongress2002WEB.txt:0
	./technical/government/Post_Rate_Comm/WolakSpeech_usps.txt:0
	```
	- The -c is very useful for larger amounts of files where printing so many lines directly to the console would quickly flood it with text. Giving only the count makes it much more manageable to read and interpret. 
-  -v option [source](https://en.wikibooks.org/wiki/Grep)
	- Example 1
		```bash
		ethan@Ethans-Laptop MINGW64 ~/Documents/VSCode/Classes/CSE15L/Lab5/docsearch (main)
$ grep -v "nucleotides" ./technical/biomed/1471-2164-3-33.txt
        Background
        Organic phosphate compounds are the central metabolites
        of all biological systems [ 1 2 ] . Some are the basic
        building blocks of nucleic acids, some like ATP and GTP,
        are additionally, cellular energy stores, others like cAMP
        or cGMP are messengers in signal transduction, and, yet
        others, such as FAD, NAD, thiamine phosphates and pyridoxal
        phosphate are cofactors for a range of enzymes [ 1 2 ] .
        Protein domains belonging to a relatively small set of
        ...
		```
		- Instead of only showing the lines containing "nucleotides", it shows all the lines that do not contain nucleotides.
	- Example 2
		```bash
		ethan@Ethans-Laptop MINGW64 ~/Documents/VSCode/Classes/CSE15L/Lab5/docsearch (main)
$ grep -v "a" ./technical/biomed/1471-2164-3-33.txt

        nucleotide binding or hydrolyzing proteins [ 6 7 8 9 ] .
        ] .

          orthologs from
          E. coli YgiF. At convergence,
          E. coli YgiF protein (residues
          Mesorhizobium loti Mll4592 with
          (49D11.13 from
          recovered the most of the members detected in the
          CYTH ( 
          which it is present.

          form.
          exception of
          (CHAD:
          c onserved
          h istidine
          nucleotide-binding site in these enzymes (Fig. 3).
          In terms of conserved gene neighborhoods,
          neighborhood of genes encoding solo CHADs (Fig. 3).

	    ...
		```
		- The -v option seems useful for filtering out certain lines from text files. It could be used to quickly take out certain elements from a dataset or json file.
-  -o option [source](https://en.wikibooks.org/wiki/Grep)
	- Example 1
		```bash
		$ grep -o "nucleotides" ./technical/biomed/1471-2164-3-33.txt
		nucleotides
		nucleotides
		nucleotides
		nucleotides
		```
		- The -o option keeps only the matched part of the line. Since there were four lines containing "nucleotides" it printed "nucleotides" four times.
	- Example 2
		```bash	
		ethan@Ethans-Laptop MINGW64 ~/Documents/VSCode/Classes/CSE15L/Lab5/docsearch (main)
		$ grep -o "monopolies" ./technical/government/Post_Rate_Comm/*.txt
		./technical/government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt:monopolies
		./technical/government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt:monopolies
		./technical/government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt:monopolies
		./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:monopolies
		./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:monopolies
		./technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:monopolies
		```
		- I'm not exactly sure why the -o option would be useful but I would speculate that it is more relevant when grep is run with a variable as the search term. Perhaps if it was in a bash script and the user didn't know what was being searched for then seeing what word it matched on might be helpful.
-  -n option [source](https://en.wikibooks.org/wiki/Grep)
	- Example 1
		```bash
		$ grep -n "nucleotides" ./technical/biomed/1471-2164-3-33.txt
		182:          likely to be domains specialized to bind nucleotides and
		218:          two metal ions, with a preference for nucleotides or
		435:          organo-phosphate derivatives including nucleotides.
		464:        catalytic domains that act on nucleotides and
		```
		- The -n option adds a number indicating which line it matched on to each of the lines.
	- Example 2
		```bash
		ethan@Ethans-Laptop MINGW64 ~/Documents/VSCode/Classes/CSE15L/Lab5/docsearch (main)
		$ grep -n "federal" ./technical/government/Post_Rate_Comm/*.txt
		./technical/government/Post_Rate_Comm/Gleiman_EMASpeech.txt:359:federal and state levels. More often than not, those involved have
		./technical/government/Post_Rate_Comm/Gleiman_EMASpeech.txt:382:of the federal records Privacy Act of 1974 and the 1974 school
		./technical/government/Post_Rate_Comm/Gleiman_EMASpeech.txt:385:federal privacy law, governs the collection and use of personal
		./technical/government/Post_Rate_Comm/Gleiman_EMASpeech.txt:386:data by federal agencies and which provides agencies a modicum of
		./technical/government/Post_Rate_Comm/Gleiman_gca2000.txt:525:Overly restrictive privacy legislation at the federal level or,
		./technical/government/Post_Rate_Comm/Gleiman_gca2000.txt:531:conservatives of the benefits of federal preemption and liberals of
		```
		-  This option would be very useful for long files. It would make it easier to look up the section where the match occurred. 