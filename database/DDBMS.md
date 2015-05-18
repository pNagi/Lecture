#Client-Server Processing, Parallel Database Processing and Distributed Databases
(ชื่อบท)

##Outline
+ Overview
+ Client-Server Database Architectures
+ Parallel Database Architectures
+ Architectures for Distributed Database Management Systems
+ Transparency for Distributed Database Processing
+ Distributed Database Processing

##Evolution of Distributed Processing and Distributed Data
+ Need to share resources across a network

###1970s
+ Main frames
  + Timesharing
  + Centralized resources
+ First computer networks

###1980s
+ PCs and workstations
+ Local networks (LAN)

###1990s
+ Client-Server computing
  + request to server
  + server performs request and communicates result to client

####Timesharing
![Timesharing](./img/db_ddbms-01.png)
####Simple Resource Sharing
![Remote Procedure Call](./img/db_ddbms-02.png)
####Client-Server Processing
![Client-Server](./img/db_ddbms-03.png)
####Distributed Processing and Data
![Client-Server approach](./img/db_ddbms-04.png)

##Motivation
###For Client-Server Processing
+ Flexibility
  <ul>
  ในแง่ที่ว่า ง่ายต่อการ ดูแลรักษาและปรับให้เข้ากับระบบ
  </ul>
+ Scalability
  <ul>
  support เวลาเปลี่ยน hardware หรือ software (ที่ capacity มีผลกับระบบ)
  </ul>
+ Interoperability
  <ul>
  ก็คือการทำงานร่วมกัน สามารถเชื่อมระบบสองอันเข้าหากันได้ เพื่อที่จะได้ exchange data หรือใช้ software ร่วมกันได้
  </ul>

###For Parallel Database Processing
(Multiple Processors อาจมีคอมหลายเครื่อง and Multiple Discs)
+ Scale up
  <ul>
  เพิ่มปริมาณงานที่ทำให้เสร็จได้
  </ul>
+ Speed up
  <ul>
  เพิ่มความเร็วในการทำงานแต่ละ Task (ก็คือลดเวลาที่ใช้ในแต่ละ Task)
  </ul>
+ Availability<br>
  <ul>
  เพิ่ม accessibility (ความสามารถในการเข้าถึง) ให้ระบบ
  <li>High available: downtime(เวลาที่เครื่องไม่ทำงาน) น้อย</li>
  <li>Fault-tolerant: ไม่มี downtime
  </ul>

###For Distributed Data
+ Data Control<br>
  <ul>
  จัดตำแหน่ง data ให้ match กับ organization's structure
  </ul>
+ Communication costs<br>
  <ul>
  จำตำแหน่ง data ให้ใกล้เคียงกับ data usage เพื่อลด Communication cost (เวลาที่สิ้นเปลืองไประหว่างที่ communicate) และเพื่อ improve performance
  </ul>
+ Reliability<br>
  <ul>
  ทำให้ data พร้อมใช้งาน(ว่าง)บ่อย ๆ ก็เลยก้อป data ไปไว้หลาย ๆ ที่ (site)
  </ul>

###Summary of Distributed Processing and Data
| Technology | Advantages | Disadvantages |
| :------------- | :------------- | :------------- |
| Client-Server Processing | Flexibility, Scalability, Interoperability | High complexity, high development cost, possible interoperability problems |
| Parallel Database Processing | Scale up, Speed up, Availability, Scalability for predictive performance improvements | Possible interoperability problems, high cost |
| Distributed Databases | Local control of data, improved performance, reduced communication costs, increased reliability | High complexity, additional security concerns |

##Client-Server Database Architectures
+ แบ่งเป็นสองฝั่งคือ Client กับ Server โดยมี  Network เป็นตัวเชื่อม
+ เป็นระบบแบบ ส่ง messages (request for service) โดยส่งระหว่าง clients กับ servers

###Design Issues
+ **Division of processing**<br>
  แบ่ง tasks ไปที่ clients and servers
+ **Process management**<br>
  ทำงานร่วมกันระหว่าง clients กับ servers (ส่ง messages)
+ **Middleware**<br>
  software for process management

###Tasks to Distributed
performed on client or remotely on a server
+ **Presentation**
  <ul>
  code to maintain graphical user interface
  </ul>
+ **Validation**
  <ul>
  code to ensure ว่า user inputs สอดคล้องกับ database
  </ul>
+ **Business logic**
  <ul>
  code to perform business function
  </ul>
+ **Workflow**
  <ul>
  code to ensure completion of business process
  </ul>
+ **Data Access**
  <ul>
  code to extract(สกัด) data to answer queries and modify database
  </ul>

![](./img/db_ddbms-05.png)
![](./img/db_ddbms-06.png)
![](./img/db_ddbms-07.png)

###Middleware -> Interoperability
+ A software component that performs **process management**
+ Allow clients and servers to exist on different platforms.
+ Allow servers to efficiently process messages from **a large number of clients**
+ Often located on **a dedicated computer**

ex. ODBC, JDBC

![](./img/db_ddbms-08.png)
![](./img/db_ddbms-09.png)

Middleware ช่วยให้ clients กับ servers ติดต่อกันได้แม้ไม่ได้ใช้ platform เดียวกัน

###Data Access Middleware
+ เป็นส่วนประสานงานระหว่าง relational กับ non relational data โดยใช้ SQL (ODBC,JDBC)
+ Requests to access data from a DBMS are sent to a data access driver rather than directly to the DBMS.
+ The data access driver converts the SQL statement into the SQL supported by the DBMS and then routes the request to the DBMS.
+ The data access driver adds another layer of overhead between an application and a DBMS.
 + However,the data access driver supports independence between an application and the proprietary SQL supported by a DBMS vendor.

####Two-Tier Architecture
####Three-Tier Architecture
+ Middleware Server
+ Application Server
####Multiplier Architecture

##Parallel DBMS
+ Uses a collection of resources (processors, disks, and memory) to perform work in parallel
+ Divide work among resources to achieve desired performance (scaleup and speedup) and availability.
+ Uses high speed network, operating system, and storage system
+ Purchase decision involves more than parallel DBMS

###Basic Architecture
###Distributed Database

##￼Distributed Database Architectures


##Summary
+ Utilizing distributed processing and data can significantly improve DBMS services but at the cost of new design challenges.
+ Client-server architectures provide alternatives among cost, complexity, and benefit levels.
+ Parallel database processing provides improved performance (speedup and scaleup) and availability.
+ Architectures for distributed DBMSs differ in the integration of the local databases and level of data independence.

##Glossary
###Relational Database
ฐานข้อมูลเชิงสัมพันธ์<br>
*ฐานข้อมูลแบบหนึ่งซึ่งประกอบด้วยตารางข้อมูลจำนวนมาก แต่ละตารางอาจใช้เก็บข้อมูลเกี่ยวกับเรื่องของคน สถานที่ เหตุการณ์ สิ่งต่างๆ หรือความสัมพันธ์ระหว่างเรื่องเหล่านี้ การเก็บข้อมูลเป็นตารางๆ นี้นอกจากมีลักษณะสอดคล้องกับการใช้งานข้อมูลในชีวิตประจำวันเช่น ตารางเดินรถไฟแล้ว ยังมีพื้นฐานหลัการมาจากคณิตศาสตร์ที่เรียกว่า ความสัมพันธ์ หรือ relations ด้วย*












.
