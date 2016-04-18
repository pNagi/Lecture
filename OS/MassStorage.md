###Average I/O time
average access time = seek time + latency
= average access time + (Amount of Data/transfer rate) + controller overhead

Ex. 
+ Data 4KB
+ HDD 7200 rpm
+ seek time 5 ms
+ latency = 30 / 7200 = 0.00417 s
+ transfer rate 1 Gb/s
+ controller overhead 0.1 ms

_Note that capital 'B' is byte, small 'b' is bit_

= 5 ms + 4.17 ms + (4KB/(1Gb/s)) + 0.1 ms
= 9.27 ms + (4KB/(1Gb/s))
```
1 Gb   1 B    1         (1024)^3 B    1 KB
---- . --- = --- GB/s . ---------- . -----
1 s    8 b    8            1 GB      1024B
```
= 9.27 + 0.31 ms
= 9.58

#####umdown's law
ถ้าตรงไหนช้าสุด ก็ทำให้ตรงนั้นเร็วขึ้น

เพราะ Solid State ไม่ต้องเสียเวลา seek time + latency ก็เลยเร็วกว่า

###Solid state
+ เร็วกว่า
+ ทนกว่าในแง่ที่เอามาโยนเล่น
+ แต่ถ้าเขียนบ่อย ๆ จะพังเร็ว
