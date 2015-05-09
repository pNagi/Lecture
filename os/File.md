#File-System Interface

##Outline
+ File Concept
+ Access Methods
+ Disk and Directory Structure n File-System Mounting
+ File Sharing
+ Protection

##File Concept
+ Address space
+ Types:
 + Data
  <ul>
  <li>numeric</li>
  <li>character</li>
  <li>binary</li>
  </ul>
 + Program
+ Contents (เขียนโดยคนสร้าง)
 + Many types
  + Consider **text file**, **source file**, **executable file**
  
##File Attribites
+ **Name** - เป็น information เดียวที่ human-readable
+ **Identifier** - id กำหนดใน file system
+ **Type**
+ **Location** - pointer to file location
+ **Size**
+ **Protection** - {reading, writing, executing}
+ **Time**, **date**, and **user identification** - for protection, security, and using monitoring
+ other information

##File Operations
+ File is an **abstract data type**
+ `Create`
+ `Write` – at **write pointer** location
+ `Read` – at **read pointer** location
+ `Reposition within file` - seek
+ `Delete`
+ `Truncate` (vt. ตัดสั้น)
+ `Open(Fi)` – search the directory structure on disk for entry `Fi`, and move the content of entry to memory
+ `Close (Fi)` – move the content of entry `Fi` in memory to directory structure on disk

##Open Files
skip

##Open File Locking
+ จัดการโดย OS and file systems
 + คล้าย ๆ reader-writer locks
 + **Shared lock** ไว้อ่าน (สามารถเข้าใช้พร้อมกันได้ concurrently)
 + **Exclusive lock** ไว้เขียน<br>
 _อ่านเพิ่มเติมใน database เอานะ_
+ เป็นสื่อกลาง(mediates) ในการ access file
+ Mandatory or advisory:
 + **Mandatory** - access จะถูก denied กลับมาขึ้นอยู่กับสถานะของ locks **หลังจาก request ไปแล้ว**
 + **Advisory** - **เช็คสถานะก่อน** ค่อยคิดว่าจะทำไง
 
##File Types - Name, Extension
skip

##File Structure
+ None - sequence of words, bytes n Simple record structure
 + Lines
 + Fixed length
 + Variable length
+ Complex Structures
 + Formatted document
 + Relocatable load file
+ Can simulate last two with first method by inserting appropriate control characters
+ Who decides:
 + Operating system
 + Program
 
##Sequential-access File
(pic)

##Access Methods
skip

##Other Access Methods
skip

##Directory Structure
+ A collection of nodes containing information about all files<br>
(pic)<br>
Both the directory structure and the files reside on disk

##Disk Structure
+ Disk can be subdivided into **partitions**
+ Disks or partitions can be **RAID** protected against failure
+ Disk or partition can be used **raw** – without a file system, or **formatted** with a file system
+ Partitions also known as minidisks, slices
+ Entity containing file system known as a **volume**
+ Each volume containing file system also tracks that file system’s info in **device directory** or **volume table of contents**
+ As well as **general-purpose file systems** there are many **special-purpose file systems**, frequently all within the same operating system or computer

##A Typical File-system Organization
(pic)

##Types of File Systems
skip

##Operations Performed on Directory
+ Search for a file
+ Create a file
+ Delete a file
+ List a directory
+ Rename a file
+ Traverse the file system (แสดง output / print)

##Directory Organization
The directory is organized logically to obtain
+ Efficiency – locating a file quickly
+ Naming – convenient to users
 + Two users can have same name for different files
 + The same file can have several different names
+ Grouping – logical grouping of files by properties, (e.g., all Java programs, all games, ...)

###Single-Level Directory
skip

###Two-Level Directory
skip

###Tree-Structured Directories
skip

###Acyclic-Graph Directories
skip

###General Graph Directory
skip

##File System Mounting

##File Sharing
skip

##Protection
skip

###Access Lists and Groups
skip

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
