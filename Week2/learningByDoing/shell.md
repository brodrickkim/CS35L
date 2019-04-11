## Shell-Scripting

* Spring 2019, CS35L - Lab 7
* TA: Rishab Ketan Doshi
* Week 2, Lecture 2, April 11

### Details

#### Example - 1 (HelloWorld :D )

Copy paste below code into a file `helloWorld.sh`.

```
echo "Hello World :D"
```

* Try running the file using `./helloWorld.sh`.
* Any errors?
* Before fixing error , run the command `echo $?`  (note the output number) (we'll discuss this again)
* Fix by making sure that file contains executable permission


```
chmod +x helloWorld.sh
```

Also `printf` can be used to print the file; printf can output data with complex formatting, just like C printf().

```
echo "Hello World :D"
printf "%.3e\n" 46553132.14562253
```

#### Example - 2 (Find which shell executes your code)

Copy paste below code into a file `shellIdentifier.sh`

```
#!/bin/csh
echo "This script is being executed by : "
ps -p $$ -ocomm=
```

Run the above file with different options. What is the output you get for each of the below cases?

* `./shellIdentifier.sh`
* `sh shellIdentifier.sh`
* `bash shellIdentifier.sh`
* `ksh shellIdentifier.sh`

How to identify your default shell?
Hint: Can you do something to your first line in the shell script?

#### Example - 3 (Variables)

Copy paste below code into a file `potternames.sh`

```
#!/bin/sh

dumbledore=albus_percival_wulfric_brian_dumbledore

echo "Printing dumbledore's long name! $dumbledore"

first=tom middle=marvolo last=riddle 	#Multiple assignments allowed on one line 

echo "First: $first"
echo "Middle: $middle"
echo "Last: $last"

fullname="$first $middle $last" 		#Double quotes required here, for concatenating 

echo "Fullname : $fullname"

anothername="he who must not be named" #Use quotes for whitespace in value 

echo "Anothername : $anothername"

oldname=$fullname 

echo "Oldname : $oldname"
```

Details:

* Variable names start with a letter or underscore and may contain any number of following letters, digits, or underscores
* Hold string variables by default
* How do we write comments in shell-scripts?


#### Example - 4 (Quotes)

Copy paste below code into file `quotes.sh`

```
#!/bin/sh

a=ls

echo "Printing a using single quotes"
echo '$a' 
echo "****"
echo " "

echo "Printing a using double quotes"
echo "$a" 
echo "****"
echo " "

echo "Printing a using backticks"
echo `$a`
echo "****"
echo " "

var=$(ls)
echo "Printing var using () notation" 
echo $var
echo "****"
echo " "

```
<b>Explanation :- </b>

<b>Single quotes ' '</b>

* Do not expand at all, literal meaning 

<b>Double quotes " "</b>

* Almost like single quotes but expand backticks and $

<b>Backticks ``` `` ``` or `$()`</b>

* Expand as shell commands

#### Example - 5 (Commandline arguments + Arithmetic operations)

Copy paste below code into the file `add.sh`

```
#!/bin/sh
echo "$1 + $2"
sum=$(($1 + $2)) 
echo "The sum is $sum"
```

Details: nth argument(starting from 1 not 0) can be accessed by $n. If n > 9, then use {} => use `echo "10th arg is {10}"`

#### Example - 6 (if, else statements ; case esac )

Copy paste below code into the file `greater.sh`

```
#!/bin/bash 

echo "No. of arguments to the script $#"

if [ $1 -gt $2 ] 
then
	echo "$1 greater than $2" 
else
	echo "$1 lesser than $2"
fi
```

* What is $1, $2, $#?

* What is -gt?

```
#!/bin/sh

a=10
b=20

if [ $a == $b ]
then
   echo "a is equal to b"
elif [ $a -gt $b ]
then
   echo "a is greater than b"
elif [ $a -lt $b ]
then
   echo "a is less than b"
else
   echo "None of the condition met"
fi
```

* Check and see what `case ... esac` is.

```
CARS="bmw"
  
#Pass the variable in string 
case "$CARS" in 
    #case 1 
    "mercedes") echo "Headquarters - Affalterbach, Germany" ;; 
      
    #case 2 
    "audi") echo "Headquarters - Ingolstadt, Germany" ;; 
      
    #case 3 
    "bmw") echo "Headquarters - Chennai, Tamil Nadu, India" ;; 
esac 

```

#### Example 7 - Arrays

src - https://www.geeksforgeeks.org/array-basics-shell-scripting-set-1/

```
#! /bin/bash 
# To declare static Array 
arr=(prakhar ankit 1 rishabh manish abhinav) 

# To print all elements of array 
echo ${arr[@]}	 # prakhar ankit 1 rishabh manish abhinav 
echo ${arr[*]}	 # prakhar ankit 1 rishabh manish abhinav 
echo ${arr[@]:0} # prakhar ankit 1 rishabh manish abhinav 
echo ${arr[*]:0} # prakhar ankit 1 rishabh manish abhinav 

# To print first element 
echo ${arr[0]}	 # prakhar 
echo ${arr}		 # prakhar 

# To print particular element 
echo ${arr[3]}	 # rishabh 
echo ${arr[1]}	 # ankit 

# To print elements from a particular index 
echo ${arr[@]:0} # prakhar ankit 1 rishabh manish abhinav 
echo ${arr[@]:1} # ankit 1 rishabh manish abhinav 
echo ${arr[@]:2} # 1 rishabh manish abhinav 
echo ${arr[0]:1} # rakhar 

# To print elements in range 
echo ${arr[@]:1:4} # ankit 1 rishabh manish 
echo ${arr[@]:2:3} # 1 rishabh manish 
echo ${arr[0]:1:3} # rak 

# Length of Particular element 
echo ${#arr[0]}	 # 7 
echo ${#arr}	 # 7 

# Size of an Array 
echo ${#arr[@]}	 # 6 
echo ${#arr[*]}	 # 6 

# Search in Array 
echo ${arr[@]/*[aA]*/} # 1 

# Replacing Substring Temporary 
echo ${arr[@]//a/A}	 # prAkhAr Ankit 1 rishAbh mAnish AbhinAv 
echo ${arr[@]}		 # prakhar ankit 1 rishabh manish abhinav 
echo ${arr[0]//r/R}	 # pRakhaR 

```


#### Example 8 - Loops

Copy paste below code into the file 'loops.sh'

Learn syntax of :

* while loop
* for loop


```
#!/bin/sh

#while loop illustration

echo "While loop below"
COUNT=6
while [ $COUNT -gt 0 ] 
do
echo "Value of count is: $COUNT"
((COUNT=COUNT-1))
done 

#for loop illustration

echo "For loop below"

files=`ls`
for f in $files 
do
echo $f 
done
```

* we have `break` and `continue` in shell too - check them out

#### Example 9 - Debugging shell scripts

You can debug your shell scripts by setting execution tracing to on or off.

This can be done by using the set command as below. Copy paste the code into `debugExample.sh` and try running it.


```
#!/bin/bash
clear
 
# turn on debug mode
set -x
for f in *
do
   file $f
done
# turn OFF debug mode
set +x
ls
# more commands
```

* set –x: to turn it on 
* set +x: to turn it off

Alternatively, you can start your shell script with the -x flag as below:

```
bash -x loops.sh 
```

#### Example 10 - Iterating through commandline arguments

```
#!/bin/bash
for var in "$@"
do
    echo "$var"
done
```

#### Example 11 - Iterating through files in the current directory using `ls`

```
#!/bin/bash
for var in `ls`
do
    echo "$var"
done
```


#### Example 12 - Exit status in shell scripts

Typical Values Of Exit Status On Bourne Shell
0 – Success.
1 – A built-in command failure.
2 – A syntax error has occurred.
3 – Signal received that is not trapped

We can use these to decide control of next statements in the shell script.

Mainly concerned with status 0 or not.

Create a file `tmpwords.txt` with below content


```
cherishable
flourishable
imperishability
imperishable
imperishableness
imperishably
nonperishable
nonperishables
nourishable
perishability
perishabilty
perishable
perishableness
perishables
perishably
unnourishable
unperishable
unperishableness
unperishably
```

Try out this shell script

`$?` - status of previous command

```

#!/bin/bash

echo "Looking for 'rishab' in the words file , output below"
cat tmpwords.txt | grep "rishab"

if [ $? -eq 0 ] 
then
	echo "Status code was 0, all good" 
else
	echo "Status code was non zero, something bad has happened"
fi


echo "Looking for 'rishabdoshi' in the words file, output below"
cat tmpwords.txt | grep "rishabdoshi"

if [ $? -eq 0 ] 
then
	echo "Status code was 0, all good" 
else
	echo "Status code was non zero, something bad has happened"
	echo "Status code was $?" # what does this print? How do you explain this?
fi


```

