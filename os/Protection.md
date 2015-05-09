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
+ Guilding principle - **principle of least privilege**
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
+ Generally, a sparse matrix
+ Option 1 - Global Table
 + เก็บ ordered triples <`domain`, `object`, `right-set`> ใน table
 <ul>+  `A` requested คำสั่ง (operation) `oj` ที่ `domain` `di` โดยการ search จาก table เพื่อหา <`di`, `oj`, `rk`>
  <li> โดยที่ M ต้องเป็นคำสั่งที่อยู่ใน set ของ `Rk`</li>
 </ul>
 + ข้อเสียคือ table จะใหญ่มาก ทำให้ main memory ไม่พอ
 + ข้อเสียอีกอย่างคือ รวมยาก (ในแง่ของ `object` นึงมีกี่ `domain` ที่สามารถเรียกอ่านได้)
+ Option 2 - Access lists for objects
 + แต่ละ column


# Glossary
+ execute (vt.) ดำเนินการ กระทำการ ระหารชีวิต
+ invoke (vt.) ก่อให้เกิด วิงวอน
+ invoke on (phrv) อ้อนวอนให้มีบางสิ่งเกิดขึ้นกับ
+ confinement (n.) การจำกัด กักขัง
+ sparse (adj.) หร็อมแหร็ม บางตา มีน้อย ไม่มาก
