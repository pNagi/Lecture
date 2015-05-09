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
_Privilege: (n.) ข้อได้เปรียบ, เอกสิทธ์, สิทธิพิเศษ_
_ในความหมายทางคอมคือ Permission ในการ perform action ต่าง ๆ เช่นสร้างไฟล์ อ่านไฟล์ ลบไฟล์ access device
+ Guilding principle - **principle of least privilege**
 + Programs, users and systems should be given just enough **privileges** to perform their tasks<br>
 เราควรจะให้ privilege ต่อ 1 user ให้น้อยที่สุด เพื่อป้องกันการ hack
 + Limits damage if entity has a bug, gets abused
 + Can be static (during life of system, during life of process)
 + Or dynamic (changed by process as needed) - **domain switching, privilege escalation**
 + "Need to know" a similar concept regarding access to data
+ Must cosider "grain" aspect (grain ระบุว่ากำหนดสิทธิมากน้อยแค่ไหน)
 + Rough-grained privilege management easier, simpler, nut least privilege now done in large chunks
  + For example, traditional Unix processes either have abilities of the associated user, or root
 + Fine-grained management more complex, more overhead, but more protective
  + File ACL lists, RBAC
+ Domain can be user, process, procedure

##Domain Structure
+ Access-right = <object-name, rights-set>
 where _right-set_ is a subset of all valid operations that can be performed on the object
+ Domain = set of access-rights

##Domain Implementation (UNIX)
+ Domain = user-id
+ Domain switch accomplised via file system
 Domain switch เปลี่ยน user ไปใช้อีก user
 + Each file has associated with it a domain bit (setuid bit)
 + When file is executed and setuid = on, then user-id is set to owner of the file being executed
 + When execution completes user-id is reset
+ Domain switch accomplished via passwords
 + `su` command temporarily switches to anothe user's domain when other domain's password provided
   คำสั่ง `su` เป็นของ root เมื่อจะสั่งจึงทำงานด้วย root
+ Domain switching via commands
 + `sudo` command prefix executes specified command in another domain (if original domain has privilege or password given)
