## Learning by doing - `diff` and `patch`

* Spring 2019, CS35L - Lab 7
* TA: Rishab Ketan Doshi
* Week 3, Lecture 1, April 16
* src of these examples [here](https://linuxacademy.com/blog/linux/introduction-using-diff-and-patch/)

The commands diff and patch form a powerful combination. They are widely used to get differences between original files and updated files in such a way that other people who only have the original files can turn them into the updated files with just a single patch file that contains only the differences. 

### Example 1 - diff command

create two files originalfile and updatedfile using below commands

* ` echo "These are a few words." > originalfile `
* ` echo "These still are just a few words." > updatedfile `

Run the below command:

```
diff originalfile updatedfile
```

What is the output?

Explaining the output.

The 1c1 is a way of indicating line numbers and specifying what should be done. Note that those line numbers can also be line ranges (12,15 means line 12 to line 15). The “c” tells patch to replace the content of the lines. Two other characters with a meaning exist: “a” and “d”, with “a” meaning “add” or “append” and “d” meaning “delete”. The syntax is (line number or range)(c, a or d)(line number or range), although when using “a” or “d”, one of the (line number or range) parts may only contain a single line number.

* When using “c”, the line numbers left of it are the lines in the original file that should be replaced with text contained in the patch, and the line numbers right of it are the lines the content should be in in the patched version of the file.
* When using “a”, the line number on the left may only be a single number, meaning where to add the lines in the patched version of the file, and the line numbers right of it are the lines the content should be in in the patched version of the file.
* When using “d”, the line numbers left of it are the lines that should be deleted to create the patched version of the file, and the line number on the right may only be a single number, telling where the lines would have been in the patched version of the file if they wouldn’t have been deleted. 

### Example 2 - patch command

```
diff originalfile updatedfile > patchfile.patch
```

Outputs the information to a patch file. This can then be used to get the updated file if we have the original file.

To really apply the patch to get the updated file. We need to have a situation where we have the original file and the patch file. 

Lets say we have both of these on our friendsComputer. For the purposes of this class, lets say friendsComputer is a directory.

```
mkdir friendsComputer; cp originalfile friendsComputer/. ; cp patchfile.path friendsComputer/.
```

Now we have the originalfile and the patchfile on the friendsComputer. How does our friend get the updatedfile. 
Apply the patch!

```
cd friendsComputer;
```

```
patch originalfile -i patchfile.patch -o updatedfile
```

Verify that updatedfile on our friendsComputer is same as our computer.

```
diff updatedfile ../updatedfile
```

### Conclusion

Many more options exist, this tutorial was meant to just tease and introduce you to the diff and patch command. You will have to use these commands with different options for this weeks lab.

### Follow up:

1. What is the -pnum option used for in patch? (check `man patch`)
2. What is -u format used for in diff? (try above examples with -u format)
3. Can you compare and update directories with diff and patch? 