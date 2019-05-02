# f-stat

Content in this file is extended from this [source](https://www.go4expert.com/articles/understanding-linux-fstat-example-t27449/).

### Read about fstat

```
man fstat
```

These  functions  return  information about a file like permissions, file type, file size etc.

### signature

```
int fstat(int fd, struct stat *buf);
```
return  information about a file, in the buffer pointed to by buf.

The stat structure is where the information is stored. This looks like below:

```c
 struct stat {
               dev_t     st_dev;         /* ID of device containing file */
               ino_t     st_ino;         /* inode number */
               mode_t    st_mode;        /* file type and mode */
               nlink_t   st_nlink;       /* number of hard links */
               uid_t     st_uid;         /* user ID of owner */
               gid_t     st_gid;         /* group ID of owner */
               dev_t     st_rdev;        /* device ID (if special file) */
               off_t     st_size;        /* total size, in bytes */
               blksize_t st_blksize;     /* blocksize for filesystem I/O */
               blkcnt_t  st_blocks;      /* number of 512B blocks allocated */
               };
```

This is available in the header file `sys/stat.h`.

### Example 1 - Basic Use

```c
#include <stdio.h> 
#include <sys/types.h> 
#include <sys/stat.h> 
#include <unistd.h> 
#include <errno.h> 
#include <string.h> 
#include <fcntl.h> 
 
int main(void) 
{ 
    int f_d = 0; 
    struct stat st; 
      
    // Open the file test.txt through open() 
    // Note that since the call to open directly gives 
    // integer file descriptor so we used open here. 
    // One can also use fopen() that returns FILE* 
    // object. Use fileno() in that case to convert 
    // FILE* object into the integer file descriptor 
    f_d = open("test.txt",O_RDONLY); 
 
    //Check if open() was successful 
    if(-1 == f_d) 
    { 
        printf("\n NULL File descriptor\n"); 
        return -1; 
    } 
 
    // set the errno to default value 
    errno = 0; 
    // Now a call to fstat is made 
    // Note that the address of struct stat object 
    // is passed as the second argument 
    if(fstat(f_d, &st)) 
    { 
        printf("\nfstat error: [%s]\n",strerror(errno)); 
        close(f_d); 
        return -1; 
    } 
 
    // Access the object 'buff' for accessing 
    // various stats information. 
 
    // Close the file 
    close(f_d); 
 
    return 0; 
}
```

### Example 2 - File Type, File Size, Modification Time.

```c
#include <stdio.h> 
#include <sys/types.h> 
#include <sys/stat.h> 
#include <unistd.h> 
#include <errno.h> 
#include <string.h> 
#include <fcntl.h> 
#include <time.h> 
 
int main(void) 
{ 
    int f_d = 0; 
    struct stat st; 
      
    // Open the file test.txt through open() 
    // Note that since the call to open directly gives 
    // integer file descriptor so we used open here. 
    // One can also use fopen() that returns FILE* 
    // object. Use fileno() in that case to convert 
    // FILE* object into the integer file descriptor 
    f_d = open("test.txt",O_RDONLY); 
 
    //Check if open() was successful 
    if(-1 == f_d) 
    { 
        printf("\n NULL File descriptor\n"); 
        return -1; 
    } 
 
    // set the errno to default value 
    errno = 0; 
    // Now a call to fstat is made 
    // Note that the address of struct stat object 
    // is passed as the second argument 
    if(fstat(f_d, &st)) 
    { 
        printf("\nfstat error: [%s]\n",strerror(errno)); 
        close(f_d); 
        return -1; 
    } 
 
    switch (st.st_mode & S_IFMT) { 
           case S_IFBLK:  printf("block device\n");            break; 
           case S_IFCHR:  printf("character device\n");        break; 
           case S_IFDIR:  printf("directory\n");               break; 
           case S_IFIFO:  printf("FIFO/pipe\n");               break; 
           case S_IFLNK:  printf("symlink\n");                 break; 
           case S_IFREG:  printf("regular file\n");            break; 
           case S_IFSOCK: printf("socket\n");                  break; 
           default:       printf("unknown?\n");                break; 
           } 
 
     printf("File size:                %lld bytes\n",(long long) st.st_size); 
     printf("Last status change:       %s", ctime(&st.st_ctime)); 
     printf("Last file access:         %s", ctime(&st.st_atime)); 
     printf("Last file modification:   %s", ctime(&st.st_mtime)); 
 
 
    // Close the file 
    close(f_d); 
 
    return 0; 
}
```

## HW Hints
* Use this function to check type of file, if file is growing 
