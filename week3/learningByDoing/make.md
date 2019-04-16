## Learning by doing - `make`
* Spring 2019, CS35L - Lab 7
* TA: Rishab Ketan Doshi
* Week 3, Lecture 1, April 16

### Example 1 - helloworld makefile 

* This example is taken from lab 8's slides for this week.

Create below hello.c file

```
#include <stdio.h> 

int main() { 
	printf("Hello, world!\n"); 
	return 0; 
}
```

Makefile task:

* Compile everything together with a single command and execute it - `gcc hello.c`
* Now create a simple makefile(given below) to compile these files
* Run the executable and observe the output
* Invoke make again and observe
* Change hello.cpp, do a make again and observe the output

A makefile for this can be as below:

```
all: hello.exe 
hello.exe: hello.o 
		gcc -o hello.exe hello.o 
hello.o: hello.c 
		gcc -c hello.c 
clean: 
		rm hello.o hello.exe
```


### Example 2 - Multiple files

Create below files with the same name in your playground directory for this week.

* [DigitalTimeException.h](https://github.com/Yushen-Chang-9/C-Plus-Plus-HW-2016/blob/master/DigitalTimeException.h)
* [DigitalTimeException.cpp](https://github.com/Yushen-Chang-9/C-Plus-Plus-HW-2016/blob/master/DigitalTimeException.cpp)
* [DigitalTimeException.h](https://github.com/Yushen-Chang-9/C-Plus-Plus-HW-2016/blob/master/DigitalTimeException.h)
* [DigitalTimeException.cpp](https://github.com/Yushen-Chang-9/C-Plus-Plus-HW-2016/blob/master/DigitalTimeException.cpp)
* [DigitalTest.cpp](https://github.com/Yushen-Chang-9/C-Plus-Plus-HW-2016/blob/master/DigitalTest.cpp)

Paste the below command in your terminal in the same directory where all files are present.

* `g++ DigitalTest.cpp`
* `g++ DigitalTest.cpp DigitalTime.cpp `
* `g++ DigitalTest.cpp DigitalTime.cpp DigitalTimeException.cpp`

Which one worked? Why?

```
all: DigitalTest.o
DigitalTest.o: DigitalTest.cpp DigitalTime.cpp DigitalTimeException.cpp
		gcc -c DigitalTest.cpp DigitalTime.cpp DigitalTimeException.cpp
clean: 
		rm DigitalTest.o DigitalTest
```
