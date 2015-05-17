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
+ **Volume control block** (linux เรียก **superblock**, windows เรียก **master file table**) contains volume details
 + Total # of blocks, # of free blocks, block size, free block pointers or array
 + เก็บทุกอย่างที่ file system ใช้เช่น มีไฟล์อะไรบ้าง ว่างกี่บล็อค
 + format = ลบ volume control block สร้างใหม่
 + ไม่ได้มีแค่บล็อคเดียว
+ Directory structure organizes the files
 + Names and inode numbers, master file table
+ Per-file *File Control Block* (*FCB*) contains many details about the file
 + inode number, permissions, size, dates
 + NFTS stores into in master file table using relational DB structures
 + เป็นส่วนหนึ่งของ volume

##In-Memory File System Structures

##Partitions and Mounting
+ แบ่ง partition
+ root partition
 + เช่น Drive C
 + drive ที่ลง OS ไว้
 + ถ้าใช้ windows อยู่ root ก็เป็นฝั่ง windows
 + ถ้า virtual root ตัวนอกก็ตัวนอก ตัวในก็ตัวใน มันมองจากมุมมมองของ OS ที่รันอยู่

+ Mount คือเอา partition ในเครื่องให้เห็นเป็น drive นึง
 + เปิดเข้ามาต้อง mount แน่นอน

#### ทำไมต้องแบ่ง Partition
1. เวลา format windows จะได้ไม่ต้อง format data
2. linux/windows แชร์ partition(ฟังไม่เข้าใจ)
3. ลง OS ใน partition เดียวกันไม่ได้

##Virtual File Systems
+ **Virtual File Systems** (**VFS**) on Unix provide an object-oriented way of implementing file systems
+ VFS allows the same system call interface (the API) to be used for different types of file systems
 + Separates file-system generic operations from implementation details
 + Implementation can be one of many file systems types, or network file system
<ul><li>Implements **vnodes** which hold inodes or network file details</li></ul>
 + Then dispatches operation to appropriate file system implementation routines

##Directory Implementation
+ **Linear list** of file names with pointer to the data blocks l Simple to program
 + เก็บแบบ array
 + ไม่มีใครใช้หรอกมันช้า
 + Time-consuming to execute
<ul><li>Linear search time</li>
<li>Could keep ordered alphabetically via linked list or use B+ tree</li></ul>
+ **Hash Table** – linear list with hash data structure
 + เก็บแบบ hash map
 + Decreases directory search time
 + Collisions – situations where two file names hash to the same location
 + Only good if entries are fixed size, or use chained-overflow method

##Allocation Methods
1. contiguous
 + เก็บเรียงกันต่อไปเรื่อย ๆ
2. extent
 + เก็บไฟล์เป็นช่วง ๆ
 + เกิด fragmentation คือมันห่างกัน ไม่ปะติดปะต่อกัน
 + จึงต้อง defrag
 + ปัญหาคือจะรู้ได้ไงว่าไฟล์ต่อไปอยู่ไหน
  <ol>
  1. วิธีแรกคือเก็บ link list ไปอันต่อไป
   <ul><li>ข้อเสียคือ ถ้าจะอ่านส่วนตรงกลางของไฟล์ ต้องไปวนตั้งแต่อันแรก กว่าจะถึงส่วนที่ต้องการ ก็ช้ามาก</li></ul>
  2. แบบ index
   <ul><li>ช้า เปลือง mem เพิ่มมา 1 ช่อง</li>
   <li>โดดมาปุ๊ป เจอปั๊ปไม่ต้องไปวนตั้งแต่อันแรก ข้อดีคือจะอ่านส่วนไหนของไฟล์ก็อ่ารได้เลย)</li></ul>
  </ol>

##หัวข้อไหนไม่รู้ Recovery, Scan disk
+ เวลาไฟดับ หลังเปิดเครื่องใหม่
+ Scan disk คือนั่งไล่หาว่า ไฟล์ไหนใน disk ไม่มีเจ้าของหรือเจ้าของไม่ตรงกัน (ปกติ master file จะรู้ตำแหน่งทั้งหมดของทุก file)
+ ถ้าไม่ scan disk file ที่ไม่มีเจ้าของก็จะอยู่ในนั้นต่อไป เรียกไม่ได้
+ แต่ถ้า scan แล้วมันจะสร้าง map ตั้งชื่อว่า lost file ไว้และให้เป็นเจ้าของ file นั้น(ที่ไม่มีเจ้าของ) แต่จะไม่เก็บอยู่ที่เดิม เพราะไม่รู้ว่าที่เดิมอยู่ที่ไหน

##Log Structured File Systems (Journal File-System)
+ เก็บ `log/journal` เอาไว้ทุกการกระทำ
+ จะเก็บ `log/journal` ไว้ก่อน แล้วพอทำเสร็จก็จะลบ `journal` ออก
+ ข้อดีคือ สมมุติไฟดับ
+ ถ้ายังไม่ได้ทำ เปิดมาใหม่ก็เจอ `journal` อยู่ ก็ทำตามที่ `journal` บอก ไฟล์ก็จะถูกแก้เป็นแบบใหม่
+ ต่อให้ทำเสร็จแล้ว แล้วไฟดับก่อนลบ `journal` ไฟล์ก็จะถูกแก้อีกครั้ง แต่ไม่เป็นปัญหา เพราะข้อมูลไม่ได้ผิดเพี้ยนอะไร
+ สมมุติสั่งหลายอย่าง
+ ทำไปครึ่งทางแล้วไฟดับ
+ ก็ไม่เป็นปัญหา เพราะเปิดมา `journal` ก็ยังอยู่ ไฟล์ก็แค่ถูกแก้ใหม่ กลายเป็น แบบใหม่ทั้งหมด ไม่ครึ่ง ๆ กลาง ๆ (เป็นข้อดีมาก ๆ)
+ แต่ถ้าไฟดับตอนกำลังเขียน `journal`
+ ให้ถือว่า `journal` พัง ก็ลบทิ้งไปเลย เพราะไฟล์ยังไม่ได้ถูกแก้ และไฟล์ก็จะได้ไม่ทำคำสั่งครึ่ง ๆ กลาง ๆ
+ ข้อดีมาก ๆ คือทำให้ไฟล์ ไม่ถูกแก้ครึ่ง ๆ กลาง ๆ แต่เป็นไฟล์เดิมไม่ก็ไฟล์ใหม่ที่ถูกแก้แล้วไปเลย

