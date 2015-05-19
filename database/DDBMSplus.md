##Distributed DBMS (DDBMS)
*ระบบการจัดการฐานข้อมูลแบบกระจาย*

###มุมมองทาง Logical
+ มี 1 ฐานข้อมูล (single logical database)
+ ซึ่งแบ่งออกเป็น `fragments` ต่าง ๆ
+ โดย `fragments` นั้นจะถูกจัดเก็บลงในคอมเครื่องเดียวหรือหลายเครื่องก็ได้
+ แต่อยู่ภายใต้การควบคุมของแต่ละ DBMS
+ คอมแต่ละตัวจะมีการเชื่อมต่อสื่อสารกันแบบเครือข่าย
+ ซึ่งแต่ละ site หรือสาขาก็สามารถประมวลผลเองได้โดยอิสระ
+ และ แต่ละ user สามารถเรียกใช้บริการให้ประมวลผลหรือจัดเก็บช้อมูลลงสาขาตัวเองหรือสาขาอื่น ๆ ที่อยู่ในเครือข่ายได้

###มุมมองทาง Physical
+ มีการจัดเก็บข้อมูลอยู่ในฐานข้อมูลที่กระจายกันอยู่
+ กระจายอยู่ใน**คอมหลายเครื่อง**และ**คอมอยู่คนละที่**
+ แต่สามารถเชื่อมโยงกันได้ผ่านระบบเครือข่าย

###การใช้งาน
User เข้าใช้ผ่าน Application
+ สามารถตั้งให้ใช้ได้แต่ local(ใช้ข้อมูลจากสาขาตัวเอง) หรือแบบ global(ใช้ข้อมูลจากสาขาอื่น) ได้

###Concept
+ สรุปแล้ว DDBMS คือ software ที่ช่วยให้ user มองผ่าน(Transparent)ความเป็นจริงที่ว่าระบบข้างหลังนั้นยุ่งยากแค่ไหน
+ เพื่อที่ user จะได้ใช้งานได้แม้ไม่รู้ว่าระบบด้านหลังจัดเก็บแบบไหน

###Component
+ แต่ละสาขา (site) ไม่จำเป็นต้องมี local database เป็นของตัวเอง
ตามรูป
รูป

##Summary
###Distributed Database
คือระบบที่กระจายฐานข้อมูลไปยังที่ต่าง ๆ และ เชื่อมต่อกันผ่านระบบเครือข่าย

###DDBMS
software ที่จัดการระบบฐานข้อมูล และอำนวยความสะดวกให้ user


##จดส่วนสำคัญ
+ สิ่งที่ user เห็น คือ Single Logical Database

+ Local Database กับ Remote Database

+ A distributed database management system is then defined as the software system that permits the management of the DDBS and makes the distribution transparent to the users

##หลักการพื้นฐาน

1. มีความเป็นอิสระในการประมวลผล (Local Automomy)
2. ไม่มีระบบใดท่ีทําหน้าท่ีเป็นศูนย์กลางในการควบคุม (No reliance on a central site)
3. การทํางานเป็นไปอย่างต่อเนื่อง (Continuous Operation)
4. ความเป็นอสิระกับท่ีตั้ง (Location independence/transparency)
5. ความเป็นอิสระของการแตกกระจาย (Fragmentation independence/transparency)
6. การมองผ่านการเก็บซ้ํา (Replication transparency/ Replication independence)
7. การจัดการการสืบค้นแบบกระจาย (Distributed query processing)
8. การจัดการรายการเปลี่ยนแปลงแบบกระจาย (Distributed transaction management)
 + ใช้งานโปรโตคอลที่เรียกว่า “Two-phase commit”
9. เป็นอิสระกับเคร่ืองที่ใช้งาน(Hardware independence)
10. เป็นอิสระกับโปรแกรมระบบปฏิบัติการ(Operating system independence)
11. เป็นอิสระกับระบบเครือข่าย(Network independence)
12. เป็นอิสระกับระบบจัดการฐานข้อมลู (DBMS independence)
