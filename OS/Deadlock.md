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
 + `resource` นึงสามารถถูกใช้โดย `process` ได้แค่ 1 `process`
 + only one `process` at a time can use a `resource`
+ **Hold and wait**
 + `process` hold `resource` ไว้แล้ว wait `resource` ตัวอื่น
 + a process holding at least one resource is waiting to acquire(ได้รับ) additional resources held by other process
+ **No preemption**(การจอง)
 + `resource` จะถูก release ได้ก็ต่อเมื่อ `process` ที่เป็นเจ้าของมันสั่งเท่านั้น (ซึ่งจะ release ก็ต่อเมื่อ tasks  ของ process  นั้น ๆ เสร็จ)
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
 + ถ้า tasks ที่ทำอยู่ request ไปที่ resources อื่นแล้วไม่ได้ให้บังคับคืนของเก่าทั้งหมด
4. Prevent Circular Wait
 + total ordering โดยกำหนดให้การขอ resource ต้องขอจากน้อยไปมากเท่านั้น
 + ถ้าต้องการตัวน้อย ให้ขอก่อน

### Deadlock Avoidance
จำลอง state

#####BASIC FACTS
+ if system in `safe state` = no deadlock
+ if system in `unsafe state` = possibility of deadlock
+ Avoidance = การันตีว่า system จะไม่เข้า `unsafe state`

####Avoidance Algorithms
1. Single instance (deadlock แน่ ๆ ถ้ามี cycle)
 + ใช้ resource-allocation graph
2. Multiple instances (ถ้ามี cycle อาจจะเกิด deadlock)
 + ใช้ Banker's algorithm

#####Resource-allocation graph Algorithm

//eiei

#####Banker's Algorithm
+ Multiple instances
+ Each process must a priori claim maximum use
+ When a process requests a resource it may have to wait
+ When a process gets all its resources it must return them in a finite amount of time

//eiei


####Detection
1. Single instance
 + ถ้าวาดกราฟแล้วมี cycle เป็น deadlock แน่ ๆ
2. Several instances
 + ใช้วิธีคล้าย ๆ Banker's Algorithm
 + วนจนแก้อะไรไม่ได้แล้วตัวที่ finish[i] เป็น false คือตัวที่ติด deadlock (มีหลายตัว)

####Recovery from Deadlock

##### Process Termination
+ Two basic approaches
 + ยกเลิก(ทำให้ล้มเหลว) all deadlocked processes
 + ยกเลิกทีละ process จนกว่า deadlock cycle จะหมด
+ วิธีการเลือก process ที่จะ abort(ยกเลิก)
 1. priority of the process
 2. how long process computed, และ จะเสร็จเมื่อไหร่
 3. จำนวน resources ที่ process ใช้อยู่
 4. จำนวน resources ที่เหลือที่จะทำให้ process complete
 5. how many processes will need to be terminated
 6. process มีการ interactive(มีการสื่อสารระหว่างกัน) หรือรวมกลุ่มกันอยู่หรือเปล่า

##### Resource Preemption
+ Selecting a victim - minimize cost
+ Rollback - return to some safe state, restart process for that state
+ Starvation - same process may always be picked as victim, include number of rollback in cost factor
