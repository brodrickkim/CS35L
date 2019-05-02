# lseek

* We saw that with every file descriptor, there is a file-pointer that refers to the location in the file from where read/write operations are done.
* lseek is a system call that is used to modify this location in the file.
* The new location can be specified in different modes / ways 
  * Relative to current location of pointer
  * Relative to end of file
  * In Absolute terms
  
## syntax

```c
off_t lseek(int fd, off_t offset, int whence);
```

1. fd is the file descriptor whose file-pointer you want to modify
2. offset is the number of bytes you want to modify the pointer by 
3. whence is the mode in which the lseek works. Below table describes the legal values it can take and their meanings respectively.

    | Value |	Meaning |
    --------------------|------------------|
    | SEEK_SET |	Offset is to be measured in absolute terms. |
    | SEEK_CUR |	Offset is to be measured relative to the current location of the pointer. |
    | SEEK_END | Offset is to be measured relative to the end of the file. |


## Example - 1 - read,write,lseek
* Create a file foo.txt

```
I will write after this full stop.
<this_will_be_replaced_by_system_call>
 <this_is_content_present_at_the_end>..<this_content_starts_2_bytes_after_your_last_read>
```

```c
#include<stdio.h>
#include <fcntl.h>
int main()
{
  int fd, sz_read,sz_write;
  char *c = (char *) malloc(100*sizeof(char));
  char *new_buffer = (char *) malloc(100*sizeof(char));

  fd = open("foo.txt", O_RDWR);
  if (fd < 0) { perror("r1"); exit(1); }

  //reading 35 bytes from the file foo.txt
  sz_read = read(fd, c, 35);
  printf("called read(% d, c, 35).  returned that"
         " %d bytes  were read.\n", fd, sz_read);
  c[sz_read] = '\0';
  printf("Those bytes are as follows: % s\n", c);
  
  sz_write = write(fd, "**This was written by the system call**", strlen("**This was written by the system call**")); 
  
  printf("called write(%d, \"**This was written by the system call**\", %d). It returned %d\n", fd, strlen("**This was written by the system call**"), sz_write); 
  
  //Now lets read the file again.
  sz_read = read(fd, new_buffer, 37);
  printf("called read(% d, new_buffer, 37).  returned that"
         " %d bytes  were read.\n", fd, sz_read);
  new_buffer[sz_read] = '\0';
  printf("Those bytes are as follows: % s\n", new_buffer);
  
  //changing position of file-pointer. Incrementing by 2 bytes from current position.
  printf("\nGoing to call lseek now. I want to increment pointer by 2 bytes. Fingers crossed \n");
  lseek(fd, 2, SEEK_CUR);
  
  //reading content now
  char *another_new_buffer = (char *) malloc(100*sizeof(char));
  sz_read = read(fd, another_new_buffer, 51);
  printf("called read(% d, another_new_buffer, 51).  returned that"
         " %d bytes  were read.\n", fd, sz_read);
  another_new_buffer[sz_read] = '\0';
  printf("Those bytes are as follows: % s\n", another_new_buffer);
}
```

## Example 2 - lseek with different options

```
<this_content_is_at_the_beginning_of_the_file_and_measures_69_bytes>
<i_am_a_40_byte_block_that_you_skipped>
<this_content_starts_at_110_bytes_from_top>
```

```
#include<stdio.h>
#include <fcntl.h>
int main()
{
  int fd, sz_read;
  char *c = (char *) malloc(100*sizeof(char));
  char *new_buffer = (char *) malloc(100*sizeof(char));

  fd = open("newfoo.txt", O_RDONLY);
  if (fd < 0) { perror("r1"); exit(1); }

  //reading 69 bytes from the file newfoo.txt
  sz_read = read(fd, c, 69);
  printf("called read(% d, c, 69).  returned that"
         " %d bytes  were read.\n", fd, sz_read);
  c[sz_read] = '\0';
  printf("Those bytes are as follows: % s\n", c);
  
  //changing position of file-pointer. Incrementing by 40 bytes from current position.
  printf("\n\nGoing to call lseek now. I want to increment pointer by 40 bytes. Fingers crossed \n\n");
  lseek(fd, 40, SEEK_CUR);

  
  //Now lets read the file again.
  sz_read = read(fd, new_buffer, 44);
  printf("called read(% d, new_buffer, 44).  returned that"
         " %d bytes  were read.\n", fd, sz_read);
  new_buffer[sz_read] = '\0';
  printf("Those bytes are as follows: % s\n", new_buffer);
  
  //setting pointer to top 110 bytes from the start of the file
    printf("\n\nGoing to call lseek now. I want to change pointer to 110 bytes from start of the file. Fingers crossed \n\n");
  lseek(fd, 110, SEEK_SET);
  
  //reading content now
  char *another_new_buffer = (char *) malloc(100*sizeof(char));
  sz_read = read(fd, another_new_buffer, 44);
  printf("called read(% d, another_new_buffer, 44).  returned that"
         " %d bytes  were read.\n", fd, sz_read);
  another_new_buffer[sz_read] = '\0';
  printf("Those bytes are as follows: % s\n", another_new_buffer);
}


```

## HW Hints
* How to use lseek on a growing file?
* Check if file has grown using fstat before and after reading the file using system calls.
* If file has grown, use lseek to move to the point from where you need to start reading the file again.

