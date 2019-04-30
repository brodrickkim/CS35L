# System Calls

## References
* Read, Write - https://www.usna.edu/Users/cs/aviv/classes/ic221/s18/units/04/unit.html#orgf339059
* Open, Close - https://www.geeksforgeeks.org/input-output-system-calls-c-create-open-close-read-write/

## write
Using a lower level function, a system call, to write directly to the standard out device, i.e., the terminal window. The system call that writes to a file or device is write(). Bellow, is a the system call hello world:


```c
#include <unistd.h>

int main(int argc, char * argv[]){
  char hello[] = "Hello World\n";
  char *p;

  for(p = hello ; *p ; p++){
     write(1, p, 1); 
  }

}
```

```c
#include <unistd.h>

int main(int argc, char * argv[]){
  char hello[] = "Hello World\n";
  char *p;

  for(p = hello ; *p ; p++){
     write(1, p, 1); 
  }

  for(p=hello; *p ; p+=2) {
     write(1,p,2);
  }

}
```

```
//    .-- Write to standard out, file descriptor 1
//    v
write(1, p, 1); 
//       ^  ^
//       |  '--- Number of bytes to write, just the char p points to
//       |
//       '-------- char *, points to the byte we want to write
```

write()'ing a Buffer of Bytes
The above example was working with one byte at a time, but system call I/O is buffered. The write() and read() system calls are not string based I/O, like the format print functions. They will read and write any data type. Let's look at bit more at the actual function prototype form the man page:

```
  ssize_t write(int fd, const void *buf, size_t count);
//                  ^               ^            ^
//file descriptor---'       buffer--'            '-- num. bytes to write
```

Note that the second argument is not a char *, but rather a void *, which means that it accepts a pointer to any type. We refer to this as the buffer. A buffer is the general term for an array of bytes. Unlike a string, which is also an array of bytes, as char's, strings have the added property of always being NULL terminated. Buffers are more low-level, and can refer to any data type. As we learned in previous lessons, pointers and arrays are the same thing and that we can arbitrarily cast between different pointer types. This allows us to arbitrarily cast any data type to a byte array, a buffer, and work with the data byte-by-byte. Consider the example below, where we write a pair_t.

```c
/*write_pair.c*/
#include <unistd.h>

typedef struct{
  int left;
  int right;
} pair_t;

int main(int argc, char * argv[]){

  pair_t p;
  p.left = 10;
  p.right = 20;

  write(1, &p, sizeof(pair_t));

  return 0;
}
```

## read

```
  ssize_t read(int fd,      void *buf, size_t count);
//                  ^               ^            ^
//file descriptor---'       buffer--'            '-- num. bytes to write
```

read() will attempt to read up to count number of bytes and store them into the buffer. The total number of bytes read is returned. This is important so that you know how many bytes made it into the buffer. If EOF is reached, read() returns 0.

To demonstrate the connection between read()'ing and write()'ing raw bytes, let's continue the example from above. Suppose we are interested in reading in the raw bytes of a pair_t. We can do the following:

```c
/*read_pair.c*/
#include <unistd.h>
#include <stdio.h> //format print

typedef struct{
  int left;
  int right;
} pair_t;

int main(int argc, char * argv[]){

  pair_t p;

  read(0, &p, sizeof(pair_t));

  printf("left: %d right: %d\n",p.left, p.right);

  return 0;
}
```

Note that the read() is reading from file descriptor 0, which is standard input, and the buffer is the address of the p, reading at most the size of a pair_t. The read() command is just reading byte-by-byte the data that is the pair_t and filling up the memory region of p with those bytes. It might be a bit mystifying, but this actually works, and we can test it by aligning the two programs in a pipeline.

```
#>./write_pair | ./read_pair 
left: 10 right: 20
```

## File I/O

The system call to open a file is open(), which is well named, and the system call to close a file is close(), also well named. These system calls are low level and do operate over file streams, as FILE *, but instead return an integer value which is the file descriptor.

