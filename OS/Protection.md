# Protection

## Outline
+ Goals of Protection
+ Principles of Protection
+ Domain of Protection
+ Access Matrix
+ Implementation of Acess Matrix
+ Access Control
+ Revocation of Acess Rights
+ Capability-Based Systems
+ Language-Based Protection

## Objectives
+ Discuss the goals and principles of protection in a modern computer system
+ Explain how protection domains combined with an `access matrix` used to specify the `resources` a `process` may access
+ Examine capability and _language-based protection_ systems

## Goals of Protection
+ In one protection model, computer consists of a collection of objects, hardware or software
+ Each object has a unique name and can be accessed through a well-defined set of operations
+ Protection problem - ensure that each object is accessed correctly and only be those processes that are allowed to do so

## Principles of Protection
_Privilege: (n.) ข้อได้เปรียบ, เอกสิทธ์, สิทธิพิเศษ_<br>
_ในความหมายทางคอมคือ Permission ในการ perform action ต่าง ๆ เช่นสร้างไฟล์ อ่านไฟล์ ลบไฟล์ access device_
+ **Principle of least privilege** ให้แต่ละ users หรือ processes มี privilege แค่เท่าที่ใช้ (ให้น้อยที่สุด)
 + Programs, users and systems should be given just enough **privileges** to perform their tasks<br>
 เราควรจะให้ privilege ต่อ 1 user ให้น้อยที่สุด เพื่อป้องกันการ hack
 + Limits damage if entity has a bug, gets abused
 + Can be static (during life of system, during life of process)
 + Or dynamic (changed by process as needed) - **domain switching, privilege escalation**
 + "Need to know" a similar concept regarding access to data
