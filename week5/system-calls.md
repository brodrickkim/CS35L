# System Calls

## Create:

Create: Used to Create a new empty file.

Parameters :

1. filename : name of the file which you want to create
2. mode : indicates permissions of new file.

Returns :
return first unused file descriptor (generally 3 when first creat use in process beacuse 0, 1, 2 fd are reserved)
return -1 when error

How it works in the OS
* Create new empty file on disk
* Create file table entry
* Set first unused file descriptor to point to file table entry
* Return file descriptor used, -1 upon failure

```c
// C program to illustrate 
// open system call 
#include<stdio.h> 
#include<fcntl.h> 
#include<errno.h> 
extern int errno; 
int main() 
{	 
	// if file does not have in directory 
	// then file foo.txt is created. 
	int fd = open("foo.txt", O_RDONLY | O_CREAT); 
	
	printf("fd = %d/n", fd); 
	
	if (fd ==-1) 
	{ 
		// print which type of error have in a code 
		printf("Error Number % d\n", errno); 
		
		// print program detail "Success or failure" 
		perror("Program");				 
	} 
	return 0; 
} 
```
