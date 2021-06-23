# Optimised-File-System
Through this project we have implemented the basic functions of the file system and we have optimized the existing file system by adding 
features such as reducing seek time for next free block using priority queue with linked list for dynamic allocation and also reducing memory 
fragmentation. Using 128 bytes block size for the 20 MB application successfully optimizes over the existing file system.
## Methodology
Since we had come across one method of handling and improving the disk performance and free space management and have noticed the 
pros and cons of the restructuring method, we wanted to try a different technique to address the same issue of disk space and free memory 
management. Generally, operating systems have block size of 1-4KB. But here, we plan to create an application using only 20 MB, where we 
will be dividing 20 MB memory in 163840 blocks, each of 128 bytes.
The reason why we chose that particular block size is: As we increase the size of the block, more and more fragmentation occurs. As we 
decrease the size of block the size of the File Allocation table will increase, which will cause wastage of memory without storing any useful 
information. It will also increase the time for seeking the free block, time for finding a particular file for read, write and rename. So, Small 
blocks are bad for performance but good for disk space utilization and larger blocks are bad for disk utilization but good for performance. So, 
the size of 128 bytes per block is chosen to balance both the memory efficiency and time efficiency.
In order to store the file location and access it, the system will maintain two tables, that is one, file allocation table and second, file detail 
table.
The file detail table will store all the attributes of the file like the file name, the size, the date and time of creation, various file permissions 
etc. These attributes will be stored along with the bytes needed to store this information.
In the file allocation table, any file which has size more than 128 bytes will consume more than one block of memory. Thus, here in our 
method, to avoid external fragmentation, the memory allocation will not be restricted to continuous memory blocks. Therefore, the file 
allocation table will maintain and store the address of the next block in the particular file.
Each entry in FAT will consume 3 bytes of memory. For 20 MB space we made (20*1024*1024/128)= 163840 blocks of size 128 bytes. So the 
total size of FAT will be 163840*3 = 491520 bytes which is around 480 KB (491520/1024=480).
This being the new technique we will be using, we will also create a basic file system which when given commands will perform functions like 
creating a file, deleting a file, reading, writing, renaming a file etc. 

The file Disk.txt stores all the details of the table as text plus its allocation details
## Features
Here we have focused on optimization of two features.
- Seek time for free block To keep track of all the free blocks we are maintaining a simple queue which gives a free block for allocation in constant 
time or in O(1) complexity. Because FAT does not restrict the allocation of block to only continuous blocks, system does not need to traverse the 
whole memory for seeking the free block.
- Reducing memory fragmentation If a file need 20 blocks of memory then it will be accommodated even if there are no 20 continuous blocks 
available. Thus it will completely avoid external fragmentation. To reduce the internal fragmentation, we have reduced the block size down to 128 
bytes.

## Results
![image](https://user-images.githubusercontent.com/70501926/123091302-cf8f3400-d446-11eb-9c00-6d6291e93960.png)
![image](https://user-images.githubusercontent.com/70501926/123091321-d6b64200-d446-11eb-81dc-9fd3e598bcf9.png)
![image](https://user-images.githubusercontent.com/70501926/123091360-e0d84080-d446-11eb-89a6-15bdc53d6596.png)
![image](https://user-images.githubusercontent.com/70501926/123091381-e766b800-d446-11eb-957e-5053c4cf2100.png)
![image](https://user-images.githubusercontent.com/70501926/123091417-f0578980-d446-11eb-9535-31c9a1156bbb.png)
![image](https://user-images.githubusercontent.com/70501926/123091448-f9e0f180-d446-11eb-9806-a3aacd8375a7.png)
![image](https://user-images.githubusercontent.com/70501926/123091470-02392c80-d447-11eb-876a-6247428cee41.png)
![image](https://user-images.githubusercontent.com/70501926/123091499-0cf3c180-d447-11eb-8887-12bd2dc1eb44.png)
![image](https://user-images.githubusercontent.com/70501926/123091527-167d2980-d447-11eb-8d7d-d9bedc928d4c.png)
![image](https://user-images.githubusercontent.com/70501926/123091655-3e6c8d00-d447-11eb-8265-23d8412dff88.png)