+ Must cosider "grain" aspect (grain ระบุว่ากำหนดสิทธิมากน้อยแค่ไหน)<br>
[coarse-grained vs fine-grained](http://www.webfarmr.eu/2011/05/coarse-grained-vs-fine-grained-access-control-part-i/)<br>
<ul>
 <li>**Rough-grained (coarse)** privilege management easier, simpler, but least privilege now done in large chunks(chunk = ชิ้นหนา)
 <ul>
  <li>_coarse-grained access control will work on larger items_</li>
  <li>For example, traditional Unix processes either have abilities of the associated user, or root</li>
 </ul>
 <li>**Fine-grained** management more complex, more overhead, but more protective</li>
 <ul> 
  <li>_fine-grained access control will work on smaller items_</li>
  <li>File ACL lists, RBAC</li>
 </ul>
</ul>
```
Examples
 Coarse: Employees can open the door.
 Fine: Employees based in the US can open or close the door during office hours.
 Finer: Employees in the Engineering department and based in the US can open or close the door during office hours if they are assigned to an active project.
```
+ Domain can be user, process, procedure

##Domain Structure

![](https://github.com/pNagi/Lecture/blob/master/img/14_01_ThreeDomains.jpg)

####Access-right
form: < object-name, rights-set ><br>
= where _right-set_ is a subset of all valid operations that can be performed on the object
####Domain
= set of _access-rights_<br>
_Note that Domain = user-id_

##Domain Implementation (UNIX)
+ Domain = user-id
+ **Domain switch** accomplised via file system<br>
 **Domain switch** เปลี่ยน user ไปใช้อีก user
 + Each file has associated with it a domain bit (setuid bit)
 + When file is executed and setuid = on, then user-id is set to owner of the file being executed
 + When execution completes user-id is reset
+ **Domain switch** accomplished via passwords
 + `su` command temporarily switches to anothe user's domain when other domain's password provided<br>
   คำสั่ง `su` เป็นของ root เมื่อจะสั่งจึงทำงานด้วย root
+ **Domain switching** via commands
 + `sudo` command prefix executes specified command in another domain (if original domain has privilege or password given)

##Domain Implementation (MULTICS)
+ Let `Di` and `Dj` be any two domain rings
+ if `j < i` -> `Di` is subset of `Dj`

![](https://github.com/pNagi/Lecture/blob/master/img/14_02_MULTICS_Rings.jpg)

##Multics Benefits and Limits
+ Ring/hierachical structure proviced more than the basic kernel/user or root/normal user design
+ Fairly complex -> more overhead
+ But does not allow strict need-to-know
 + Object accessible in `Dj` but not in `Di`, then `j` must be < `i`
 + But then every segment accessible in `Di` also accessible in `Dj`

##Access Matrix
+ View protection as a matrix (access matrix)
+ Rows represent domain
+ Columns represent objects
+ **Access(i, j)** is the set of operations that a process excecuting in Domain[i] can invoke on Object[j]

###Access Matrix คือตารางที่อธิบาย protection state
+ Rows คือ` subjects` หรือ `domain`
 + ซึ่ง `subjects` คือ active entities เช่น (users, processes, etc.)
+ Column คือ `objects` ซึ่ง `objects` ในที่นี้แบ่งออกเป็นสองแบบ คือ
 1. Passive entity (not `subject`)
 2. Any entity acting passively (คืออาจเป็นพวก `subject` จากข้อบน)

`Subject`/`Object` | `o1` | ... | `om` | `s1` | ... | `sn`
---|---|---|---|---|---|---|---|---
`s1` | 
...|
`sn`|

+ Subjects `S` = {`s1`,...,`sn`}
+ Objects `O` = {`o1`,...,`om`}
+ Rights `R` ={`r1`,...,`rk`}
+ Entries `A[si , oj]` ⊆ `R`
+ `A[si, oj]` = {`rx`,...,`ry`} คือ `subject` `si` มี `rights` `rx`,...,`ry` ใช้กับ object `oj`

##Use of Access Matrix
+ If a process in Domain `Di` tries to do “op” on object `Oj`, then “op” must be in the access matrix
+ User who creates object can define access column for that object
+ Can be expanded to dynamic protection
 + Operations to add, delete access rights
 + Special access rights:
  <ul>
   <li>_owner of `Oi`_</li>
   <li>_copy op from `Oi` to `Oj` (denoted by `*`)_</li>
   <li>_control – `Di` can modify `Dj` access rights_</li>
   <li>_transfer – switch from domain `Di` to `Dj`_</li>
  </ul>
 + Copy and Owner applicable to an object
 + Control applicable to domain object
+ **Access matrix** design separates mechanism from policy
 + Mechanism
 <ul>
  <li>Operating system provides access-matrix + rules</li>
  <li>If ensures that the matrix is only manipulated by authorized agents and that rules are strictly enforced</li>
 </ul>
 + Policy
 <ul>
  <li>User dictates policy</li>
  <li>Who can access what object and in what mode</li>
 </ul>
+ But doesn’t solve the general confinement(การจำกัด) problem

##Implement of Access Matrix
_`access list` = <`domain`, `rights-set`>_<br>
_`capability list` = <`object`, `rights-set`>_<br>

+ Generally, a sparse matrix
+ Option 1 - Global Table
 + เก็บ ordered triples <`domain`, `object`, `right-set`> ใน table
 + เวลา `domain` จะสั่งคำสั่ง M บน `oj` มันก็จะไป search จาก table เพื่อหา <`di`, `oj`, `rk`>
 <ul>
  <li> โดยที่ M ต้องเป็นคำสั่งที่อยู่ใน set ของ `Rk`</li>
 </ul>
 + ข้อเสียคือ table จะใหญ่มาก ทำให้ main memory ไม่พอ
 + ข้อเสียอีกอย่างคือ รวมยาก (ในแง่ของ `object` นึงมีกี่ `domain` ที่สามารถเรียกอ่านได้)
+ Option 2 - Access lists for objects
 + แต่ละ column ถูกจัดให้เป็น `access list` ไปเลยสำหรับ 1 `object` (`object` เก็บ `access list`)
 + ใน 1 `object` เลย มี <`domain`, `rights-set`> define ไว้ว่ามี `domain` ไหนที่มี `access rights` สำหรับ `object` นี้บ้าง (`domain` ไหนไม่มีก็จะไม่เก็บ)
 + ข้อดีคือ Easily extended to contain default set -> If M ∈ default set, also allow access
+ Option 3 - Capability list for domains
 + คราวนี้สลับกันคือเป็น domain based คือ `domain` เป็นคนเก็บ `capability List`
 + `object` represented by its name or address เรียกว่า `capability`
 + สมมุติจะสั่ง คำสั่ง `M` บน `object` `oj` process ก็จะเรียกหา operation  ใน `capability list` ของ `domain` นั้น ๆ
  <ul>
   <li>คือถ้า `domain` ที่สั่งเป็นเจ้าของ `capability` ก็แสดงว่าสารมารถ access ได้</li>
  </ul>
 + `capability list` เกี่ยวข้องกับ `domain` ก็จริง แต่ตัว `domain` ไม่สามารถ `access` เข้าไปได้ (คือถ้าเข้าไปแก้ได้ มันก็แก้ให้ตัวเองมีสิทธิทำทุกอย่างได้ในระบบ)
  <ul>
   <li>เป็น protected object ที่ maintain โดย OS และ การ access แบบ indirect</li>
   <li>Like a "secure pointer"</li>
   <li>Idea can be extended up to applications</li>
  </ul>
+ Option 4 - Lock-key
 + แบบที่รวมทั้งสองอย่าง (เก็บทั้งสองแบบ `access-list` กับ `capability list`)
 + `object` เก็บ unique bit patterns list เรียกว่า **locks**
 + `domain` เก็บ unique bit patterns list เรียกว่า **keys**
 + `domain` จะสามารถ access ได้แค่ `object` ที่ `key` matches กับ `lock` ไว้แล้ว

##Comparison of Implementations
+ Many trade-offs to consider
 + แบบ Global table คือมัน simple แต่กิน memory
 + แบบ Access lists คือ ต้องมี `users`
  <ul>
   <li>จำกัดสิทธิของ `domain` ลำบาก เพราะ `rights` เก็บอยู่ที่ `object` ฝ่ายเดียว</li>
   <li>ต้องเช็คก่อนทุกครั้งว่าใครเป็นคน access เข้ามาที่ `object` พอมีหลาย `objects` และหลาย `access rights` เลยทำให้ช้ามาก</li>
  </ul>
 + แบบ Capability lists คือ บอกชัดเจนว่าสามารถ access ที่ไหนได้บ้าง
  <ul>
   <li>แต่ข้อเสียคือ ยกเลิก(revoke) capabilities ลำบาก</li>
  </ul>
 + แบบ Lock-key ข้อดีคือ effective and flexible, สามารถส่ง `key` จาก `domain` ไปอีก `domain` อย่างอิสระ และ revoke(ยกเลิก) ง่าย

#### Systems ส่วนใหญ่ใช้แบบ รวม access lists and capabilities
+ First access to an object -> access list searched
 + If allowed, capability created and attached to
process
 <ul>
  <li>Additional accesses need not be checked</li>
 </ul>
 + After last access, capability destroyed 4 Consider file system with ACLs per file

##Access Control
+ Protection can be applied to non-file resources
+ Oracle Solaris 10 provides **role- based access control (RBAC)** to implement least privilege<br>
 แบบนี้คือ permission จะขึ้นอยู่กับ role ไม่ใช่ตัวบุคคล<br>
 สมมุติ user คนนึงมี role เป็น admin ก็จะมีสิทธิเท่าที่ admin ทุกคนสามารถทำได้
 + **Privilege** is right to execute system call or use an option within a system call
 + Can be assigned to processes
 + Users assigned **roles** granting access to privileges and programs
 <ul>
 <li>Enable role via password to gain its privileges</li>
 </ul>
 + Similar to access matrix

##Revocation of Access Rights
+ Various options to remove the access right of a domain to an object
 + **Immediate vs. delayed**
 + **Selective vs. general**
 + **Partial vs. total**
 + **Temporary vs. permanent**
+ **Access List** – Delete access rights from access list
 + **Simple** – search access list and remove entry
 + **[Immediate]**, **[general or selective]**, **[total or partial]**, **[permanent or temporary]**
+ **Capability List** – Scheme required to locate capability in the system before capability can be revoked
 + **Reacquisition** – periodic delete, with require and denial if revoked
 + **Back-pointers** – set of pointers from each object to all capabilities of that object (Multics)
 + **Indirection** – capability points to global table entry which points to object – delete entry from global table, not selective (CAL)
 + **Keys** – unique bits associated with capability, generated when capability created
 <ul>
  <li>Master key associated with object, key matches master key for access</li>
  <li>Revocation – create new master key</li>
  <li>Policy decision of who can create and modify keys – object
owner or others?</li>

# Glossary
+ execute (vt.) ดำเนินการ กระทำการ ระหารชีวิต
+ invoke (vt.) ก่อให้เกิด วิงวอน
+ invoke on (phrv) อ้อนวอนให้มีบางสิ่งเกิดขึ้นกับ
+ confinement (n.) การจำกัด กักขัง
+ sparse (adj.) หร็อมแหร็ม บางตา มีน้อย ไม่มาก
