## Learning by doing - `awk` command
* Spring 2019, CS35L - Lab 7
* TA: Rishab Ketan Doshi
* Week 2, Lecture 2, April 11

### Details

* Awk is a scripting language used for manipulating data and generating reports.
* The awk command programming language requires no compiling, and allows the user to use variables, numeric functions, string functions, and logical operators.

### Learn by examples

We will learn the awk command by below examples.

#### Sample File Creation
Create a file `employee.txt` in your system, with the below content

```
ajay manager account 45000
sunil clerk account 25000
varun manager sales 50000
amit manager account 47000
tarun peon sales 15000
deepak clerk sales 23000
sunil peon sales 13000
satvik director purchase 80000 
```

#### Example 1

Paste the below command in your terminal and press enter.

```
awk '{print}' employee.txt
```

* Notice the output, what did this command do?
<br><b>Answer:</b><br>
This is the default behavior of Awk ; wherein Awk prints every line of data from the specified file.

#### Example 2

Paste the below command in your terminal and press enter.

```
awk '/manager/ {print}' employee.txt 

```
* Notice the output, what did this command do?
<br><b>Answer:</b><br>
In the above example, the awk command prints all the line which matches with the 'manager'.

#### Example 3

```
awk '{print $1,$4}' employee.txt 
```

* Notice the output, what did this command do?
<br><b>Answer:</b> Spliting a Line Into Fields :-<br> For each record i.e line, the awk command splits the record delimited by whitespace character by default and stores it in the $n variables. If the line has 4 words, it will be stored in $1, $2, $3 and $4 respectively. Also, $0 represents the whole line.

### Note
* We have barely scratched the surface with `awk`, which is a powerful scripting language itself.
* Read the man page for the awk command and check the various other options that it supports.

### References:
https://www.geeksforgeeks.org/awk-command-unixlinux-examples/