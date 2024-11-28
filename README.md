java c
FIT2014
Assignment 2
Regular Languages, Context-Free Languages, Lexical analysis, Parsing, Turing machines and Quantum Computation
DUE: 11:55pm, Friday 4 October 2024
In these exercises, you will
• implement a lexical analyser using lex (Problem 3);
• implement parsers using lex and yacc (Problems 1–6);
• program a Turing machine (Problem 7);
• learn about some aspects of quantum circuits and quantum registers, by applying our methods to calculations with them (Problems 2–6);
• practise your skills relating to the Pumping Lemmas and Context-Free Languages (Problem 8).
Solutions to Problem 7 must be implemented in the simulator Tuatara. We are providing version 2.1 on Moodle under week 8; the file name is tuatara-monash-2.1.jar. You must use exactly this version, not some other version downloaded from the internet. Do not unpack this file. It must be run directly using the Java runtime.
How to manage this assignment
• You should start working on this assignment now and spread the work over the time until it is due. Do as much as possible before week 10.
• Don’t be deterred by the length of this document! Much of it is an extended tutorial to get you started with lex and yacc (pp. 7–11) and documentation for functions, written in C, that are provided for you to use (pp. 12–17); some matrices and sample outputs also take up a fair bit of space. There is an optional three-page introduction to some of the basics of quantum computing (pp. 17–19), which is there for those who are interested in knowing more but is not required for this assignment. Although lex and yacc are new to you, the questions about them only require you to modify some existing input files for them rather than write your own input files from scratch.
• The tasks required for the assignment are on pp. 3–6.
For Problems 1–5, read the background material on pp. 7–11.
For Problems 2–6, also read the background material on pp. 12–17.
For Problem 7, read the background material on p. 21.
For Problem 8, read the background material on p. 22.
Instructions
Instructions are mostly as for Assignment 1, except that some of the filenames have changed, and now each Problem has its own directory. To begin working on the assignment, download the workbench asgn2.zip from Moodle. Create a new Ed Workspace and upload this file, letting Ed automatically extract it. Edit the student-id file to contain your name and student ID. Refer to Lab 0 for a reminder on how to do these tasks.
Open a terminal and change into the directory asgn2. You will find four other files already in the directory: plus-times-power.l, plus-times-power.y, quant.h and prob6.awk. You will not modify these files directly; you will make copies of the first two and modify the copies, while quant.h and prob6.awk must remain unaltered (although it’s ok to have copies of them in other directories).
You need to construct new lex files, using plus-times-power.l as a starting point, for Problems 1, 3, 4  5, and you’ll need to construct a new yacc file from plus-times-power.y for Problems 4  5. Your submission must include:
• the file student-id, edited to contain your name and student ID
• a lex file prob1.l which should be obtained by modifying a copy of plus-times-power.l
• a PDF file prob2.pdf which should contain your solution to Problem 2 (with your name and student ID at the start)
• a lex file prob3.l which should also be obtained by modifying a copy of plus-times-power.l
• a lex file prob4.l which should be obtained by modifying a copy of prob3.l
• a yacc file prob4.y which should be obtained by modifying a copy of plus-times-power.y
• a lex file prob5.l which should be obtained by modifying a copy of prob4.l
• a yacc file prob5.y which should be obtained by modifying a copy of prob4.y
• a text file prob6.txt which should contain ten lines, being your solution to Problem 6
• a Tuatara Turing machine file prob7.tm
• a PDF file prob8.pdf which should contain your solution to Problem 8 (with your name and student ID at the start).
The original directory structure and file locations must be preserved. For each problem, the files you are submitting must be in the corresponding subdirectory, i.e. problemx for Problem x. Each of these problem subdirectories contains empty files with the required filenames. These must each be replaced by the files you write, as described above. Before submission, check that each of these empty files is, indeed, replaced by your own file.
To submit your work, download the Ed workspace as a zip file by clicking on “Download All” in the file manager panel. The “Download All” option preserves the directory structure of the zip file, which is required to aid the marking process. You must submit this zip file to Moodle by the deadline given above.
Assignment tasks
First, read about “Lex, Yacc and the PLUS-TIMES-POWER language” on pp. 7–11.
Problem 1. [2 marks]
Construct prob1.l, as described on pp. 9–11, so that it can be used with plus-times-power.y to build a parser for PLUS-TIMES-POWER.
Now refer to the document “Quantum circuits, registers and the language QUANT”, pages 12–17. In fact, for Problem 2, you can focus just on pages 15–17 and the language QCIRC.
Problem 2. [3 marks]
Write a Context-Free Grammar for the language QCIRC over the eleven-symbol alphabet {I, H, X, Y, Z, CNOT, TOF, *, ⊗, (, ) }. It can be typed or hand-written, but must be in PDF format and saved as a file prob2.pdf.pdf.
Now we use some very basic regular expressions (in the lex file, prob3.l) and a CFG (in the yacc file, prob4.y) to construct a lexical analyser (Problem 3) and a parser (Problem 4) for QCIRC.
Problem 3. [3 marks]
Using the file provided for PLUS-TIMES-POWER as a starting point, construct a lex file, prob3.l, and use it to build a lexical analyser for QCIRC.
You’ll need to introduce simple regexps for the various tokens, among other things.
Sample output:
$ ./a.out
CNOT* ( H (x)I代 写FIT2014 Assignment 2Java
代做程序编程语言)
Token: CNOT; Lexeme: CNOT
Token and Lexeme: *
Token and Lexeme: (
Token: H; Lexeme: H
Token: KRONECKERPROD; Lexeme: (x)
Token: I; Lexeme: I
Token and Lexeme: )
Token and Lexeme: 
Control-D
Problem 4. [6 marks]
Make a copy of prob3.l, call it prob4.l, then modify it so that it can be used with yacc. Then construct a yacc file prob4.y from plus-times-power.y. Then use these lex and yacc files to build a parser for QCIRC that can correctly evaluate any expression in that language.
Note that you do not have to program any of the quantum expression functions yourself. They have already been written: see the Programs section of the yacc file. The actions in your yacc file will need to call these functions, and you can do that by using the function call for pow(. . . ) in plus-times-power.y as a template.
The core of your task is to write the grammar rules in the Rules section, in yacc format, with associated actions, using the examples in plus-times-power.y as a guide. You also need to do some modifications in the Declarations section; see page 10 and further details below.
When entering your grammar into the Rules section of prob4.y, it is best to leave the existing rules for the nonterminal start unchanged, as this has some extra stuff designed to allow you to enter a series of separate expressions on separate lines. So, take the Start symbol from your grammar in Problem 2 and represent it by the nonterminal line instead of by start.
The specific modifications you need to do in the Declarations section should be:
• You need a new %token declaration for the tokens I, H, X, Y, Z, CNOT, TOF, and KRONECKERPROD. These have the same structure as the line for the NUMBER token, except that “num” is replaced by “str” (since each of the above tokens represents a string, being names of matrices, registers or operations, whereas NUMBER represents a number).
• You should include each of our two matrix operations, * (multiplication) and KRONECKERPROD (the Kronecker product, ⊗), in a %left or %right statement. Such a statement specifies when an operation is left- or right-associative, i.e., whether you do multiple consecutive operations left-to-right or right-to-left. Mathematically, for * and ⊗, it doesn’t matter. So, for these, you can use either %left or %right. But you should do one of them, because it helps the parser determine an order in which to do the operations and removes some ambiguity. For operations whose %left or %right statements are on different lines, the operations with higher precedence are those with higher line numbers (i.e., later in the file). Ordinary matrix multiplication should have higher precedence than Kronecker product.
• For nonterminal symbols, you can include a %type line that declares its type, i.e., the type of value that is returned when an expression generated from this nonterminal is evaluated. E.g.,
%type  start here
Here, “qmx” is the type name we are using for quantum matrices. The various type names can be seen in the %union statement a little earlier in the file. But you do not need to know how that works in order to do this task.
• You should still use start as your Start symbol. If you use another name instead, you will need to modify the %start line too.
Sample output:
$ ./a.out
CNOT* ( H (x)I)
4x4 matrix:
0.7071 0.0000 0.7071 0.0000
0.0000 0.7071 0.0000 0.7071
0.0000 0.7071 0.0000 -0.7071
0.7071 0.0000 -0.7071 0.0000
Control-D
Problem 5. [5 marks]
Make a copy of prob4.l, call it prob5.l. Also, make a copy of prob4.y, call it prob5.y. Then modify these lex and yacc files further to build a parser for QUANT that can correctly evaluate any expression in that language.
Again, the core of your task is to write the grammar rules in the Rules section, in yacc format with associated actions, in prob5.y. You will also need new tokens KET0 and KET1, which represent k0 and k1 respectively. These tokens need appropriate rules in prob5.l and declarations in prob5.y, and you will use them in the grammar.
Problem 6. [5 marks]
In the problem6 directory you will find a file, prob6.awk. This is an awk program for converting your student ID number to a particular quantum register expression.
Do this conversion by running this awk program using awk -f prob6.awk, then (when it waits for your input) entering your student ID number. You will see the quantum register expression appear as output.
(a) Copy this quantum register expression (which will be a member of QUANT) and enter it as the first line in the text file prob6.txt.
(b) Run your parser on your expression from (a), and report the result of evaluating it by appending the output to the file prob6.txt.
The answer to (a) should be the first line of your file prob6.txt. Your answer to (b) should occupy the remaining nine lines. The file should therefore have ten lines altogether. You can use wc prob6.txt to verify this.
For example, if your ID is 12345678, then your ten-line file prob6.txt should look like this:
(X (x) Y (x) Z) * (Y (x) CNOT) * (X (x) Y (x) Z) * (k0 (x) k0 (x) k0)
3-qubit register, 8-element vector:
0.0000
0.0000
0.0000
0.0000
0.0000
0.0000+1.0000i
0.0000
0.0000
Turing machines
Now refer to the description of the number choice function on page 21.
Problem 7. [7 marks]
Build, in Tuatara v2.1, a Turing machine that computes the number choice function, and save the Turing machine as a file prob7.tm.
Context-Free Languages
Now refer to the description of Universal Models on page 22.
Problem 8. [9 marks]
(a) Prove, using the Pumping lemma for Regular Languages, that there is no Universal Regular Expression.
(b) Prove, using the Pumping lemma for Context-Free Languages, that there is no Universal Context-Free Grammar.
Your submission can be typed or hand-written, but it must be in PDF format and saved as a single file prob8.pdf.





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
