# od

od command in Linux is used to convert the content of input in different formats with octal format as the default format.This command is especially useful when debugging Linux scripts for unwanted changes or characters.

Create a file `input.txt`

```
100
101
102
103
104
105
```

## Example 1
```shell
od -c -w4 < input.txt
```

outputs

```
0000000   1   0   0  \n
0000004   1   0   1  \n
0000010   1   0   2  \n
0000014   1   0   3  \n
0000020   1   0   4  \n
0000024   1   0   5  \n
0000030
```

Explanation:

* The first column gives the byte offset from the beginning of the file. What this means is that the output in this line begins at so many bytes from the start of the line.
* The `-w4` option tells `od` that the output has to be such that there are 4 bytes on every output line. Try running without this flag to see what happens. (it will print out default number of bytes-32 on every line).
* The `-c` option tells `od` that output has to be in character format. Essentially just like input characters.

## Example 2

```shell
od -b -w4 < input.txt
```

outputs 

```
0000000 061 060 060 012
0000004 061 060 061 012
0000010 061 060 062 012
0000014 061 060 063 012
0000020 061 060 064 012
0000024 061 060 065 012
0000030
```

Explanation:

* The `-b` option tells `od` that the output has to be in octal format. `1`s ascii code is 49, which when represented as an octal is 61. `0`s ascii code is 48, which is 60 in octal. Similarly other numbers can be explained.

## Example 3

```shell
od -An -w4 -c < input.tx
```

outputs
```
   1   0   0  \n
   1   0   1  \n
   1   0   2  \n
   1   0   3  \n
   1   0   4  \n
   1   0   5  \n
```

Explanation:

The first column is removed when you add the `-An` flag. Check man page for what other options are available for the `-A` flag and what `n` means.

## Example 4

```shell
od -An -w4 -b -N2 < input.txt
```

outputs

```
 061 060
```

Explanation:

The `-N` option is used to specify the number of bytes to read from the file.

## Example 5

```shell
od -An -b -w1 < input.txt
```

outputs

```
061
 060
*
 012
 061
 060
 061
 012
 061
 060
 062
 012
 061
 060
 063
 012
 061
 060
 064
 012
 061
 060
 065
 012
 061
 060
*
 012
```

The * in the output signifies output that has been supressed as these are duplicates of values seen previously. If we dont want duplicates to be suppressed, we have to use a `-v` option.

```
od -An -b -w1 -v < input.txt
```

## Example 6

```
od -An -w2 -v -o -t d2 < input.txt
```

output

```
030061
  12337
 005060
   2608
 030061
  12337
 005061
   2609
 030061
  12337
 005062
   2610
 030061
  12337
 005063
   2611
 030061
  12337
 005064
   2612
 030061
  12337
 005065
   2613
 030061
  12337
 005060
   2608
```

Explanation:

The odd numbered rows are the octal representation of the bytes(-o) as we saw above and the even numbered lines are the decimal representation of these numbers(-d2).

## Lab Hints
* Check man page to see how you can use od to create floating point numbers(-fF)?
