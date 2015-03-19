## Table of Content
+ System Model
+ Deadlock Characterization
+ Methods for Handling Deadlocks
+ Deadlock Prevention
+ Deadlock Avoidance
+ Deadlock Detection
+ Recovery from Deadlock

#### Objectives
+ To develop a description of deadlocks, which prevent sets of concurrent(ประจวบเหมาะ) processes from completing their tasks
+ To present a number of different methods for preventing or avoiding deadlocks in a computer system

### System Model
+ System consists of `resources`
+ `Resources type` R1, R2, R3,...,Rm
 + เช่น *CPU cycles, memory space, I/O devices*
+ Each `resource type` Ri has Wi `instances`
+ Each process utilizes a resource as follows:
 + **request**
 + **use**
 + **release**
 
### Deadlock Characterization
`Deadlock` เกิดก็ต่อเมื่อ condition ต่อไปนี้เกิดขึ้นพร้อมกัน
+ **Mutual exclusion**
 + only one process at a time can use a resource
+ **Hold and wait**
 + a process holding at least one resource is waiting to acquire(ได้รับ) additional resources held by other process
+ **No preemption**(การจอง)
 + a resource can be released only voluntarily(อย่างสมัครใจ) by the process holding it, after the process has completed its task
+ **Circular wait**
 + สมมุติมี set of process {p0, p1, p2,...,pn}
 + p0 รอ resource ที่ p1 ถืออยู่
 + p1 รอ resource ที่ p2 ถืออยู่
 + p2 รอ resource ที่ p3 ถืออยู่
 + ...
 + pn รอ resource ที่ p0 ถืออยู่
 + **สรุปคือรอวนกันเป็นวงกลม**

#### Resource-Allocation Graph

A set of vertices V and a set of edges E
+ V is partitioned in to two types:
 + P = {p1, p2, p3,...,pn}, set consists of all processes in the system
 + R = {r1, r2, r3,...,rn}, set consists of all resource types in the system
+ **request edge** - directed edge Pi->Rj
+ **assignment edge** - directed edge Rj->Pi

### Methods for Handling Deadlock
วิธีรับมือกับ deadlock
+ เมินมัน
 + สมมุติว่า deadlock ไม่มีทางเกิดขึ้น เพราะโอกาสเกิดขึ้นน้อยมาก (OS ส่วนใหญ่ใช้วิธีนี้เช่น UNIX)
+ Deadlock detection and recocery
 + ปล่อยมันเกิดไปแล้วค่อย Recover ทีหลัง
+ Make sure that system จะไม่ enter deadlock state
 + Deadlock prevention
 + Deadlock avoidance

### Deadlock Prevention
เนื่องจากการเกิด `deadlock` มี condition 4 แบบ เราเลยออกแบบ OS ให้ condition ขาดไปข้อนึงจะได้ไม่เกิด `deadlock`

1. No Mutual Exclusion
 + ไม่ล็อค resource
 + shared resources เช่น read-only files ที่ไม่ทำให้เกิด deadlock
2. ทำให้ไม่มี Hold and Wait
 + ไม่ให้ยืมถ้าไม่คืนของเก่า
 + ข้อเสีย คือ อาจทำให้เกิด `starvation`
3. Force Preemption
4. Prevent Circular Wait

### Deadlock Avoidance
จำลอง state

BASIC FACTS
+ if system in `safe state` = no deadlock
+ if system in `unsafe state` = possibility of deadlock
+ Avoidance = การันตีว่า system จะไม่เข้า `unsafe state`

Avoidance Algorithms
+ Single instance (deadlock แน่ ๆ ถ้ามี cycle)
 + ใช้ resource-allocation graph
+ Multiple instances (ถ้ามี cycle อาจจะเกิด deadlock)
 + ใช้ Banker's algorithm

#####Resource-allocation graph Algorithm

#####Banker's Algorithm
+ Multiple instances
+ Each process must a priori claim maximum use
+ When a process requests a resource it may have to wait
+ When a process gets all its resources it must return them in a finite amount of time