All open files in the operating system are managed via file descriptors, which are indexes into the file descriptor table. The file descriptor table is a kernel data structure which tracks open files for all programs, and we'll discuss the details of this in a later lesson.

### Open

Create: Used to Create a new empty file.

open: Used to Open the file for reading, writing or both.
Syntax in C language 

```
#include<sys/types.h>
#includ<sys/stat.h>
#include <fcntl.h>  
int open (const char* Path, int flags [, int mode ]); 
```

Parameters
* Path : path to file which you want to use
* use absolute path begin with “/”, when you are not work in same directory of file.
* Use relative path which is only file name with extension, when you are work in same directory of file.
* flags : How you like to use

```O_RDONLY: read only, O_WRONLY: write only, O_RDWR: read and write, O_CREAT: create file if it doesn’t exist, O_EXCL: prevent creation if it already exists```

How it works in the OS:
* Find existing file on disk
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

### Close

Tells the operating system you are done with a file descriptor and Close the file which pointed by fd.
Syntax in C language
```
#include <fcntl.h>
int close(int fd); 
```

Parameter
* fd :file descriptor

Return
* 0 on success.
* -1 on error.

How it works in the OS:

* Destroy file table entry referenced by element fd of file descriptor table
	– As long as no other process is pointing to it!
* Set element fd of file descriptor table to NULL

```c
// C program to illustrate close system Call 
#include<stdio.h> 
#include <fcntl.h> 
int main() 
{ 
	int fd1 = open("foo.txt", O_RDONLY); 
	if (fd1 < 0) 
	{ 
		perror("c1"); 
		exit(1); 
	} 
	printf("opened the fd = % d\n", fd1); 
	
	// Using close system Call 
	if (close(fd1) < 0) 
	{ 
		perror("c1"); 
		exit(1); 
	} 
	printf("closed the fd.\n"); 
} 
```

## More examples:

### Read example 1
create a file `foo.txt` with the below content
```
0123456789abcdefghijklmnopqrstuvwxyz
```

```c
// C program to illustrate 
// read system Call 
#include<stdio.h> 
#include <fcntl.h> 
int main() 
{ 
  int fd, sz; 
  char *c = (char *) calloc(100, sizeof(char)); 
  
  fd = open("foo.txt", O_RDONLY); 
  if (fd < 0) { perror("r1"); exit(1); } 
  
  sz = read(fd, c, 10); 
  printf("called read(% d, c, 10).  returned that"
         " %d bytes  were read.\n", fd, sz); 
  c[sz] = '\0'; 
  printf("Those bytes are as follows: % s\n", c); 
} 
```

### Read example 2
```c
// C program to illustrate 
// read system Call 
#include<stdio.h> 
#include<fcntl.h> 
  
int main() 
{ 
    char c; 
    int fd1 = open("foo.txt", O_RDONLY, 0); 
    int fd2 = open("foo.txt", O_RDONLY, 0); 
    read(fd1, &c, 1); 
    printf("c = % c\n", c); 
    read(fd2, &c, 1); 
    printf("c = % c\n", c); 
    exit(0); 
} 
```

The descriptors fd1 and fd2 each have their own open file table entry, so each descriptor has its own file position for foo.txt. Thus, the read from fd2 reads the first byte of foo.txt, and the output is c = 0 for both the print statements.

### Write example
```c
// C program to illustrate 
// write system Call 
#include<stdio.h> 
#include <fcntl.h> 
main() 
{ 
  int sz; 
  
  int fd = open("foowrite.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644); 
  if (fd < 0) 
  { 
     perror("r1"); 
     exit(1); 
  } 
  
  sz = write(fd, "hello geeks\n", strlen("hello geeks\n")); 
  
  printf("called write(% d, \"hello geeks\\n\", %d)."
    " It returned %d\n", fd, strlen("hello geeks\n"), sz); 
  
  close(fd); 
} 

```

