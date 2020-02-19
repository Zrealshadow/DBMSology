### 数据库论文阅读目录

该仓库将会介绍一些数据库领域的经典论文，包括SIGMOD、VLDB、ICDE、FAST、ATC中的best paper，分组了部分论文，根据自己的理解，可能不全面。对于一些比较老的基础文章，请参见仓库： https://github.com/JunpengCode/databaseology 。 pingcap总结： https://github.com/JunpengCode/awesome-database-learning
https://www.kawabangga.com/db
#### **论文介绍**

* Bloom Filter
2018 sigmod best paper，该论文出自andy pavlo的学生。andy在数据库方面有独特的见解。bloom filter在disk-oriented database management system中有特别
的作用：在内存快读判断一个key是否存在，这些key就是存储的磁盘上的数据本身。该结构存在两个主要问题：（1）bloom filter存在“one-side error”也就是说：if key
is present, then bloom filter returns true. 该命题的逆否命题是：如果bloom filter返回false，那么说明key一定不存在。（2）bloom filter只支持point query，
但是不支持range query。针对bloom filter存在的第一个问题，要从设计合适的hash function等角度入手解决，比较难。针对第二个问题，SuRF采用了FST数据结构解决了
不支持范围查询的问题，能够给出开区间[key, +inf）,[key1, key2], (-inf, +inf)上的range query问题。具体技术请参见原文：
SuRF: Practical Range Query Filtering with Fast Succinct Tries

* To BLOB or Not To BLOB: Large Object Storage in a Database or a Filesystem?
本文主要讲述对于Binary Lager OBject（BLOB）究竟应该存储在database中使用DBMS管理还是应该用Filesystem来管理，即究竟BLOB应该作为一个数据库record还是file？
文章支持当文件系统是NTFS，DBMS是SQL Server 2005时，当文件大小下雨256KB时，DBMS管理更加高效，当对象大于1MB时，采用filesystem管理更加高效。文章还提出数据库
设计者应该考虑加入文件系统的碎片整理过程。**注：现今，当我们在存储视频等比较大的文件时，尽量不要直接用BLOB存储在数据库中，而是应该用filesystem管理，在数据库中可用只存储文件链接。**
