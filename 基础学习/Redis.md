# 一、基础篇
# 二、实战篇
## 导入项目
### 数据库导入
### 项目导入
修改application.yml里的相关配置
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683286212378-ab064439-1393-4bc2-a05a-701ce4132a93.png#averageHue=%23fcfbfb&clientId=ua1497e69-88ef-4&from=paste&height=603&id=u9bce135d&originHeight=603&originWidth=1891&originalType=binary&ratio=1&rotation=0&showTitle=false&size=101267&status=done&style=none&taskId=u6297bfe5-64f2-4998-8f8f-75385f32f1d&title=&width=1891)
### nginx导入
运行nginx.exe即可
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683286304840-e466ac72-1c39-4167-8136-b499e412d789.png#averageHue=%231c1c1c&clientId=ua1497e69-88ef-4&from=paste&height=510&id=u81364588&originHeight=510&originWidth=960&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11998&status=done&style=none&taskId=ub33e0fae-c8dc-45f0-ba23-a380d12e1ea&title=&width=960)
## 短信登录
 ![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683286966675-16087ca5-2f5f-464d-8f51-eed5f61f2e1f.png#averageHue=%23f1eeee&clientId=ua1497e69-88ef-4&from=paste&height=767&id=u00239dfb&originHeight=767&originWidth=1576&originalType=binary&ratio=1&rotation=0&showTitle=false&size=334791&status=done&style=none&taskId=ua2d497bd-983c-47ae-b7aa-e83b3c81255&title=&width=1576)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683287549775-1067e74c-b7c1-4bf2-ad61-0b96d6fa719e.png#averageHue=%23d8dad0&clientId=ua1497e69-88ef-4&from=paste&height=751&id=u19cc2f30&originHeight=751&originWidth=1593&originalType=binary&ratio=1&rotation=0&showTitle=false&size=501136&status=done&style=none&taskId=uabf315e3-56cb-4d7e-9d2b-ca65cdd08dd&title=&width=1593)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683288839448-1f18bdf2-4cdf-44e1-82f0-16bfb2eaed0a.png#averageHue=%23f2ebe9&clientId=ua1497e69-88ef-4&from=paste&height=674&id=u3e3a77b1&originHeight=674&originWidth=1126&originalType=binary&ratio=1&rotation=0&showTitle=false&size=188336&status=done&style=none&taskId=uebfcddc7-a4c7-477e-bb71-36704eef5a2&title=&width=1126)

# 三、高级篇
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681821165917-aa95d24f-a908-487f-8cd1-812b431ed22b.png#averageHue=%23f8eded&clientId=u99b2d76b-f83b-4&from=paste&height=339&id=uc0729b40&originHeight=670&originWidth=1612&originalType=binary&ratio=1&rotation=0&showTitle=false&size=235589&status=done&style=none&taskId=u1c8aee6a-1aa6-4e89-8ab8-ae399942e0c&title=&width=815)
## 1 分布式缓存
### Redis持久化
#### RDB
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681821434388-7dc387a0-2354-450e-b1c5-f72c433a90fd.png#averageHue=%2377a273&clientId=u99b2d76b-f83b-4&from=paste&height=663&id=ufc1c8603&originHeight=663&originWidth=1571&originalType=binary&ratio=1&rotation=0&showTitle=false&size=376753&status=done&style=none&taskId=u730c9d1f-cd38-4123-aa7f-a5a407c9f5a&title=&width=1571)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681821607135-31cc3b80-f08c-448e-a39b-4f7b0fa95d82.png#averageHue=%23799390&clientId=u99b2d76b-f83b-4&from=paste&height=620&id=u0f592aca&originHeight=620&originWidth=1478&originalType=binary&ratio=1&rotation=0&showTitle=false&size=297578&status=done&style=none&taskId=u12551b06-baed-4dbf-b119-f50bf4215d1&title=&width=1478)
#### 原理
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681822171819-0b1466d0-2e85-48c3-ac1d-20222a7a0bc2.png#averageHue=%23e9e9e4&clientId=u99b2d76b-f83b-4&from=paste&height=728&id=u261e6f73&originHeight=728&originWidth=1640&originalType=binary&ratio=1&rotation=0&showTitle=false&size=406721&status=done&style=none&taskId=u217e7717-b64c-4d40-a4f8-860e887997c&title=&width=1640)
在 Redis 中，bgsave 命令用于在后台异步执行 RDB 持久化操作，将当前内存中的数据快照保存到磁盘中，以便在 Redis 重启时恢复数据。
bgsave 命令的底层实现原理及细节如下：

1. 子进程的创建

当执行 bgsave 命令时，Redis 会先创建一个子进程，该子进程将负责执行 RDB 持久化操作。

2. 生成 RDB 文件

子进程通过调用 fork() 函数创建出与父进程相同的内存映像，然后通过遍历内存中的数据生成 RDB 文件。在生成 RDB 文件期间，Redis 会阻塞主线程的所有写操作，以确保 RDB 文件的一致性。

3. 文件的写入

子进程在生成 RDB 文件后，将该文件写入磁盘中。在写入期间，Redis 会阻塞主线程的所有写操作，以确保文件的完整性和一致性。

4. 结束操作

子进程在将 RDB 文件写入磁盘后，向主进程发送信号，通知主进程生成 RDB 文件操作已经完成。此时，Redis 将解除对写操作的阻塞，恢复正常的写入操作。
需要注意的是，bgsave 命令可能会对 Redis 的性能产生一定的影响。由于该命令会阻塞主线程的所有写操作，因此在 Redis 写入量较大的情况下，bgsave 命令可能会导致主线程阻塞时间过长，从而影响 Redis 的性能。因此，在实际生产环境中，应谨慎使用 bgsave 命令，避免对 Redis 的性能产生过大的影响。同时，也可以考虑使用 AOF 持久化方式，该方式可以在不影响写入性能的前提下，实现数据的持久化。

进程如何访问内存中的数据进程访问内存中的数据需要经过以下步骤：

1. 通过进程ID获取进程控制块（PCB），PCB中包含了该进程的地址空间信息；
2. 根据PCB中的地址空间信息，将进程的虚拟地址转换为物理地址；
3. 通过物理地址从内存中获取数据。

在实际的操作系统中，访问内存的过程是由硬件和操作系统内核共同完成的。具体来说，当进程进行内存访问时，硬件首先会将虚拟地址发送给操作系统内核，内核根据地址转换表（页表）将虚拟地址转换为物理地址，然后再将物理地址返回给硬件，硬件最终通过物理地址从内存中获取数据。这个过程涉及到了硬件的地址转换和操作系统内核的页表管理，是一个比较复杂的过程。
页表页表是计算机操作系统中一种用于实现虚拟内存的数据结构，它将虚拟内存地址映射到物理内存地址。在操作系统中，每个进程都有自己的地址空间，地址空间分为多个虚拟页面，每个页面大小通常为4KB或者更大。操作系统通过页表将虚拟内存地址映射到物理内存地址，使得进程可以访问到虚拟内存中的数据。页表通常包含一个页目录和若干个页表项，每个页表项存储了一个虚拟页面和对应的物理页面的映射关系。当进程访问一个虚拟内存地址时，操作系统会通过页表查询对应的物理内存地址，然后将数据从物理内存中读取或者写入到虚拟内存中。页表还可以通过页表项中的访问权限位来控制进程对虚拟内存的访问权限，从而保证系统的安全性。
#### AOF持久化
Redis在进行持久化时，由于两个RDB的过程中存在间隔，因此可能会导致数据的丢失。
##  ![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682659915604-a01744ae-553c-497b-a29a-0a458e9c86b1.png#averageHue=%23f8f0f0&clientId=u14fb91cc-0b08-4&from=paste&height=726&id=u77d1b973&originHeight=726&originWidth=1550&originalType=binary&ratio=1&rotation=0&showTitle=false&size=213106&status=done&style=none&taskId=u439a0862-65a5-4dfc-917a-a01157178e9&title=&width=1550)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682660219125-2e28747d-4a2a-440e-8ee1-ee0723cc2dd5.png#averageHue=%23b8c0b6&clientId=u14fb91cc-0b08-4&from=paste&height=788&id=u2300bec1&originHeight=788&originWidth=1441&originalType=binary&ratio=1&rotation=0&showTitle=false&size=470592&status=done&style=none&taskId=u1e2ce112-8cc6-4f3a-a2fb-966d7fefae7&title=&width=1441)
#### AOF VS RDB
AOF记录的是操作，RDB记录的是数据，因此AOF的文件要比RDB大很多（一个key对应一个数据，但是一个key可能对应多个操作，有些记录的操作是无意义的）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682662534343-b19f2b0b-2091-4fcb-b9eb-85a9eeb1ce65.png#averageHue=%23cbcbca&clientId=u14fb91cc-0b08-4&from=paste&height=651&id=u39445539&originHeight=651&originWidth=1549&originalType=binary&ratio=1&rotation=0&showTitle=false&size=336204&status=done&style=none&taskId=u17a6e29f-af8e-4bec-b5a0-3d7b94c1860&title=&width=1549)
### Redis主从
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682663265575-79a5803e-3267-4117-9402-3f6ee421f788.png#averageHue=%23f9f5f5&clientId=u14fb91cc-0b08-4&from=paste&height=778&id=ud571e134&originHeight=778&originWidth=1445&originalType=binary&ratio=1&rotation=0&showTitle=false&size=212174&status=done&style=none&taskId=uf64cc017-1162-4374-82fa-1df8b0160ab&title=&width=1445)
#### 数据同步原理
##### 全量同步

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682667007850-63c52991-b952-4932-8e4a-ebf9ac2ae318.png#averageHue=%23e8ecdd&clientId=ua385996a-4264-4&from=paste&height=773&id=u8b288754&originHeight=773&originWidth=1459&originalType=binary&ratio=1&rotation=0&showTitle=false&size=265104&status=done&style=none&taskId=ub826e47d-5fb1-4040-86ea-7fd1e0a524b&title=&width=1459)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682667139825-921d1564-2a29-417d-b047-2c13c72bba47.png#averageHue=%23f3f2f2&clientId=ua385996a-4264-4&from=paste&height=708&id=u622266a7&originHeight=708&originWidth=1590&originalType=binary&ratio=1&rotation=0&showTitle=false&size=336323&status=done&style=none&taskId=ua452e018-68ee-4a51-8fb1-2f529ee6cd1&title=&width=1590)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682667222880-8ddd538a-41ee-444f-8437-6cf640b4f1f3.png#averageHue=%23e7e9db&clientId=ua385996a-4264-4&from=paste&height=782&id=u42b50617&originHeight=782&originWidth=1506&originalType=binary&ratio=1&rotation=0&showTitle=false&size=263317&status=done&style=none&taskId=u910b3650-5b2f-4acc-87cb-13e652b4a7e&title=&width=1506)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682667337322-103490b6-11f0-4e65-a475-61dc7e020b98.png#averageHue=%23f6f4f4&clientId=ua385996a-4264-4&from=paste&height=590&id=uc657a55e&originHeight=590&originWidth=1492&originalType=binary&ratio=1&rotation=0&showTitle=false&size=222458&status=done&style=none&taskId=u35166521-18e8-4a20-bb79-421197e16c3&title=&width=1492)
##### 增量同步
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682667607554-6de5bf83-c93a-4dc5-927c-ba5305953bea.png#averageHue=%23eee1e0&clientId=ua385996a-4264-4&from=paste&height=783&id=uea41b3d9&originHeight=783&originWidth=1632&originalType=binary&ratio=1&rotation=0&showTitle=false&size=363378&status=done&style=none&taskId=u02f8256c-fb34-424e-85a5-498c9e7643b&title=&width=1632)
#### 优化
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682667748315-9b1a0a69-2b87-4377-9fbb-e95ce5111788.png#averageHue=%23f4eeed&clientId=ua385996a-4264-4&from=paste&height=788&id=u1426a4e5&originHeight=788&originWidth=1482&originalType=binary&ratio=1&rotation=0&showTitle=false&size=410056&status=done&style=none&taskId=u029b38f3-39a0-4388-a207-409009ec351&title=&width=1482)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682667803418-aed0624c-d497-4d0b-b2a5-7d182f883de2.png#averageHue=%23f4f2f2&clientId=ua385996a-4264-4&from=paste&height=704&id=u710d30f8&originHeight=704&originWidth=1423&originalType=binary&ratio=1&rotation=0&showTitle=false&size=277196&status=done&style=none&taskId=ufdd499d5-1c57-4cd0-b1da-95108a458be&title=&width=1423)
### Redis哨兵
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682668048423-7b3fe2b5-5eaf-4a49-9a43-9ec8cc923816.png#averageHue=%23faf7f7&clientId=ua385996a-4264-4&from=paste&height=526&id=u7bc0e55a&originHeight=526&originWidth=1597&originalType=binary&ratio=1&rotation=0&showTitle=false&size=117702&status=done&style=none&taskId=u2d2ac0b0-acc2-468f-a835-c5b0245b42f&title=&width=1597)
#### 哨兵的作用及原理
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682668198588-358a39a3-a103-43e4-bd85-6d536b51f676.png#averageHue=%23f4ebe7&clientId=ua385996a-4264-4&from=paste&height=777&id=u00509f15&originHeight=777&originWidth=1524&originalType=binary&ratio=1&rotation=0&showTitle=false&size=446468&status=done&style=none&taskId=uc835b191-7905-421b-8920-acc633e0167&title=&width=1524)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682668269662-e9dd6cf5-1b6e-4063-bc3f-d82da212daaf.png#averageHue=%23f5ece8&clientId=ua385996a-4264-4&from=paste&height=773&id=u89e86a4f&originHeight=773&originWidth=1528&originalType=binary&ratio=1&rotation=0&showTitle=false&size=403341&status=done&style=none&taskId=u851de79a-6658-478a-881a-bf859ceea49&title=&width=1528)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682668360148-e8369a90-bb8d-491a-80f1-a071751ce1ac.png#averageHue=%23f5f5f5&clientId=ua385996a-4264-4&from=paste&height=479&id=uee4992ea&originHeight=479&originWidth=1609&originalType=binary&ratio=1&rotation=0&showTitle=false&size=237065&status=done&style=none&taskId=u47af43c6-3440-46ca-b0c3-68b60e117cb&title=&width=1609)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682668435389-53081ccf-f0e9-4578-a1bb-73ed525abe4a.png#averageHue=%23f5f0ee&clientId=ua385996a-4264-4&from=paste&height=739&id=u1cc2b59a&originHeight=739&originWidth=1574&originalType=binary&ratio=1&rotation=0&showTitle=false&size=393955&status=done&style=none&taskId=u98858837-e7bf-41fb-9c6e-5dc54664208&title=&width=1574)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682669014568-4baa0171-2a91-4d9c-9851-f07c1cec65cd.png#averageHue=%23f6f4f4&clientId=ua385996a-4264-4&from=paste&height=725&id=uad5bac9a&originHeight=725&originWidth=1422&originalType=binary&ratio=1&rotation=0&showTitle=false&size=251069&status=done&style=none&taskId=u9cdccd96-ff70-49f8-99a1-3e8c25c4d7b&title=&width=1422)
### 
#### 搭建哨兵集群
### Redis分片集群
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682670245620-c17db0dc-96e5-43a5-85ed-4e072ae971c4.png#averageHue=%23f5f0ee&clientId=ua385996a-4264-4&from=paste&height=770&id=u3c867e81&originHeight=770&originWidth=1527&originalType=binary&ratio=1&rotation=0&showTitle=false&size=407572&status=done&style=none&taskId=u76d8e1a5-35c8-491f-89b1-9fe0e225774&title=&width=1527)
#### 散列插槽
 ![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682672383952-45973486-65ca-4189-ade7-e3d7fdfb8e3c.png#averageHue=%23dcdbdb&clientId=ua385996a-4264-4&from=paste&height=776&id=u86d53821&originHeight=776&originWidth=1609&originalType=binary&ratio=1&rotation=0&showTitle=false&size=497837&status=done&style=none&taskId=ubfa5d978-08c8-4db5-b13b-b17d9413ba3&title=&width=1609)
redis为什么将插槽和数据绑定？
当有master宕机时，可以将它的插槽转移到其他master上，数据跟着插槽走，就永远可以找到数据的位置
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682672349620-e2c60e07-37f9-4d66-84db-b30ae7595bc7.png#averageHue=%233f3e3b&clientId=ua385996a-4264-4&from=paste&height=489&id=u587d0edb&originHeight=489&originWidth=1168&originalType=binary&ratio=1&rotation=0&showTitle=false&size=251743&status=done&style=none&taskId=ubba903b0-de87-40f5-ad75-3d7cffd2ead&title=&width=1168)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682672517625-15c16b99-2738-49a4-8f89-60bea0965033.png#averageHue=%23f4f2f2&clientId=ua385996a-4264-4&from=paste&height=573&id=ua33ff48f&originHeight=573&originWidth=1524&originalType=binary&ratio=1&rotation=0&showTitle=false&size=213903&status=done&style=none&taskId=ub39a4f3b-452a-4808-ae10-1d79523cfd2&title=&width=1524)
#### 集群伸缩
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682672669625-cf3ae264-5f11-48c0-8b60-2fffcad7fa4e.png#averageHue=%23bbbaba&clientId=ua385996a-4264-4&from=paste&height=711&id=ub4be92f4&originHeight=711&originWidth=1415&originalType=binary&ratio=1&rotation=0&showTitle=false&size=335784&status=done&style=none&taskId=u4bcbfe4e-77c5-4fd1-8812-291427e2df6&title=&width=1415)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682672734214-0545f65c-d0f3-41e9-8182-929f0a79f737.png#averageHue=%23f7f6f6&clientId=ua385996a-4264-4&from=paste&height=350&id=u91547c20&originHeight=350&originWidth=1477&originalType=binary&ratio=1&rotation=0&showTitle=false&size=205032&status=done&style=none&taskId=u7694c5a4-089a-4649-bd38-0c952c5457b&title=&width=1477)
添加一个新的节点到集群后，默认该节点并没有分配插槽。因此需要从已经存在的结点中分配一部分插槽给新的节点
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682673068543-9f71d04a-8356-4ccd-b8dd-b6faeea03bcc.png#averageHue=%23343632&clientId=ua385996a-4264-4&from=paste&height=425&id=u6b5a551e&originHeight=425&originWidth=1857&originalType=binary&ratio=1&rotation=0&showTitle=false&size=791975&status=done&style=none&taskId=ucaa64682-15e2-42c8-aec3-470cb4c1ade&title=&width=1857)
执行reshared指令后
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682673136789-ed5ac028-90cb-4dc8-b210-1ef2185515b1.png#averageHue=%2330332e&clientId=ua385996a-4264-4&from=paste&height=406&id=u44c99ad7&originHeight=406&originWidth=1864&originalType=binary&ratio=1&rotation=0&showTitle=false&size=756133&status=done&style=none&taskId=u18161d3f-32f5-44df-8764-4b95bde65d0&title=&width=1864)
#### 故障转移
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682673284497-3103bd40-1c7d-4588-89c0-d36fee7a90fe.png#averageHue=%235d5d58&clientId=ua385996a-4264-4&from=paste&height=605&id=u1b7582bf&originHeight=605&originWidth=1543&originalType=binary&ratio=1&rotation=0&showTitle=false&size=838433&status=done&style=none&taskId=ua03a3007-60fc-47cf-a164-edda199b2d9&title=&width=1543)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683165332955-dc91a58a-5acc-4352-874a-ab765280cc0d.png#averageHue=%23f5f4f4&clientId=ubb294aae-6022-4&from=paste&height=778&id=u26022d32&originHeight=778&originWidth=1556&originalType=binary&ratio=1&rotation=0&showTitle=false&size=338458&status=done&style=none&taskId=u73169d9d-f721-43bd-8bc5-f7831a4d1dd&title=&width=1556)
#### RedisTemplate访问分片集群
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683166440108-af56618a-050f-4000-aa96-ab04a0cc4f8a.png#averageHue=%23f8f8f7&clientId=ubb294aae-6022-4&from=paste&height=709&id=u7953bf30&originHeight=709&originWidth=1408&originalType=binary&ratio=1&rotation=0&showTitle=false&size=226034&status=done&style=none&taskId=u6eccb898-be6e-4723-a3e4-adbadc7733c&title=&width=1408)
## 2 多级缓存
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683166910991-c961a619-8fdd-4322-94d9-cd48ec100824.png#averageHue=%23f9f7f7&clientId=ubb294aae-6022-4&from=paste&height=731&id=ub83f418b&originHeight=731&originWidth=1434&originalType=binary&ratio=1&rotation=0&showTitle=false&size=208746&status=done&style=none&taskId=u31572eab-4ca1-44a9-9cae-f84de7638cd&title=&width=1434)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683167222919-5936b5e0-19f6-4817-8de5-4b4992e20e4f.png#averageHue=%23f4f2f1&clientId=ubb294aae-6022-4&from=paste&height=748&id=u71554a6a&originHeight=748&originWidth=1634&originalType=binary&ratio=1&rotation=0&showTitle=false&size=306712&status=done&style=none&taskId=u2ca87391-0224-4ec1-a1ec-086692b51ca&title=&width=1634)
### JVM进程缓存
#### 导入案例
##### 安装MySQL
###### 1.1.准备目录
为了方便后期配置MySQL，我们先准备两个目录，用于挂载容器的数据和配置文件目录：
```shell
# 创建文件夹
mkdir mysql
# 进入mysql目录
cd mysql
```
###### 1.2.运行命令
进入mysql目录后，执行下面的Docker命令：
```shell
docker run \
 -p 3306:3306 \
 --name mysql \
 -v $PWD/conf:/etc/mysql/conf.d \
 -v $PWD/logs:/logs \
 -v $PWD/data:/var/lib/mysql \
 -e MYSQL_ROOT_PASSWORD=123 \
 --privileged \
 -d \
 mysql:5.7.25
```
###### 1.3.修改配置
在mysql/conf目录添加一个my.cnf文件，作为mysql的配置文件：
```shell
# 创建文件
vi conf/my.cnf
```
文件的内容如下：
```properties
[mysqld]
skip-name-resolve
character_set_server=utf8
datadir=/var/lib/mysql
server-id=1000
```
###### 1.4.重启
配置修改后，必须重启容器：
```shell
docker restart mysql
```
###### 1.5 连接
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683198774624-0a6d377d-ce5f-4e1d-86df-8acc2f6c0c95.png#averageHue=%23f9f9f9&clientId=ua1497e69-88ef-4&from=paste&height=667&id=ud0800318&originHeight=667&originWidth=563&originalType=binary&ratio=1&rotation=0&showTitle=false&size=20351&status=done&style=none&taskId=u31a325d8-d535-478c-b3cc-72e69b3083d&title=&width=563)
##### 导入SQL
接下来，利用Navicat客户端连接MySQL，然后导入课前资料提供的sql文件：
其中包含两张表：

- tb_item：商品表，包含商品的基本信息
- tb_item_stock：商品库存表，包含商品的库存信息

之所以将库存分离出来，是因为库存是更新比较频繁的信息，写操作较多。而其他信息修改的频率非常低。
#### 初识Caffeine
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683200200071-21ea6dcd-8ed6-4d0f-8ac6-5ab0803d2b14.png#averageHue=%23f2f2f2&clientId=ua1497e69-88ef-4&from=paste&height=576&id=uc8b8fe51&originHeight=576&originWidth=1549&originalType=binary&ratio=1&rotation=0&showTitle=false&size=287790&status=done&style=none&taskId=uae982e16-ad23-485c-a6d8-b8b9185144c&title=&width=1549)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683200248597-ccacdd8f-b78f-432d-8e7c-0ee9da9a3982.png#averageHue=%23f7f6f6&clientId=ua1497e69-88ef-4&from=paste&height=687&id=ufee3bcc8&originHeight=687&originWidth=1500&originalType=binary&ratio=1&rotation=0&showTitle=false&size=233026&status=done&style=none&taskId=ud691dec3-6765-4599-b38c-f4eaeab74b9&title=&width=1500)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683200376209-87a528fc-42f5-4f6d-9bc3-3d4ec5ce741e.png#averageHue=%23f1f4ef&clientId=ua1497e69-88ef-4&from=paste&height=718&id=u9f60194b&originHeight=718&originWidth=1349&originalType=binary&ratio=1&rotation=0&showTitle=false&size=283736&status=done&style=none&taskId=u0b7bf622-94d1-4653-b7db-a58f4d1370e&title=&width=1349)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683200582876-3ddd478a-6dc0-448a-bc18-984363247f61.png#averageHue=%23f3f3f3&clientId=ua1497e69-88ef-4&from=paste&height=658&id=uac29dd5b&originHeight=658&originWidth=1540&originalType=binary&ratio=1&rotation=0&showTitle=false&size=327811&status=done&style=none&taskId=u53760320-e6e5-4b2a-ae00-8a1e10c1c9c&title=&width=1540)
#### 实现进程缓存
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683201102457-cdf83830-add1-4163-9c06-0eaafd8fa788.png#averageHue=%23f3f2f2&clientId=ua1497e69-88ef-4&from=paste&height=413&id=ua32c5635&originHeight=413&originWidth=1272&originalType=binary&ratio=1&rotation=0&showTitle=false&size=175160&status=done&style=none&taskId=u7a5a132c-5452-43a2-91a5-72542ce5e30&title=&width=1272)

- 创建CaffeineConfig配置类

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683201091727-782d3da6-1247-4eb8-9f6e-e66c176a9e7d.png#averageHue=%23f1f5ef&clientId=ua1497e69-88ef-4&from=paste&height=899&id=u7cce68b2&originHeight=899&originWidth=1074&originalType=binary&ratio=1&rotation=0&showTitle=false&size=370447&status=done&style=none&taskId=u1a799775-3d9e-4ef8-8f38-80a9d762696&title=&width=1074)

- 注入

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683201177292-44c9744d-711a-4331-8eb9-c4fb1484544a.png#averageHue=%23ecf0ea&clientId=ua1497e69-88ef-4&from=paste&height=748&id=u390dc4ee&originHeight=748&originWidth=1273&originalType=binary&ratio=1&rotation=0&showTitle=false&size=385220&status=done&style=none&taskId=u26323b46-970b-479c-a2a0-9046cc84e79&title=&width=1273)

- 更改代码，先从本地缓存中读取，本地缓存没有再从数据库中读取

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683201251991-5b25b6c3-fbb9-4983-a22d-a4d64c00b193.png#averageHue=%23f1f6ee&clientId=ua1497e69-88ef-4&from=paste&height=233&id=u79678b35&originHeight=233&originWidth=888&originalType=binary&ratio=1&rotation=0&showTitle=false&size=107705&status=done&style=none&taskId=uc0d22fdf-7299-436d-b9af-90e4e18338a&title=&width=888)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683201304525-4c95e6ae-31bc-4d18-82f3-220452e3851c.png#averageHue=%23f0f5ed&clientId=ua1497e69-88ef-4&from=paste&height=236&id=uec38d369&originHeight=236&originWidth=933&originalType=binary&ratio=1&rotation=0&showTitle=false&size=134086&status=done&style=none&taskId=ubbe29a04-ce18-4aa0-9ecd-deec7cea835&title=&width=933)
### Lua语法
#### 初识Lua
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683269647460-32ccbd58-43dd-4894-9b3a-e844d54dae06.png#averageHue=%23f6f6f6&clientId=ua1497e69-88ef-4&from=paste&height=743&id=ucd6758dd&originHeight=743&originWidth=1529&originalType=binary&ratio=1&rotation=0&showTitle=false&size=335511&status=done&style=none&taskId=u44029b56-aa4c-4298-afc3-599d59701d8&title=&width=1529)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683269694288-c75525c4-4aa0-423e-98e1-ffe6fd4e3499.png#averageHue=%23eef0eb&clientId=ua1497e69-88ef-4&from=paste&height=639&id=u51241ec0&originHeight=639&originWidth=1210&originalType=binary&ratio=1&rotation=0&showTitle=false&size=173992&status=done&style=none&taskId=ue32338bb-43ae-4f78-a187-dca28533c15&title=&width=1210)
#### 数据类型
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683269871179-7c6ab598-8f04-4a8a-baf1-8076786072ef.png#averageHue=%23eee3e1&clientId=ua1497e69-88ef-4&from=paste&height=574&id=aJwhG&originHeight=574&originWidth=1572&originalType=binary&ratio=1&rotation=0&showTitle=false&size=246063&status=done&style=none&taskId=u5fdf40f0-9715-4a16-94eb-bcba61327c2&title=&width=1572)
#### 变量
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683270564110-eec3afd2-55ba-4320-ba99-d0dcf2c9c1de.png#averageHue=%23f2f4ef&clientId=ua1497e69-88ef-4&from=paste&height=662&id=u017408d9&originHeight=662&originWidth=1134&originalType=binary&ratio=1&rotation=0&showTitle=false&size=243165&status=done&style=none&taskId=ue5723c2c-67b4-4419-ba33-42798103583&title=&width=1134)
#### 循环
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683270679693-33d1474d-f4e3-48bd-b12a-61c824ae854e.png#averageHue=%23e7e7e2&clientId=ua1497e69-88ef-4&from=paste&height=624&id=u1f0c2161&originHeight=624&originWidth=1212&originalType=binary&ratio=1&rotation=0&showTitle=false&size=206168&status=done&style=none&taskId=u56776038-be5d-4810-99b6-df246a4e6ab&title=&width=1212)
#### 函数
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683270896229-215f8b0f-e2ad-4327-8f29-6b4612ba5c8e.png#averageHue=%23f2f4ef&clientId=ua1497e69-88ef-4&from=paste&height=501&id=u4aa6f6ae&originHeight=501&originWidth=1062&originalType=binary&ratio=1&rotation=0&showTitle=false&size=127327&status=done&style=none&taskId=u5a83a3a3-52df-4235-b34d-de358e0249e&title=&width=1062)
#### 条件控制
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683270984190-5eb3a942-e7a7-4f13-88fb-ddf953dcd385.png#averageHue=%23e2e2e1&clientId=ua1497e69-88ef-4&from=paste&height=681&id=udc67c2ed&originHeight=681&originWidth=1558&originalType=binary&ratio=1&rotation=0&showTitle=false&size=248552&status=done&style=none&taskId=u1961fc4f-577b-43e7-afa3-1f1ac864c87&title=&width=1558)
### 多级缓存
#### 安装OpenResty
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683271207453-4ea9262a-b871-43d2-bd58-a79aed34982b.png#averageHue=%23f5f5f5&clientId=ua1497e69-88ef-4&from=paste&height=709&id=ufab02c4c&originHeight=709&originWidth=1526&originalType=binary&ratio=1&rotation=0&showTitle=false&size=293471&status=done&style=none&taskId=uf3f33443-d5cb-4c0d-9f89-1eb84892880&title=&width=1526)
#### OpenResty快速入门
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683275001939-780817dc-89fc-459e-9966-1ffc7f1b3ee9.png#averageHue=%23b8c0a4&clientId=ua1497e69-88ef-4&from=paste&height=1045&id=u0dd688f4&originHeight=1045&originWidth=1874&originalType=binary&ratio=1&rotation=0&showTitle=false&size=754283&status=done&style=none&taskId=u3c233ab5-7dc1-48c2-bc16-d68d421c5a3&title=&width=1874)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683275100662-7f68071a-fd39-43db-a8ca-bdf10cac98b8.png#averageHue=%23e4e5e1&clientId=ua1497e69-88ef-4&from=paste&height=613&id=ud80ae15e&originHeight=613&originWidth=1203&originalType=binary&ratio=1&rotation=0&showTitle=false&size=275975&status=done&style=none&taskId=u246fa06a-18ee-4c54-b957-cd7618d9934&title=&width=1203)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683275662322-c940547d-3a51-471a-aa5a-8bd954aa521b.png#averageHue=%23e2d8d8&clientId=ua1497e69-88ef-4&from=paste&height=784&id=u8f24c1e7&originHeight=784&originWidth=1548&originalType=binary&ratio=1&rotation=0&showTitle=false&size=470702&status=done&style=none&taskId=u878c6c52-67a8-4520-81a3-40ef4f59fdb&title=&width=1548)
# 面试问题
## 1.缓存
缓存通常是由键值对（key-value pairs）组成的，其中键（key）通常表示请求的内容，值（value）则是查询结果或者数据。缓存的基本工作原理就是将请求和查询结果进行匹配，如果缓存中已经存在相同的请求，就直接从缓存中获取查询结果，而不是再次查询底层存储系统。
在实际应用中，缓存的键值对可能会有不同的形式，比如**在HTTP缓存中**，键通常是请求的URL地址，而值则是响应的内容。在**数据库缓存中**，键可以是查询语句，而值则是查询结果。在**Web应用程序中**，缓存键可以是用户ID、会话ID或者其他的请求参数，而缓存值可以是查询结果、页面片段、计算结果等。
需要注意的是，缓存中的键值对需要根据实际业务场景进行设计和管理。通常需要考虑缓存的命中率、缓存空间的利用率、缓存过期和失效等问题。同时，缓存的键值对也需要进行合理的清理和管理，避免缓存中存在过期或者无用的数据。
## 2.缓存穿透
缓存穿透指的是，在缓存中无法命中需要查询的数据，从而导致该查询请求穿透到底层的存储系统中，而且这个查询请求是恶意的或非常频繁的，导致存储系统的访问压力变得非常大，甚至瘫痪。造成缓存穿透的主要原因是查询的数据并不存在于缓存中，而且也不存在于底层的存储系统中。
缓存穿透可能对系统的性能和稳定性造成极大的影响，因此需要采取一些措施来防止和减轻缓存穿透的影响。常用的防止缓存穿透的方法有以下几种：

1. 增加缓存的命中率：可以使用一些策略来提高缓存的命中率，如数据预热、LRU等。这样可以减少查询数据时的缓存未命中率。
2. 在缓存中设置空对象：当查询的数据不存在时，将一个空对象设置到缓存中，这样下一次查询相同的数据就可以从缓存中获取空对象，而不需要查询底层存储系统。
3. 进行参数校验：对查询请求进行参数校验，过滤掉一些非法或恶意的查询请求，如参数为空或参数非法的请求。
4. 布隆过滤器：可以使用布隆过滤器对查询请求进行过滤，将一些不可能存在于数据中的查询请求过滤掉。
5. 限制并发请求数：可以设置一定的并发请求限制，防止恶意攻击导致系统瘫痪。
## 3.布隆过滤器如何对请求进行过滤
布隆过滤器可以用于对请求进行过滤，通常的步骤如下：

1. 创建一个空的布隆过滤器，并设置其容量和错误率。
2. 将所有需要过滤的数据（例如IP地址、URL地址等）通过哈希函数映射到布隆过滤器的位数组上，并将对应的位设置为1。
3. 当有请求到达时，将请求中的数据通过哈希函数映射到位数组上，并判断对应的位是否都为1。如果有任何一个位不为1，则说明该请求的数据一定不在过滤器中，可以直接拒绝该请求。
## 4.缓存雪崩
缓存雪崩指的是在缓存中大量数据同时失效或者过期，导致后续的请求都无法从缓存中获取数据，而需要重新从数据库或其他存储系统中获取数据，从而导致这些存储系统的压力骤增，甚至可能会导致系统崩溃的现象。
## 5. 有人把一个超级大的文件存redis，这有什么问题 ?
大key
