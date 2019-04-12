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
liam@yahoo.com
noah@yahoo.com
william@yahoo.com
james@yahoo.com
logan@yahoo.com
benjamin@yahoo.com
mason@yahoo.com
elijah@yahoo.com
oliver@yahoo.com
emma@yahoo.com
olivia@yahoo.com
ava@yahoo.com
isabella@yahoo.com
sophia@yahoo.com
mia@yahoo.com
charlotte@yahoo.com
amelia@yahoo.com
evelyn@yahoo.com
Hi
Ok
There
How are you gmail
Ok google
yahoo! This was awesome
yahoo was a popular search website
```

```
sed -E 's/^[a-z].*@yahoo\.com/rishab@gmail\.com/g' emails.txt 
```


* Notice the output, what did this command do?
<br><b>Answer:</b><br>
Finds all the strings that match the regular expression and replaces them with the string `rishab@gmail.com`

#### Example 5 : Backreferencing with `sed`

back-references are regular expression commands which refer to a previous part of the matched regular expression. Back-references are specified with backslash and a single digit (e.g. ‘\1’). The part of the regular expression they refer to is called a subexpression, and is designated with parentheses.

Back-references and subexpressions are used in two cases: in the regular expression search pattern, and in the replacement part of the s command.

The following example uses two subexpressions in the regular expression to match two space-separated words. The back-references in the replacement part prints the words in a different order:

```
echo "James Bond" | sed -E 's/(.*) (.*)/The name is \2, \1 \2./'

```
Output is:
```
The name is Bond, James Bond.
```

### Follow up 

* Read the man page for the sed command and check the various other options that sed supports.

* Write down atleast two other options that sed provides.

### References:

* https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/
* https://www.geeksforgeeks.org/sed-command-linux-set-2/
* https://www.gnu.org/software/sed/manual/html_node/Back_002dreferences-and-Subexpressions.html
