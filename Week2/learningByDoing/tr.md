## Learning by doing - `tr` command
* Spring 2019, CS35L - Lab 7
* TA: Rishab Ketan Doshi
* Week 2, Lecture 2, April 11

### Details

* TR command - short for translate characters
* It supports a range of transformations including uppercase to lowercase, squeezing repeating characters, deleting specific characters and basic find and replace.


### Learn by examples

We will learn the tr command by below examples.

#### Sample File Creation
Create a file `harry.txt` in your system, with the below content


```
Nearly                                                 ten       years       had       passed       since       the       Dursleys       had       woken       up       to       find
their       nephew       on       the       front       step,       but       Privet       Drive       had       hardly       changed       at
all.       The       sun       rose       on       the       same       tidy       front       gardens       and       lit       up       the       brass
number       four       on       the       Dursleys'       front       door;       it       crept       into       their       living
room,       which       was       almost       exactly       the       same       as       it       had       been       on       the       night
when       Mr.       Dursley       had       seen       that       fateful       news       report       about       the       owls.
```

#### Example 1

Paste the below command in your terminal and press enter.

```
cat harry.txt | tr "[a-z]" "[A-Z]"
```

* Notice the output, what did this command do?
* The above simple `tr` command translates all the lower case characters to uppercase characters.
* Did the original file change? 


#### Example 2
Paste the below command in your terminal and press enter.

```
tr -s [:space:] < harry.txt
```

* Notice the output, what did this command do?
<br><b>Answer:</b><br>
The -s option squeezes all the characters of the mentioned type(in this case space) and replaces it with one occurence.

#### Example 3
Paste the below command in your terminal and press enter.

```
cat harry.txt | tr -d [:space:]
```

* Notice the output, what did this command do?
<br><b>Answer:</b><br>
The -d flag is used for deletion of the mentioned character from the input. In this case, we deleted the space character. 

#### Example 4

Paste the below command in your terminal and press enter.

```
echo "my ID is 73535" | tr -cd [:digit:]
```

* Notice the output, what did this command do?
<br><b>Answer:</b><br>
You can complement the SET1(in this case [:digit:]) using -c option. The above command removed all characters except digits. `d` in `-cd` specifies that the complement set has to be deleted.

### Example 5

Paste the below command in your terminal and press enter.

```
echo "unix" | tr -c "u" "a"
```

* What is the output?
* Can you explain what is happening?
* all the characters other than u are being replaced with a

What happens when you add the `s` - squeeze option to the same command, as below:

```
echo "unix" | tr -cs "u" "a"
```

* What is the output?
* Can you explain what is happening?
* The 'a' character has reduced from a large number to just one character. This command means that squeeze all a's from the output.
* Look at the man documentation for tr and see how the -s option works

```
-s      
Squeeze multiple occurrences of the characters listed in the last operand (either string1 or string2) in the input into a single instance of the character.  This occurs
after all deletion and translation is completed.
```

### References:

* https://www.geeksforgeeks.org/tr-command-in-unix-linux-with-examples/