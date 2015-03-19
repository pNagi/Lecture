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

#### System Model
+ System consists of resoueces
+ Resources type R1, R2, R3,...,Rm
 *CPU cycles, memory space, I/O devices*
+ Each resource type Ri has Wi instances(กรณี)
+ Each process utilizes a resource as follows:
 + **request**
 + **use**
 + **release**
 
#### Deadlock Characterization
Deadlock เกิดก็ต่อเมื่อ condition ต่อไปนี้เกิดขึ้นพร้อมกัน
+ **Mutual exclusion**
 only one process at a time can use a resource
+ **Hold and wait**
 a process holding at least one resource is waiting to acquire(ได้รับ) additional resources held by other process
+ **No preemption(การจอง)**
 a resource can be released only voluntarily(อย่างสมัครใจ) by the process holding it, after the process has completed its task
+ **Circular wait**
 สมมุติมี set of process {p0, p1, p2,...,pn}
 p0 รอ resource ที่ p1 ถืออยู่
 p1 รอ resource ที่ p2 ถืออยู่
 p2 รอ resource ที่ p3 ถืออยู่
 ...
 pn รอ resource ที่ p0 ถืออยู่
 **สรุปคือรอวนกันเป็นวงกลม**
