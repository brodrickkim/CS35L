## Learning by doing - `sed` command
* Spring 2019, CS35L - Lab 7
* TA: Rishab Ketan Doshi
* Week 2, Lecture 2, April 11

### Details

* SED command - stands for stream editor ; can be used to edits text in a scriptable manner.
* Can perform lot's of functions on a file like: searching, find and replace, insertion or deletion.
* Mainly used for find and replace(substituition).

### Learn by examples

We will learn the sed command by below examples.

#### Sample File Creation
Create a file `geekfile.txt` in your system, with the below content

```
unix is great os. unix is opensource. unix is free os.
learn operating system.
unix linux which one you choose.
unix is easy to learn.unix is a multiuser os.Learn unix .unix is a powerful.
```

#### Example 1

Paste the below command in your terminal and press enter.
```
sed 's/unix/linux/' geekfile.txt
```

* Notice the output, what did this command do?
* The above simple `sed` command replaces the word "unix" with "linux" from the file.
* Did the original file change? 

<b>Answer:</b><br>
Here the "s" specifies the substitution operation. The "/" are delimiters. The "unix" is the search pattern and the "linux" is the replacement string.

By default, the sed command replaces the first occurrence of the pattern in each line and it won’t replace the second, third…occurrence in the line.

#### Example 2
Paste the below command in your terminal and press enter.

```
sed 's/unix/linux/2' geekfile.txt
```

* Notice the output, what did this command do?
<br><b>Answer:</b><br>
Use the /1, /2 etc flags to replace the first, second occurrence of a pattern in a line. The below command replaces the second occurrence of the word "unix" with "linux" in a line.

#### Example 3
Paste the below command in your terminal and press enter.

```
sed 's/unix/linux/g' geekfile.txt
```

* Notice the output, what did this command do?
<br><b>Answer:</b><br>
The substitute flag /g (global replacement) specifies the sed command to replace all the occurrences of the string in the line.

#### Example 4

```
sed -E 's/^[a-z].*@yahoo\.com/rishab@gmail\.com/g' emails.txt 
```

* Notice the output, what did this command do?
<br><b>Answer:</b><br>
Finds all the strings that match the regular expression and replaces them with the string `rishab@gmail.com`


### Follow up 

* Read the man page for the sed command and check the various other options that sed supports.

* Write down atleast two other options that sed provides.

### References:

* https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/
* https://www.geeksforgeeks.org/sed-command-linux-set-2/