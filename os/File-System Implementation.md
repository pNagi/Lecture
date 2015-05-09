#File System Implementation

##Outline
+ File-System Structure
+ File-System Implementation n Directory Implementation
+ Allocation Methods
+ Free-Space Management
+ Efficiency and Performance n Recovery
+ NFS
+ Example: WAFL File System

##File-System Structure
+ File structure
 + Logical storage unit
 + Collection of related information
+ **File system** resides on secondary storage (disks)
 + Provided user interface to storage, _mapping logical to physical_
 + Provides efficient and convenient access to disk by allowing data to be stored, located retrieved easily
+ Disk provides in-place rewrite and random access
 + I/O transfers performed in **blocks** of **sectors** (usually 512 bytes)
+ **File control block** – storage structure consisting of information about a file
+ **Device driver** controls the physical device
+ File system organized into layers

##Layered File System

application programs<br>
  v<br>
logical file system<br>
  v<br>
file-organization module<br>
  v<br>
basic file system<br>
  v<br>
I/O control<br>
  v<br>
devices<br>

##File System Layers

####Device drivers
+ manage I/O devices at the I/O control layer
 + Given commands like “read drive1, cylinder 72, track 2, sector 10, into memory location 1060” outputs low-level hardware specific commands to hardware controller

####Basic file system
+ given command like “retrieve block 123” translates to device driver
+ Also manages memory buffers and caches (allocation, freeing, replacement)
 + Buffers hold data in transit
 + Caches hold frequently used data

####File organization module
+ understands files, logical address, and physical blocks
 + Translates logical block # to physical block #
 + Manages free space, disk allocation

####Logical file system
+ manages metadata information
 + Translates file name into file number, file handle, location by
maintaining file control blocks (**inodes** in UNIX)
 + Directory management
 + Protection

Layering useful for reducing complexity and redundancy, but adds overhead and can decrease performanceTranslates file name into file number, file handle, location by maintaining file control blocks (inodes in UNIX)
+ Logical layers can be implemented by any coding method according to OS designer

Many file systems, sometimes many within an operating system
+ Each with its own format (CD-ROM is ISO 9660; Unix has **UFS**, FFS; Windows has FAT, FAT32, NTFS as well as floppy, CD, DVD Blu-ray, Linux has more than 40 types, with **extended file system** ext2 and ext3 leading; plus distributed file systems, etc.)
+ New ones still arriving – ZFS, GoogleFS, Oracle ASM, FUSE

##File-System Implementation
+ We have system calls at the API level, but how do we implement their functions?
 + On-disk and in-memory structures
+ **Boot control block** contains info needed by system to boot OS
from that volume
 + Needed if volume contains OS, usually first block of volume
+ **Volume control block** (linux เรียก **superblock**, **master file table**) contains volume details
 + Total # of blocks, # of free blocks, block size, free block pointers or array
+ Directory structure organizes the files
 + Names and inode numbers, master file table
+ Per-file *File Control Block* (*FCB*) contains many details about the file
 + inode number, permissions, size, dates
 + NFTS stores into in master file table using relational DB
structures
