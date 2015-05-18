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

![Timesharing](./img/db_ddbms-01.png)
![Remote Procedure Call](./img/db_ddbms-02.png)
![File Sharing](./img/db_ddbms-03.png)
![Client-Server](./img/db_ddbms-04.png)

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

แปะรูปที

###Middleware -> Interoperability
+ A software component that performs **process management**
+ Allow clients and servers to exist on different platforms.
+ Allow servers to efficiently process messages from **a large number of clients**
+ Often located on **a dedicated computer**

ex. ODBC, JDBC
แปะรูปที




















.
