# 1JVM介绍
# 2 JVM内存结构
## 2.1 程序计数器
每个线程都有一个程序计数器，是线程私有的，就是一个指针, 指向方法区中的方法字节码：**用来存储指向一条指令的地址， 也即将要执行的下一条指令代码。**

- 它是一块很小的内存空间，几乎可以忽略不记。也是运行速度最快的存储区域。
- 在JVM规范中，每个线程都有它自己的程序计数器，是线程私有的，生命周期与线程的生命周期保持一致。
- 任何时间一个线程都只有一个方法在执行，也就是所谓的当前方法。程序计数器会存储当前线程正在执行的Java方法的JVM指令地址；或者，如果是在执行native方法，则是未指定值（undefned）。
- 它是程序控制流的指示器，分支、循环、跳转、异常处理、线程恢复等基础功能都需要依赖这个计数器来完成。字节码解释器工作时就是通过改变这个计数器的值来选取下一条需要执行的字节码指令。
- 它是唯一一个在Java虚拟机规范中没有规定任何outotMemoryError情况的区域。
### 存储内容
PC寄存器用来存储指向下一条指令的地址，也即将要执行的指令代码。由执行引擎读取下一条指令。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681474577229-d1980670-2b4b-4a0b-9b4b-2fcb474a4c74.png#averageHue=%23fbf9f9&clientId=u3922c752-6690-4&from=paste&height=844&id=ud29dc989&originHeight=844&originWidth=1845&originalType=binary&ratio=1&rotation=0&showTitle=false&size=484296&status=done&style=none&taskId=u748287ab-091f-43d0-8de2-45c7ea42f16&title=&width=1845)
什么是寄存器？寄存器（Registers）是计算机内部一种用来暂存指令、地址、数据等信息的高速存储设备，其存取速度比内存更快。寄存器通常是在CPU内部实现的，因此访问速度非常快。
计算机通常具有多种不同类型的寄存器，每种类型的寄存器都用于特定的目的。例如，CPU通用寄存器（General Purpose Registers）用于存储运算数据和运算结果，指针寄存器（Pointer Registers）用于存储内存地址，程序计数器（Program Counter）用于存储下一条要执行的指令地址等等。在程序执行过程中，CPU会频繁地将数据从内存加载到寄存器中进行运算，或将计算结果从寄存器中存回内存。这样可以大大加快程序的运行速度。
不同的计算机体系结构可能具有不同数量和类型的寄存器，并且它们的寄存器的命名、大小和作用也可能会有所不同。
## 2.2 虚拟机栈
### 2.2.1 定义
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681476307441-6a6d8f5a-15eb-4e17-b106-e9ef9abd4096.png#averageHue=%23fbfbfb&clientId=u3922c752-6690-4&from=paste&height=714&id=BBg6L&originHeight=714&originWidth=1403&originalType=binary&ratio=1&rotation=0&showTitle=false&size=309701&status=done&style=none&taskId=ud79588de-329f-4881-a114-e9bb83f872f&title=&width=1403)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681475795298-d20d3782-8458-4130-92d3-3381ef4c5630.png#averageHue=%23fafafa&clientId=u3922c752-6690-4&from=paste&height=685&id=ub3a4e52d&originHeight=685&originWidth=1176&originalType=binary&ratio=1&rotation=0&showTitle=false&size=247227&status=done&style=none&taskId=ud1ae7a7e-6738-4f8a-a020-96323e2573a&title=&width=1176)
#### 问题
#### 1、垃圾回收是否设计栈内存？
不涉及，在虚拟机栈中，每个方法执行都会被压入栈中，当方法执行结束后，该方法对应的栈帧就会从栈中弹出，因此不需要进行垃圾回收
#### 2、栈内存分配越大越好吗？
并不是。每个主机的物理内存是固定的，如果为每个栈分配的内存较大，那么该主机能同时运行的线程数就会变少。并且虚拟栈的内存更多影响到该进程能递归调用的方法个数，并不会提高程序的运行速度。
另外，一般情况下，不同的操作系统都默认为栈分配一定的初始内存，如下图所示：
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681477008010-62d18807-b4ad-4410-a9fa-2a65c381735b.png#averageHue=%23f9f9f8&clientId=u3922c752-6690-4&from=paste&height=545&id=ueff9116d&originHeight=545&originWidth=1226&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197230&status=done&style=none&taskId=u70381da1-35c7-4612-ac94-f4056339c1e&title=&width=1226)
#### 3、方法内的局部变量是否线程安全？
方法内的局部变量是线程私有的，不同的线程在执行时会在内存中开辟不同的虚拟栈空间，而当执行到某一方法时，该方法的栈帧会压入到栈内。不同的进程对应的方法的栈帧也不同，因此方法内的局部变量是各自独立的，即线程安全的。但是如果方法中的局部变量（引用型）逃离了该方法的作用域(作为返回值返回)，则外界可以对其进行修改，则此时就非线程安全。

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681476577806-4b65d758-accc-44bd-b077-5814346c04dd.png#averageHue=%23fdfcfa&clientId=u3922c752-6690-4&from=paste&height=294&id=u6dd85e76&originHeight=404&originWidth=666&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86753&status=done&style=none&taskId=u84ff7aca-ee86-4724-a6ff-a310d0f85de&title=&width=484)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681477580873-74b7276f-de5b-420b-bea4-cb48d777b0d2.png#averageHue=%23fdfcfb&clientId=u3922c752-6690-4&from=paste&height=497&id=uc16deeb5&originHeight=614&originWidth=958&originalType=binary&ratio=1&rotation=0&showTitle=false&size=211255&status=done&style=none&taskId=u39edf2f5-8525-4811-89f2-d4b954fcec3&title=&width=775)
### 2.2.2 栈内存溢出

- **栈帧过多导致的内存溢出**
   - 递归调用无终止条件

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681477935757-6cf5bd1c-cedd-42cd-98a2-c2229aedd3f7.png#averageHue=%23fcfcfa&clientId=u3922c752-6690-4&from=paste&height=400&id=ufc98a472&originHeight=486&originWidth=737&originalType=binary&ratio=1&rotation=0&showTitle=false&size=136059&status=done&style=none&taskId=u8508fb80-f668-48e8-ad7d-c80ea11609d&title=&width=606)

   - 两个类循环引用

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681478375104-76129363-5edd-4a61-8f3c-2613b096fe62.png#averageHue=%23fdfdfd&clientId=u3922c752-6690-4&from=paste&height=563&id=udee33e95&originHeight=822&originWidth=907&originalType=binary&ratio=1&rotation=0&showTitle=false&size=206117&status=done&style=none&taskId=u23eee03e-f463-41a5-b9d5-078c72f25cc&title=&width=621)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681478435247-f27d8a6a-629e-4bdd-b420-9bd496655606.png#averageHue=%23fcfcfa&clientId=u3922c752-6690-4&from=paste&height=468&id=u5e741a4e&originHeight=581&originWidth=1100&originalType=binary&ratio=1&rotation=0&showTitle=false&size=236127&status=done&style=none&taskId=u84f25016-8d70-40c1-a1f1-e03b7dcc0a6&title=&width=886)
解决办法：在员工类中加@JsonIgnore注解（转换时忽略dept属性）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681478489200-6380e269-5137-4e7e-8723-7b5ec426038d.png#averageHue=%23fdfdfd&clientId=u3922c752-6690-4&from=paste&height=468&id=udc85b872&originHeight=581&originWidth=1010&originalType=binary&ratio=1&rotation=0&showTitle=false&size=135095&status=done&style=none&taskId=u87d4253f-89e1-4e47-a85e-b82cdaa6919&title=&width=814)

- **栈帧过大导致的内存溢出**
### 2.2.3 线程运行诊断
**1、CPU占用过多**
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681478895539-636a33f7-bddf-4ca6-9a20-32ec56b979c9.png#averageHue=%23f9f9f8&clientId=u3922c752-6690-4&from=paste&height=299&id=ua4bcab4f&originHeight=299&originWidth=1103&originalType=binary&ratio=1&rotation=0&showTitle=false&size=170241&status=done&style=none&taskId=u4cc22aef-8330-4368-ab2a-e505182c251&title=&width=1103)

## 2.3 本地方法栈
Java中的方法存在一些局限性，因此需要通过一些本地方法(通常由c/c++编写)(native声明)来执行一些功能。而执行本地方法所需要的内存空间就在本地方法栈中。
## 2.4 堆
上述的程序计数器、虚拟机栈、本地方法栈都是线程私有的
 ![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681479503430-2aec12fa-7aa0-4e35-ab36-06a2c312a0b0.png#averageHue=%23fcfcfb&clientId=u3922c752-6690-4&from=paste&height=474&id=u00089819&originHeight=474&originWidth=1109&originalType=binary&ratio=1&rotation=0&showTitle=false&size=130461&status=done&style=none&taskId=u5ca82a96-c6a5-4fac-a110-8db193307c3&title=&width=1109) 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681479648031-f02da729-3817-4695-ab43-3ed1ff965571.png#averageHue=%23f5f0e0&clientId=u3922c752-6690-4&from=paste&height=97&id=ua36fb0ef&originHeight=97&originWidth=860&originalType=binary&ratio=1&rotation=0&showTitle=false&size=39724&status=done&style=none&taskId=u4513f44e-752c-4c8b-8f5b-16028826939&title=&width=860)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681479737913-65ff5639-8cba-4c0c-ab34-b0c34ed4b50d.png#averageHue=%23fcfcfb&clientId=u3922c752-6690-4&from=paste&height=479&id=u10857303&originHeight=479&originWidth=923&originalType=binary&ratio=1&rotation=0&showTitle=false&size=160867&status=done&style=none&taskId=u37c4c066-edd6-4b44-9690-154f2e642e1&title=&width=923)
### 堆内存诊断
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681556271646-824e98c1-721c-4f48-b45a-541bc0087c0f.png#averageHue=%23fbfbfb&clientId=u3922c752-6690-4&from=paste&height=475&id=u4e2a979b&originHeight=475&originWidth=1157&originalType=binary&ratio=1&rotation=0&showTitle=false&size=156386&status=done&style=none&taskId=u6362a70e-d961-4d10-b055-6ca61576ebc&title=&width=1157)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681556302190-d289ebe1-5ed6-48d2-8a49-f890ba34b6ae.png#averageHue=%23fcfcfb&clientId=u3922c752-6690-4&from=paste&height=246&id=u3bf5ec7e&originHeight=246&originWidth=778&originalType=binary&ratio=1&rotation=0&showTitle=false&size=75033&status=done&style=none&taskId=u5fc38bb3-a304-4d37-ad29-800b0b8ed4b&title=&width=778)
## 2.5 方法区
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681557710844-7a16d2a4-727d-4e55-8750-f4e275bc7a38.png#averageHue=%23f3f4f0&clientId=u3922c752-6690-4&from=paste&height=132&id=u3731e801&originHeight=132&originWidth=1020&originalType=binary&ratio=1&rotation=0&showTitle=false&size=163454&status=done&style=none&taskId=ufa8e575b-c0ce-4c4f-9d12-6137e41c139&title=&width=1020)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681557826747-ce1bd267-04a9-4ceb-a29c-fd0c6c45de0b.png#averageHue=%23f3f3ee&clientId=u3922c752-6690-4&from=paste&height=283&id=u72db7ef8&originHeight=283&originWidth=1060&originalType=binary&ratio=1&rotation=0&showTitle=false&size=345841&status=done&style=none&taskId=u3a541364-be93-45f5-b437-4694a682bfe&title=&width=1060)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681557851926-a3404d62-ff25-44fd-83a0-e19bddafa69d.png#averageHue=%23e8ebe7&clientId=u3922c752-6690-4&from=paste&height=103&id=u7cbd21f8&originHeight=103&originWidth=1057&originalType=binary&ratio=1&rotation=0&showTitle=false&size=107713&status=done&style=none&taskId=u26211b42-8a5b-42fe-b5ed-0f5b1b2f737&title=&width=1057) 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681558424025-ef2dbe52-22a2-4284-add5-1de2d248de11.png#averageHue=%23e1eabc&clientId=u3922c752-6690-4&from=paste&height=927&id=u9c14d59d&originHeight=927&originWidth=1403&originalType=binary&ratio=1&rotation=0&showTitle=false&size=256471&status=done&style=none&taskId=u91df1928-40ff-4a44-b1b5-b845499a4d1&title=&width=1403)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681618671144-9e5b828c-0b18-4475-921e-1264a2d0e7c9.png#averageHue=%23fdfbfd&clientId=u3922c752-6690-4&from=paste&height=781&id=u28be9675&originHeight=781&originWidth=1799&originalType=binary&ratio=1&rotation=0&showTitle=false&size=361050&status=done&style=none&taskId=u05a7c63e-a59c-47ef-82b3-8a304a6b5a8&title=&width=1799)
类的二进制字节码文件包含类的基本信息、常量池、类方法定义（包含虚拟机指令）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681619228657-e833f648-68d7-4579-9dd1-49923b5f9ad0.png#averageHue=%23fbf9f6&clientId=u3922c752-6690-4&from=paste&height=404&id=u179292a9&originHeight=404&originWidth=694&originalType=binary&ratio=1&rotation=0&showTitle=false&size=61861&status=done&style=none&taskId=u708d90d4-dcda-41de-b8fb-4b26600b7c7&title=&width=694)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681619296853-074a1969-f63f-4ffb-b501-a2045aeac595.png#averageHue=%23fcfaf9&clientId=u3922c752-6690-4&from=paste&height=640&id=uf5580edb&originHeight=640&originWidth=776&originalType=binary&ratio=1&rotation=0&showTitle=false&size=91012&status=done&style=none&taskId=u6389cdc2-7440-4d19-9f06-52fd6eb1227&title=&width=776)

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681619780902-7aa54aa8-5d65-4017-a5fb-7ba764f30cd4.png#averageHue=%23fdfcfb&clientId=ud4f31bb5-7f28-4&from=paste&height=574&id=uffabacc7&originHeight=574&originWidth=875&originalType=binary&ratio=1&rotation=0&showTitle=false&size=62891&status=done&style=none&taskId=u58d7af29-ae99-4e62-930a-b4e574ad045&title=&width=875)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681620125103-accf59d9-9b39-41d1-bc76-1eb4489a8fb0.png#averageHue=%23c9cfd6&clientId=ud4f31bb5-7f28-4&from=paste&height=167&id=u51255c27&originHeight=167&originWidth=1329&originalType=binary&ratio=1&rotation=0&showTitle=false&size=186656&status=done&style=none&taskId=uc05aad7c-028c-4d33-98f3-322a4c72bcc&title=&width=1329)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681620596575-9d29f132-4b08-47e3-9f66-d9d6a3fd53d2.png#averageHue=%23f2eee1&clientId=ud4f31bb5-7f28-4&from=paste&height=369&id=uab302b8a&originHeight=369&originWidth=1158&originalType=binary&ratio=1&rotation=0&showTitle=false&size=191992&status=done&style=none&taskId=u2cceb8e8-b014-41e3-a50d-8178c15e9af&title=&width=1158)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681620810417-d669767e-63c7-421d-89f7-528bb21f5a08.png#averageHue=%23f1ede0&clientId=ud4f31bb5-7f28-4&from=paste&height=350&id=u8ed007d3&originHeight=350&originWidth=1263&originalType=binary&ratio=1&rotation=0&showTitle=false&size=217603&status=done&style=none&taskId=u2b22f30b-0b19-4c2d-96cc-42139688198&title=&width=1263)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681620874594-ca77d88c-fb72-442d-995c-686f8d85f2be.png#averageHue=%23e0dbd3&clientId=ud4f31bb5-7f28-4&from=paste&height=537&id=u47ab168a&originHeight=537&originWidth=1448&originalType=binary&ratio=1&rotation=0&showTitle=false&size=279125&status=done&style=none&taskId=ub80005b8-81f1-4b71-8b26-07d9bca4017&title=&width=1448)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681621005294-94c9e6d5-f8a4-4108-9431-be42bb9f9981.png#averageHue=%23fdfdfc&clientId=ud4f31bb5-7f28-4&from=paste&height=76&id=uce64ebaa&originHeight=76&originWidth=753&originalType=binary&ratio=1&rotation=0&showTitle=false&size=18105&status=done&style=none&taskId=uc2d36b08-0d18-4e9c-a57b-4c0a7a54437&title=&width=753)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681621130531-35423390-8ad8-459d-9d39-42eefbd13734.png#averageHue=%23a9c7ab&clientId=ud4f31bb5-7f28-4&from=paste&height=29&id=u3fe042e6&originHeight=29&originWidth=883&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33620&status=done&style=none&taskId=u4e4ae3ca-8c4b-4a68-8432-a77214bb1ae&title=&width=883)
字符串延迟加载
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681621282037-cc8c5539-e404-4cc2-8039-d913fb731288.png#averageHue=%23fcfafc&clientId=ud4f31bb5-7f28-4&from=paste&height=431&id=u94f60289&originHeight=431&originWidth=1134&originalType=binary&ratio=1&rotation=0&showTitle=false&size=237291&status=done&style=none&taskId=ue3d6d20c-837d-42cb-be6c-43c35d7ed0c&title=&width=1134)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681621748524-1669ef6e-25f6-4f0e-a8f6-b6daddb4969a.png#averageHue=%23f2efe2&clientId=ud4f31bb5-7f28-4&from=paste&height=683&id=u8f606a75&originHeight=683&originWidth=1372&originalType=binary&ratio=1&rotation=0&showTitle=false&size=256581&status=done&style=none&taskId=u242ba16b-f589-4cda-a315-e7a3c375583&title=&width=1372)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681621919442-be04614b-06bb-4c2e-a20a-aafac9e76308.png#averageHue=%23fcfafd&clientId=ud4f31bb5-7f28-4&from=paste&height=665&id=udba25a2d&originHeight=665&originWidth=1366&originalType=binary&ratio=1&rotation=0&showTitle=false&size=428771&status=done&style=none&taskId=u514ffe18-05af-4dac-a352-7907f50e77e&title=&width=1366)
### StringTabel性能调优

- 调整桶个数(-XX:StringTableSize=桶个数)
   - 由于StringTable底层是哈希表实现，若哈希表的桶的个数比较多，则相对来说哈希表中存储的元素较为分散，哈希碰撞的几率就会减小，查找速度将变快
- 将字符串对象入池
   - 使用new关键字创建的字符串对象会被保存至堆中。如果在应用中将new出来的字符串（存在重复）保存在list中，那么在list被销毁前，堆中的string对象不会被垃圾回收，将一直存放在堆中。但如果将s.intern()返回的对象保存在list中，那么堆中重复的字符串就可以被垃圾回收掉。

StringTableStringTable是Java中的一个内部数据结构，用于存储字符串常量池中的字符串对象。在Java虚拟机中，每个字符串常量在内存中只有一份实例，这是通过在StringTable中维护一个字符串对象池来实现的。
当一个字符串被创建时，它会被添加到StringTable中。如果StringTable中已经存在相同内容的字符串对象，则直接返回这个对象的引用；否则，将新创建的字符串对象添加到StringTable中，并返回该对象的引用。
由于字符串常量池中的字符串对象是共享的，因此可以节省内存空间并提高性能。同时，StringTable还支持垃圾回收，可以在运行时动态地添加和删除字符串对象。
需要注意的是，Java中的字符串不仅可以使用字面量形式创建，还可以通过new关键字创建。通过new创建的字符串对象不会被添加到StringTable中，因为它们不属于字符串常量池。
s.intern()方法在Java中，字符串对象有两种创建方式：使用字面量形式创建和使用new关键字创建。使用字面量形式创建的字符串对象会被添加到字符串常量池中，而使用new关键字创建的字符串对象则不会。
String.intern()方法是一个Native方法，它的作用是在运行时将字符串对象添加到字符串常量池中，并返回常量池中该字符串对象的引用。如果字符串常量池中已经存在该字符串对象，则直接返回该对象在字符串常量池中的引用。
一般来说，使用String.intern()方法可以帮助优化字符串的内存占用，因为字符串常量池中的字符串对象是共享的，可以节省内存空间。但是，需要注意的是，过度使用String.intern()方法可能会导致内存占用过高，因为字符串常量池中的字符串对象不会被垃圾回收，直到应用程序退出或者字符串常量池被清空。
因此，建议只在需要使用字符串常量池中的字符串对象时才使用String.intern()方法，同时也需要注意避免不必要的内存消耗。
StringTabel底层实现在Java中，StringTable是一个哈希表，它用于存储字符串常量池中的字符串对象。每个哈希表的节点包含一个字符串对象和指向下一个节点的指针。
StringTable使用的哈希表是一种开放地址哈希表，也被称为线性探测哈希表。在Java 8中，StringTable的哈希表大小为1009，这是一个质数，因为质数可以更好地避免哈希冲突。
StringTable中的哈希表包含一个固定大小的桶数组，每个桶中存储了一个链表，链表中的节点包含了一个字符串对象和指向下一个节点的指针。当一个新的字符串对象被添加到StringTable时，首先通过哈希函数计算出该字符串在哈希表中的索引，然后在对应的桶中查找该字符串对象。如果该桶中已经存在了相同的字符串对象，则直接返回该对象的引用。否则，将该字符串对象添加到该桶的链表中，并返回该对象的引用。
当哈希表的装载因子达到一定阈值时，StringTable会自动扩容，将哈希表的大小增加一倍。在扩容时，StringTable会将旧的哈希表中的所有元素重新计算哈希值并插入到新的哈希表中。需要注意的是，StringTable扩容时可能会导致所有线程的执行暂停，因为线程需要等待StringTable扩容完成才能继续执行。
需要注意的是，不同的Java版本中，StringTable的哈希表实现可能会有所不同。在Java 9及以上版本中，StringTable的哈希表实现已经进行了优化，使用了一种称为红黑树的数据结构，用于存储哈希冲突比较多的桶中的元素。
哈希表的桶的个数对哈希表的影响哈希表的桶的个数（即桶数组的长度）会直接影响哈希表的性能和空间利用率。如果桶的个数太小，哈希冲突就会很频繁，导致查询和插入元素的时间复杂度变高，而如果桶的个数太多，又会浪费过多的空间。
通常情况下，桶的个数会被设置为一个质数，这样可以更好地避免哈希冲突。对于一个固定大小的哈希表而言，桶的个数越多，哈希冲突的概率就越小，但同时也会占用更多的空间；反之，桶的个数越少，占用的空间就越少，但哈希冲突的概率就会增加。
在哈希表的设计中，通常需要权衡时间和空间的消耗，根据具体的应用场景和数据集大小来选择合适的桶的个数。对于一个经过充分测试和优化的哈希表而言，通常可以达到较高的性能和较低的空间消耗。
## 2.6 直接内存
不属于JVM内存，属于操作系统内存
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681631950973-4937f9b9-b389-49db-8f48-e59c8f1fb5c9.png#averageHue=%23fefcfe&clientId=ud4f31bb5-7f28-4&from=paste&height=422&id=u56cefda2&originHeight=422&originWidth=1161&originalType=binary&ratio=1&rotation=0&showTitle=false&size=104275&status=done&style=none&taskId=ubb7c4568-fb56-47f5-ae90-2e3c24f7641&title=&width=1161)
### 不使用直接内存VS使用直接内存
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681632485846-f034c96b-009a-4d42-8176-67b5c141d049.png#averageHue=%23a3a8d6&clientId=ud4f31bb5-7f28-4&from=paste&height=518&id=u08a64de3&originHeight=701&originWidth=954&originalType=binary&ratio=1&rotation=0&showTitle=false&size=172878&status=done&style=none&taskId=ud65b89c7-6b7e-4ba9-aa12-404f3f029bf&title=&width=705)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681632473989-85410c7e-8f8e-40f5-91e5-e9f30653177c.png#averageHue=%23aaadd5&clientId=ud4f31bb5-7f28-4&from=paste&height=516&id=u7baca762&originHeight=735&originWidth=982&originalType=binary&ratio=1&rotation=0&showTitle=false&size=207571&status=done&style=none&taskId=u05561b5b-4d83-4f8b-b4f4-de4e4d12739&title=&width=690)
JVM不能直接操作计算机系统的硬件，因此在进行涉及到和计算机硬件进行交互的操作时，需要切换到内核态来执行相关操作。在不使用直接内存时，如果想要从磁盘中读入数据，首先需要将磁盘文件中的部分数据读入到系统内存，在将系统内存中的数据拷贝到堆内存中，这样对于文件的读写效率就会变低。但如果使用直接内存，那么将会在系统中开辟一个直接内存缓冲区，JVM可以直接访问该缓冲区的数据。
### 释放原理
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681635220439-5418e48a-e4ae-4534-bafc-0aa935b1ba7c.png#averageHue=%23dddbdd&clientId=ud4f31bb5-7f28-4&from=paste&height=277&id=ub6f1e60d&originHeight=277&originWidth=1316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=223290&status=done&style=none&taskId=u05b53fcd-dc43-444c-a95b-417056327ee&title=&width=1316)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681634868547-8a026a09-b8c2-4d18-91a5-f3e8797b61d9.png#averageHue=%23eee9dd&clientId=ud4f31bb5-7f28-4&from=paste&height=772&id=u6164d0fc&originHeight=772&originWidth=932&originalType=binary&ratio=1&rotation=0&showTitle=false&size=308516&status=done&style=none&taskId=u8e0883b1-702e-4e03-92d2-bcf49f21c34&title=&width=932)
Cleaner对象是一个虚引用类型对象，当this所指向的对象被回收时，就会调用Cleaner中的clean方法，而clean方法就会执行当前任务对象（即Deallocator对象）的run方法
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681634909196-7bf629cc-6b79-457d-b71d-5575120a150c.png#averageHue=%23f2f0e8&clientId=ud4f31bb5-7f28-4&from=paste&height=762&id=ud6d1a7ad&originHeight=762&originWidth=776&originalType=binary&ratio=1&rotation=0&showTitle=false&size=240832&status=done&style=none&taskId=u181691a1-22b6-4de0-9296-f8b28196518&title=&width=776)
### 禁用显示回收 
JVM调优参数：`-XX:+DisableExplicitGC`，即让代码中的System.gc()无效
那么该如何回收直接内存？

- 通过调用unsafe对象的freeMemory方法

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681635431832-87b73db6-1025-43c5-900b-f8bb6a68c808.png#averageHue=%23c6c8d6&clientId=ud4f31bb5-7f28-4&from=paste&height=408&id=u45d6c40a&originHeight=408&originWidth=853&originalType=binary&ratio=1&rotation=0&showTitle=false&size=158622&status=done&style=none&taskId=uee549233-ef1d-4acd-9e88-25caefb0d8e&title=&width=853)


直接内存直接内存是一种在JVM之外分配和管理的内存，它不受JVM的垃圾回收机制控制。它通常被用于需要高效的I/O操作和需要频繁分配和释放内存的情况下，如网络编程和大数据处理。与传统的Java堆内存相比，直接内存的分配和释放速度更快，但是也需要手动释放内存。在Java NIO中，ByteBuffer类提供了一种方便的方式来使用直接内存。直接内存的缺点是容易出现内存泄漏和内存溢出等问题，因为它没有受到JVM的自动管理。
NIO操作是什么NIO（New I/O）是Java的一种基于缓冲区（Buffer）和通道（Channel）的I/O操作方式，相对于传统的I/O操作（也称为BIO，Blocking I/O），具有更高的效率和更强的可扩展性。NIO主要通过以下几个类和接口实现：

- ByteBuffer，CharBuffer，ShortBuffer，IntBuffer，LongBuffer，FloatBuffer和DoubleBuffer等缓冲区类，用于存储数据；
- Channel和Selector等通道类，用于读取和写入数据；
- Charset和CharsetEncoder/CharsetDecoder等字符编码和解码类，用于字符集转换；
- Pipe和Pipe.SinkChannel/Pipe.SourceChannel等管道类，用于线程间的通信。
NIO和IO的异同点NIO（New I/O）和IO（传统I/O）都是Java中用于进行I/O操作的方式，它们的主要区别如下：

1. 非阻塞式：NIO中的通道和缓冲区支持非阻塞式读写操作，可以避免传统I/O操作中线程阻塞等待数据到达的情况，提高了系统的并发处理能力。
2. 选择器：NIO提供了Selector机制，可以注册多个通道，通过单个线程对这些通道进行轮询，实现多路复用的高效处理方式，从而减少线程数量，提高系统性能。
3. 缓冲区：NIO中的数据读取和写入都是通过缓冲区（Buffer）来完成的，而传统I/O则是直接从输入/输出流中读取或写入数据。使用缓冲区可以提高数据读写的效率，并可以避免频繁的系统调用。
4. 文件处理：NIO中的FileChannel类提供了更加灵活和高效的文件读写操作，而传统I/O中的文件读写则需要通过FileInputStream和FileOutputStream等类来实现。

总的来说，NIO提供了更加灵活和高效的I/O操作方式，适合处理高并发、大数据量、高性能等场景，但是需要更加深入的了解操作系统的底层原理和编程模型。传统I/O操作则更加简单易用，适合处理一些简单的I/O操作。
内存泄漏内存泄漏指的是在程序中，某些对象在不再需要时没有被及时地释放所占用的内存空间，从而导致系统的内存资源逐渐减少，最终导致程序性能下降、崩溃等问题。
内存泄漏通常是由于程序设计不良或者代码实现不规范等问题造成的。比如，一个对象被创建后，如果没有及时地调用其析构函数或者手动释放其占用的内存空间，就会造成内存泄漏。另外，如果某个对象的引用计数没有被正确地处理，也会导致内存泄漏的问题。
内存溢出内存溢出（Memory Overflow）是指在程序运行过程中，申请的内存超出了操作系统所能分配给该程序的内存空间限制，导致程序崩溃的问题。内存溢出通常也被称为“Out of Memory”（OOM）。
内存溢出通常是由于程序中存在内存泄漏、内存管理不当等原因导致的。在程序运行过程中，如果频繁地申请内存，而没有及时地释放已经使用过的内存，就会导致内存溢出。此外，如果程序中存在大量的对象、数组等，也容易导致内存溢出的问题。
内存泄漏和内存溢出的区别内存泄漏（Memory Leak）和内存溢出（Memory Overflow）都是与程序内存资源管理相关的问题，但两者是不同的概念。
内存泄漏指的是在程序运行过程中，申请的内存没有及时释放，导致该内存无法再次被使用，最终导致程序的内存资源被耗尽的问题。内存泄漏的原因通常是由于程序中存在未正确释放内存的代码，或者内存管理不当等。
与内存泄漏不同，内存溢出指的是在程序运行过程中，申请的内存超出了操作系统所能分配给该程序的内存空间限制，导致程序崩溃的问题。内存溢出通常是由于程序中存在内存泄漏、内存管理不当等原因导致的。
因此，内存泄漏和内存溢出都是与程序内存资源管理相关的问题，但两者的本质不同：内存泄漏是指申请的内存没有及时释放，而内存溢出是指申请的内存超出了操作系统所能分配给该程序的内存空间限制。
JVM中新生代 老年代是什么在Java虚拟机中，堆内存可以分为新生代（Young Generation）、老年代（Old Generation）和永久代（Perm Generation，JDK8之后被元空间Metaspace所取代）。
新生代是指刚刚被创建出来的对象所存放的区域，通常包括一个Eden空间和两个Survivor空间。新创建的对象首先会被放入Eden空间中，如果Eden空间中的内存已经满了，那么会触发一次垃圾回收（Minor GC），将Eden空间中的垃圾对象清除掉，并将存活的对象移动到Survivor空间中。当Survivor空间中的内存也已经满了，那么这些存活的对象就会被移到老年代中。
老年代是指已经存活了一段时间的对象所存放的区域，通常是由多次垃圾回收操作中存活下来的对象所组成。在老年代中的对象，通常具有较长的生命周期和较高的稳定性，所以在老年代中垃圾回收的频率较低，但是一旦老年代中的内存满了，那么就会触发一次Full GC（Full Garbage Collection），清理整个堆内存中的垃圾对象。
新生代和老年代在内存大小分配上是可以调节的，通过设置堆内存的大小，可以调整新生代和老年代的大小比例，以适应不同的应用场景和需求。通常情况下，新生代的内存空间较小，老年代的内存空间较大，这是因为新生代中的对象通常具有较短的生命周期，存活时间较短，而老年代中的对象则具有较长的生命周期，存活时间较长。
# 3 垃圾回收
## 3.1 如何判断对象可以回收
### 引用计数法
 若一个对象被引用，则让它的引用计数+1.若该对象的引用计数为0，则该对象将被回收
存在问题：循环引用。A对象引用B对象，B对象同时引用A对象，但A、B两个对象都没有再被引用，但引用次数为1，因此不能进行垃圾回收
Java不采用该方法
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681636742544-60a72b94-84fc-40dd-a794-bc909c1449fa.png#averageHue=%23949c9e&clientId=ud4f31bb5-7f28-4&from=paste&height=253&id=ued2d7432&originHeight=253&originWidth=594&originalType=binary&ratio=1&rotation=0&showTitle=false&size=39543&status=done&style=none&taskId=uf3eb6707-e9da-4706-88cb-7ccde4d33b9&title=&width=594)
### 可达性分析算法
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681636997190-53f0f943-becd-4b14-8853-a1407248e781.png#averageHue=%23f8f6f8&clientId=ud4f31bb5-7f28-4&from=paste&height=285&id=ua48d0e52&originHeight=285&originWidth=1229&originalType=binary&ratio=1&rotation=0&showTitle=false&size=195375&status=done&style=none&taskId=u6b2af393-70d8-4a9b-af87-ff8afd99aa3&title=&width=1229)
可达性分析算法可达性分析算法是JVM中用于垃圾回收的一种算法。它通过从GC Roots开始向下搜索，找到所有被引用的对象，而没有被引用的对象会被判定为垃圾对象并进行回收。
GC Roots是一组根对象的引用，包括虚拟机栈中引用的对象、方法区中静态属性引用的对象以及JNI引用的对象等。通过这些GC Roots，JVM可以找到所有被引用的对象，然后标记并保留这些对象，同时回收没有被引用的对象。
可达性分析算法是一种高效且可靠的垃圾回收算法，因为它可以准确地找到所有被引用的对象，并可以处理循环引用的情况。在JVM中，主流的垃圾回收器，如Serial、Parallel、CMS、G1等都使用了可达性分析算法来进行垃圾回收。
### 四种引用
在JVM中，引用是指在程序中用于访问对象的一种方式。JVM定义了四种不同的引用类型，用于描述对象与GC Roots之间的关系，它们分别是：

1. 强引用（Strong Reference）：
- 强引用是最常见的引用类型。当一个对象具有强引用时，垃圾回收器就不会回收该对象。
- 即使在内存不足的情况下，强引用的对象也不会被回收。
- 可以使用new操作符创建强引用对象。
2. 软引用（Soft Reference）：
- 软引用通常用于实现缓存功能。
- 当一个对象具有软引用时，在垃圾回收后，内存不足时会再次触发垃圾回收，回收软引用对象。
- 软引用可以通过java.lang.ref.SoftReference类创建。
- 可以配合引用队列来释放自身
- 使用步骤
   - 创建软引用对象：使用 **SoftReference** 类创建一个软引用对象。
   - 设置软引用对象关联的引用对象：将需要被软引用关联的对象作为参数传入软引用对象的构造函数。
   - 使用软引用对象：使用软引用对象获取关联的引用对象时，需要通过 **get()** 方法来获取，如果引用对象未被回收，则返回该引用对象；如果引用对象已经被回收，则返回 **null**。
   - 判断软引用对象是否被回收：可以使用 **isEnqueued()** 方法来判断软引用对象是否已经被加入到引用队列中，即是否已经被回收。
   - 对于需要在引用对象被回收后执行一些操作的情况，可以使用引用队列（Reference Queue）来实现：使用 **ReferenceQueue** 类创建一个引用队列对象，然后将软引用对象关联到该引用队列对象上，当软引用对象关联的引用对象被回收后，软引用对象就会被加入到引用队列中。可以使用 **poll()** 或者 **remove()** 方法从引用队列中获取已经被回收的软引用对象，并执行相关操作。
- 应用场景：
   - 当需要从网络读入大量图片资源并保存在list集合时，如果使用强引用可能会导致内存溢出。但使用弱引用则可以在内存不足的情况下释放掉一些图片资源
   - `-Xmx20m -XX:+PrintGCDetails -verbose:gc` 分配java堆大小为20M，并打印垃圾回收的详细参数
```java
public static void main(String[] args) throws IOException{
    List<byte[]> list = new ArrayList<>();
    for (int i = 0; i< 5; it+) {
        list.add(new byte[ 4MB])
    };
	System. in.read();
}
```
```java
public static void soft(){
    List<SoftReference<byte[]>> list = new ArrayList<>();
    for(int i=0;i<5;i++){
        SoftReference<byte[]> soft = new SoftReference(new byte[_4MB]);
        System.out.println(soft.get());
        list.add(soft);
        System.out.println(list.size());
    }
    System.out.println("ending...");
    for(SoftReference<byte[]> soft:list){
        System.out.println(soft.get());
    }

}
```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681786873679-338d27ab-64fa-4aab-81b8-8246991af071.png#averageHue=%23e0d9cf&clientId=ud4f31bb5-7f28-4&from=paste&height=546&id=uf73b5166&originHeight=546&originWidth=1778&originalType=binary&ratio=1&rotation=0&showTitle=false&size=436567&status=done&style=none&taskId=u3c1a8f93-01a5-43cb-ad84-687db8f8654&title=&width=1778)
上述代码在垃圾回收时，释放了软引用对象所关联的byte数组对象的资源，但软引用对象本身并没有被释放，因此可通过设置引用队列的方式来释放软引用对象本身
```java
public static void soft(){
    List<SoftReference<byte[]>> list = new ArrayList<>();
    ReferenceQueue<byte[]> rq = new ReferenceQueue<>();
    for(int i=0;i<5;i++){
        // 关联引用队列，当软引用所关联的byte[]被回收时，软引用会自己加入到queue中去
        SoftReference<byte[]> soft = new SoftReference(new byte[_4MB],rq);
        System.out.println(soft.get());
        list.add(soft);
        System.out.println(list.size());
    }
    Reference<? extends byte[]> poll = rq.poll();
    while(poll!=null){
        list.remove(poll);
        poll = rq.poll();
    }
    System.out.println("ending...");
    for(SoftReference<byte[]> soft:list){
        System.out.println(soft.get());
    }
}
```

3. 弱引用（Weak Reference）：
- 弱引用通常用于实现一些特定的场景，如观察者模式
- 仅有弱引用引用该对象时，当垃圾回收时不管内存空间是否充足，都会回收弱引用对象
- 弱引用可以通过java.lang.ref.WeakReference类创建。
- 可以配合引用队列来释放自身
```java
public static void soft(){
    List<WeakReference<byte[]>> list = new ArrayList<>();
    for(int i=0;i<5;i++){
        WeakReference<byte[]> soft = new WeakReference(new byte[_4MB]);
        System.out.println(soft.get());
        list.add(soft);
        System.out.println(list.size());
    }
    System.out.println("ending...");
    for(WeakReference<byte[]> soft:list){
        System.out.println(soft.get());
    }

}
```

4. 虚引用（Phantom Reference）：
- 虚引用通常用于管理本地堆外内存（Direct Memory）或者实现比较复杂的finalize方法。
- 当一个对象具有虚引用时，它已经无法被访问到了。
- 必须配合引用队列使用，主要配合ByteBuffer使用，当引用对象回收时，虚引用会进入入队，由ReferenceHandler线程调用虚引用相关方法直接释放内存。（参考Clean对象的Cleaner方法）
- 虚引用可以通过java.lang.ref.PhantomReference类创建。

5.终接器引用（FinalReference）

- 无需手动编码，但其内部配合引用队列使用，在垃圾回收时，终结器引用入队 (被引用对象暂时没有被回收)，再由 Finalizer 线程通过终结器引用找到被引用对象并调用它的 finalize 方法，第二次 GC 时才能回收被引用对象
- 在JVM的引用类型中，终结器引用（Finalizer Reference）是一种比较特殊的引用类型，它是虚引用（Phantom Reference）的一个子类。终结器引用用于保存即将被回收的对象的finalize()方法的引用。
- 当对象被GC回收时，如果对象覆盖了finalize()方法，那么垃圾回收器会将该对象加入到FQueue队列中，并启动一个低优先级的Finalizer线程来执行该对象的finalize()方法。在执行完该对象的finalize()方法后，如果该对象还没有被任何对象引用，那么它就会被回收。
- 终结器引用可以通过java.lang.ref.Finalizer类创建。虽然终结器引用可以在一定程度上控制finalize()方法的执行，但是由于finalize()方法的执行时机不确定，而且很容易出现死锁和性能问题，因此在实际开发中应该尽量避免使用finalize()方法和终结器引用。
## 3.2 垃圾回收算法
### 标记清除法
第一阶段：标记。从根结点出发遍历对象，对访问过的对象打上标记，表示该对象可达。
第二阶段：清除。**清除的过程将遍历堆中所有的对象，将没有标记的对象全部清除掉。**对那些没有标记的对象进行回收，这样使得不能利用的空间能够重新被利用。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681793927508-c0790789-14f5-4df5-b5e1-409afa3a415f.png#averageHue=%23d0d5cc&clientId=ud4f31bb5-7f28-4&from=paste&height=689&id=u8f4a2dc5&originHeight=800&originWidth=890&originalType=binary&ratio=1&rotation=0&showTitle=false&size=145766&status=done&style=none&taskId=ubbfa3f4d-a3d6-4187-8542-3e7a384f3b8&title=&width=767)
标记清除法会记录空闲内存的起始位置与终止位置，当下次为某个对象分配内存时，可以分配这些空闲内存的位置。但若需要比较多的内存空间（比如数组对象），这些零碎的内存空间可能不能满足要求数组空间分配的要求。
标记清除法有几个优点：

- 它能够及时回收垃圾对象，避免了内存泄漏；
- 它不需要移动存活对象，因此可以保持对象原始的内存位置；
- 同时，该算法相对简单，容易实现。

但是，标记清除法也存在一些缺点。其中最主要的是，它在执行清除操作后会留下许多不连续的内存碎片，这会降低内存分配的效率。此外，它还需要暂停整个应用程序的运行，因为它需要遍历整个堆内存，这可能会导致长时间的停顿和性能问题。
标记清除法：速度快，但会造成垃圾碎片
### 标记整理法
特点：速度慢，没有内存碎片
同样是标记和清除两个阶段，标记阶段同样是从根节点出发，遍历所有对象，为对象打上标记。但清除阶段时，在回收垃圾后会把存活的对象整理到内存的一端，从而减少了内存碎片，不过，标记整理算法的缺点是在整理存活对象的时候需要移动对象，这将会导致回收效率较慢。
标记整理算法主要适用于垃圾收集器的老年代回收，因为老年代中存活对象的比例比较高，垃圾对象的比例比较低，且内存空间比较大，标记整理算法可以更好地利用老年代的特点。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681798722017-b459c0b2-0a97-4c49-8d59-5f27b2bc4106.png#averageHue=%23dfe1d7&clientId=ud4f31bb5-7f28-4&from=paste&height=430&id=ufe3cb1d2&originHeight=668&originWidth=1423&originalType=binary&ratio=1&rotation=0&showTitle=false&size=232265&status=done&style=none&taskId=ua566f444-ce6b-4023-987a-ba2210f6c8c&title=&width=915)
### 复制
维护两个内存空间From和To，首先从根节点出发，遍历From中所有的对象，为其打上标记，其中被标记的对象复制到To中。将剩下的在From空间的待回收对象清空，然后交换From和To的位置
优点：没有内存碎片
缺点：需要占用双倍的内存空间
适用于新生代的垃圾回收，新生代中的垃圾对象较多，因此需要复制的对象较少，STW时间较短
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681799535055-29b05dd1-bc6b-468e-8dfa-bf374cae3df0.png#averageHue=%23efedc6&clientId=ud4f31bb5-7f28-4&from=paste&height=436&id=uef9796c5&originHeight=457&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=122944&status=done&style=none&taskId=u13416ec9-5245-4882-89bc-6997a96b606&title=&width=1145)
## 3.3 分代垃圾回收
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681799679569-55466810-5c43-4b1f-b9db-a17e784cf961.png#averageHue=%23e6e7e3&clientId=ud4f31bb5-7f28-4&from=paste&height=258&id=ue12e8152&originHeight=351&originWidth=1518&originalType=binary&ratio=1&rotation=0&showTitle=false&size=90445&status=done&style=none&taskId=u3db5004c-b020-49c5-ada7-235c913180f&title=&width=1117)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681800108745-7e3f356b-b42a-4727-8bff-075aeb4d3a57.png#averageHue=%23e8e7e3&clientId=ud4f31bb5-7f28-4&from=paste&height=249&id=ua59ff130&originHeight=336&originWidth=1504&originalType=binary&ratio=1&rotation=0&showTitle=false&size=94092&status=done&style=none&taskId=u5519dfed-d46b-4fd9-bdab-87bebb9b069&title=&width=1115)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681800415120-fa4b69f0-0947-4c24-8684-051819af8182.png#averageHue=%23eeeeea&clientId=ud4f31bb5-7f28-4&from=paste&height=254&id=u2f1a179b&originHeight=346&originWidth=1505&originalType=binary&ratio=1&rotation=0&showTitle=false&size=97915&status=done&style=none&taskId=ud27d0966-ada3-4c6f-9719-ee0ef3f01f8&title=&width=1103)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681800553145-9f3a4594-3f1e-4bbc-a5de-2ffa94400a91.png#averageHue=%23eef0f0&clientId=ud4f31bb5-7f28-4&from=paste&height=253&id=u63ef1354&originHeight=336&originWidth=1472&originalType=binary&ratio=1&rotation=0&showTitle=false&size=98623&status=done&style=none&taskId=u80898911-f67a-4e73-bcbb-957027735f0&title=&width=1109)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681801044882-c3a3c880-24fa-4b49-8d7d-487f0d8f8d7a.png#averageHue=%23abb0e8&clientId=ud4f31bb5-7f28-4&from=paste&height=615&id=u94dccc63&originHeight=746&originWidth=1339&originalType=binary&ratio=1&rotation=0&showTitle=false&size=434518&status=done&style=none&taskId=ud4c4726d-fdbf-4043-b2b4-8d8916bffee&title=&width=1103)

分代垃圾回收是一种将堆内存划分为不同年龄代的垃圾回收方法。在JVM中，堆内存被划分为年轻代、老年代和永久代（或元空间）。
年轻代中的对象大多数是短命的，所以采用了基于复制的垃圾回收算法。当年轻代的Eden区域满了之后，会触发一次垃圾回收，将存活的对象复制到另一个区域中（并将幸存的对象寿命+1），同时清空当前区域的所有对象。年轻代中的区域通常分为一个Eden区和两个Survivor区（From和To），新分配的对象都在Eden区中，经过一次垃圾回收后（Minor GC），存活的对象会被复制到To区中，并且将From区和To区交换角色。当下次Eden区的区域再次满了之后，会对Eden区及From区的对象进行标记回收。当新生代中的幸存区的对象的寿命超过某个阈值时会认为该对象比较有价值，因此会将该对象保存至老年代中。当新生代与老年代的垃圾回收都满了之后将会触发一次FullGC，回收新生代与老年代的内存空间。
minor gc会引发stop the world（暂停其他用户进程，让垃圾进程工作，垃圾进程工作完之后，其他用户进程恢复执行）
老年代中的对象一般存活时间比较长，采用标记-清除或标记-整理算法进行垃圾回收。
永久代或元空间中存放的是JVM自身的类、方法等元数据信息，不需要进行垃圾回收。在JDK8之后，永久代被元空间所取代，元空间使用的是本地内存而不是虚拟机内存。
### 相关VM参数
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681801106013-843b0e78-9a8a-4cd9-a0dc-4b5f31773bd5.png#averageHue=%23fdfbfd&clientId=ud4f31bb5-7f28-4&from=paste&height=622&id=u9d5f3a11&originHeight=622&originWidth=1325&originalType=binary&ratio=1&rotation=0&showTitle=false&size=315285&status=done&style=none&taskId=u1995ea8b-505b-4867-85b9-9ee299caaba&title=&width=1325)
### 大对象
当为堆分配了一个需要占内存比较高的大对象时（该大对象所需内存超过新生代能够保存数据的内存），那么会将该大对象数据直接保存到老年代中，而不会触发垃圾回收
## 3.4 垃圾回收器
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681804234616-67aeca08-707d-4a85-be17-4bcffd16eee4.png#averageHue=%23fefcfe&clientId=ud4f31bb5-7f28-4&from=paste&height=598&id=u6570fa17&originHeight=598&originWidth=1199&originalType=binary&ratio=1&rotation=0&showTitle=false&size=177187&status=done&style=none&taskId=u8fa3cecd-d3bf-41c9-baeb-d406f9a9cfd&title=&width=1199)
吞吐量优先在垃圾回收的过程中，吞吐量优先是指系统能够完成垃圾回收的时间与系统总运行时间的比值，也就是垃圾回收所占用的时间与总时间的比值。如果垃圾回收所占用的时间较短，系统的吞吐量就会更高。吞吐量优先的垃圾回收器适合在后台运行，优化整体系统的吞吐量，但响应时间可能会受到一定的影响。
### 串行垃圾回收器
参数：`-XX:+UseSerialGC=Serial + SerialOld`
当执行垃圾回收线程时，其他的用户线程都会处于阻塞状态。另外由于在进行垃圾回收时，对象的引用地址可能发生改变，因此线程需要到安全点才能执行垃圾回收操作。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681804510416-1859440e-92e6-4d0e-896d-34e060382982.png#averageHue=%23b5ddc0&clientId=ud4f31bb5-7f28-4&from=paste&height=416&id=uc2a80ab0&originHeight=416&originWidth=1221&originalType=binary&ratio=1&rotation=0&showTitle=false&size=158658&status=done&style=none&taskId=u4d894c92-ea7d-41d2-ac59-ca818f73c1e&title=&width=1221)
### 吞吐量优先
`-XX:+UseParallelGC~-XX:+UseParallelOldGC `并行执行垃圾回收线程，在执行垃圾回收线程时，其他的用户进程将处于阻塞状态。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681805341606-1c913408-1181-4995-b319-eace0d853f63.png#averageHue=%23b1bae3&clientId=ud4f31bb5-7f28-4&from=paste&height=730&id=ue3b5a630&originHeight=730&originWidth=1385&originalType=binary&ratio=1&rotation=0&showTitle=false&size=307076&status=done&style=none&taskId=ue60bd333-74f7-4f76-b2ae-f23b9d106ba&title=&width=1385)
### 响应时间优先
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681807071982-f4183cc0-0395-4ff6-af01-38966ae4a8d6.png#averageHue=%23b7c2de&clientId=ud4f31bb5-7f28-4&from=paste&height=586&id=u759dd652&originHeight=586&originWidth=1261&originalType=binary&ratio=1&rotation=0&showTitle=false&size=381975&status=done&style=none&taskId=ud31b2680-97d7-4ff9-95d1-70e41246d62&title=&width=1261)
## 3.5 G1
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681813821710-d1ef2e48-3761-4a5b-a4a6-83d87d8678c6.png#averageHue=%23fefcfe&clientId=ud4f31bb5-7f28-4&from=paste&height=616&id=u6ef82ab2&originHeight=811&originWidth=1204&originalType=binary&ratio=1&rotation=0&showTitle=false&size=275979&status=done&style=none&taskId=u19a9e3f5-0493-40a6-bdb7-cb37cc1d6d7&title=&width=914)
### G1垃圾回收阶段
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681813957875-d94fa848-910e-4462-b7cf-e37401b91db7.png#averageHue=%23b4e6bf&clientId=ud4f31bb5-7f28-4&from=paste&height=407&id=u75e425d5&originHeight=677&originWidth=804&originalType=binary&ratio=1&rotation=0&showTitle=false&size=212600&status=done&style=none&taskId=u9cb5e877-d805-4258-902a-7f980a978d9&title=&width=483)
### Young Collection
会SWT
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681814129699-f08b5408-71c4-4ddc-8379-58293163db85.png#averageHue=%23addc8c&clientId=ud4f31bb5-7f28-4&from=paste&height=342&id=ubed474c9&originHeight=650&originWidth=858&originalType=binary&ratio=1&rotation=0&showTitle=false&size=89791&status=done&style=none&taskId=u5bec9bc0-6ef6-46fd-8e88-1eb7a348dd4&title=&width=451)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681814154077-7df4d491-8157-4067-b91e-09420d42d5ec.png#averageHue=%23acdb8c&clientId=ud4f31bb5-7f28-4&from=paste&height=343&id=u0535e281&originHeight=653&originWidth=846&originalType=binary&ratio=1&rotation=0&showTitle=false&size=95270&status=done&style=none&taskId=uc07f1d60-0894-4cf6-a3a6-fd7a25a4474&title=&width=445)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681814196906-8d67692a-0a56-4ee7-bf51-0cbdd47412c4.png#averageHue=%23addc8c&clientId=ud4f31bb5-7f28-4&from=paste&height=333&id=u2aedbd34&originHeight=634&originWidth=830&originalType=binary&ratio=1&rotation=0&showTitle=false&size=107917&status=done&style=none&taskId=ubc95af85-4abb-4865-a75e-45cdf54827d&title=&width=436) 
### Young Collection + CM
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681814503576-b89364a5-e259-4983-bd0f-db67b060a414.png#averageHue=%23cbd1d8&clientId=ud4f31bb5-7f28-4&from=paste&height=176&id=ua3635cab&originHeight=176&originWidth=1161&originalType=binary&ratio=1&rotation=0&showTitle=false&size=133625&status=done&style=none&taskId=u04971037-7ad0-4e20-a698-4b385efc639&title=&width=1161)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681814793960-9e6a2675-0b8e-4c00-8cc6-f705ef4ec404.png#averageHue=%23b2de94&clientId=ud4f31bb5-7f28-4&from=paste&height=402&id=u35a045ba&originHeight=626&originWidth=846&originalType=binary&ratio=1&rotation=0&showTitle=false&size=105396&status=done&style=none&taskId=ue17421f9-1948-4112-b913-92c7d84f705&title=&width=543)
### Mixed Collection
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681816345040-801250ff-1670-46ca-9be7-8efc620cfa47.png#averageHue=%23fcfafc&clientId=ud4f31bb5-7f28-4&from=paste&height=178&id=ue700d9e2&originHeight=245&originWidth=693&originalType=binary&ratio=1&rotation=0&showTitle=false&size=84245&status=done&style=none&taskId=u53d39841-beba-4f29-8b93-9c80acba8fa&title=&width=504)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681816326431-31fa04d1-9e08-4618-9593-d280ea6045a4.png#averageHue=%23b6e498&clientId=ud4f31bb5-7f28-4&from=paste&height=593&id=u3a046465&originHeight=702&originWidth=945&originalType=binary&ratio=1&rotation=0&showTitle=false&size=182187&status=done&style=none&taskId=u8161e9e9-3d10-4ac1-a591-6c1e0f98a49&title=&width=798)
G1垃圾回收器在执行Mixed Collection过程中，会使用一种混合式的垃圾回收算法。Mixed Collection主要分为以下几个步骤：

1. 初始标记（Initial Mark）：此阶段会标记根对象和直接关联到根对象的对象，并在对象头部添加标记位，标记这些对象为“存活”对象。
2. 并发标记（Concurrent Mark）：此阶段会从初始标记标记的对象出发，对整个堆空间进行标记。此阶段是与应用程序并发执行的，不会阻塞应用程序的执行。
3. 混合标记（Mixed GC）：此阶段会标记一部分区域的存活对象，为了保证系统的吞吐量，此阶段也是和应用程序并发执行的。此阶段的目的是为了缩小Full GC的范围。
4. 预清理（Cleanup）：此阶段会完成一些必要的清理工作，如回收Humongous对象和转移对象等。
5. 最终标记（Final Mark）：此阶段会标记混合标记阶段标记的所有存活对象。此阶段需要停止应用程序的执行，因为需要扫描整个堆空间。
6. 筛选回收（Live Data Counting and Evacuation）：此阶段会计算存活数据的数量，并将存活对象从旧区域复制到新区域。复制的时候，会优先复制存活对象数量少的区域。
7. 筛选放置（Remapping）：此阶段将新区域中的存活对象重新放置到旧区域。

G1的Mixed Collection过程可以看做是Young GC和Full GC的结合，将Full GC的工作量分摊到多个Mixed GC中，从而减少了Full GC的停顿时间和影响。同时，由于Mixed Collection的过程是可并行和可并发的，因此可以充分利用多核处理器和内存带宽，提高系统的吞吐量和性能。

### Full GC
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681816862782-807de851-1786-4506-b538-191ef1887c2c.png#averageHue=%23fdfbfd&clientId=ud4f31bb5-7f28-4&from=paste&height=406&id=uc047eadf&originHeight=664&originWidth=1217&originalType=binary&ratio=1&rotation=0&showTitle=false&size=259279&status=done&style=none&taskId=uaed6521b-85be-4a99-8f61-f933d24f972&title=&width=745)
### Young Collection跨代引用
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681980134644-00b58c31-8d08-4aed-aaa7-972c9af39690.png#averageHue=%23f0ece6&clientId=uead1733f-92eb-4&from=paste&height=365&id=u2bbcac39&originHeight=674&originWidth=1258&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197983&status=done&style=none&taskId=u668d4d96-710e-4f31-b9a3-119ce495ed3&title=&width=682)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681980230817-014f84b5-cddb-4459-b1ee-34e454c0a37e.png#averageHue=%23f3efec&clientId=uead1733f-92eb-4&from=paste&height=474&id=u05c929a6&originHeight=897&originWidth=1292&originalType=binary&ratio=1&rotation=0&showTitle=false&size=315545&status=done&style=none&taskId=uda2c37c3-7ad5-4e7e-8d5c-6d4836fa8c1&title=&width=683)
**新生代垃圾回收的过程：**
首先要找到根对象
然后对根对象进行可达性分析，找到存活对象
对存活对象进行复制，复制到幸存区
**产生问题：**
找到新生代对象的根对象，根对象有一部分是来自老年代的，而老年代存活的对象一般都特别多，如果去遍历整个老年代，效率非常低。
**应对措施：**
采用了cart table的方式，对老年代进行细分，分成了许多个card,每个card大约是512K。如果老年代某个对象，引用了新生代的对象，我们把这个老年代的对象标记为脏card。这样，找老年代的根对象时，就不用遍历整个老年代了，只需要关注脏card，减小搜索范围，提高效率。
老年代有脏卡标记，而新生代则有remembered  Set记录外部对它的引用，记录都有哪些脏卡。将来对新生代进行垃圾回收时，先通过remembered Set 知道有哪些脏卡，然后通过脏卡区域遍历GC Root。
### Remark
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681981736347-31ea91fb-2c52-482f-a3cc-5cd4e35d6f76.png#averageHue=%23efefef&clientId=uead1733f-92eb-4&from=paste&height=370&id=uc64f8a04&originHeight=513&originWidth=1134&originalType=binary&ratio=1&rotation=0&showTitle=false&size=92201&status=done&style=none&taskId=u5fe01ddf-8633-4dc2-a6b3-d67554febb4&title=&width=817)  
**** 情况一：**
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682420276829-78a5fc7f-bc86-40ad-a590-82501eed5a0a.png#averageHue=%23e0e0e0&clientId=u5500d316-9aa7-4&from=paste&height=290&id=u0bed9519&originHeight=467&originWidth=460&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42700&status=done&style=none&taskId=u886cad5c-1212-472d-b55c-f92764d4745&title=&width=286)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682420399283-69258051-5eca-433b-8e4d-b9cc46f9bc70.png#averageHue=%23dedede&clientId=u5500d316-9aa7-4&from=paste&height=286&id=ue5dc7d80&originHeight=462&originWidth=425&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36891&status=done&style=none&taskId=u9c951d94-8147-4d1e-b4fd-3b39bec5f38&title=&width=263)
**情况二：**
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682420276829-78a5fc7f-bc86-40ad-a590-82501eed5a0a.png#averageHue=%23e0e0e0&clientId=u5500d316-9aa7-4&from=paste&height=290&id=AHRBX&originHeight=467&originWidth=460&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42700&status=done&style=none&taskId=u886cad5c-1212-472d-b55c-f92764d4745&title=&width=286)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682420399283-69258051-5eca-433b-8e4d-b9cc46f9bc70.png#averageHue=%23dedede&clientId=u5500d316-9aa7-4&from=paste&height=286&id=dBGbD&originHeight=462&originWidth=425&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36891&status=done&style=none&taskId=u9c951d94-8147-4d1e-b4fd-3b39bec5f38&title=&width=263)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682420468216-d6c755f5-f5a2-40d0-bfe3-fc7c61f6656e.png#averageHue=%23dedede&clientId=u5500d316-9aa7-4&from=paste&height=284&id=ue5bb3536&originHeight=463&originWidth=425&originalType=binary&ratio=1&rotation=0&showTitle=false&size=41605&status=done&style=none&taskId=ufe4fafa3-3976-4121-8a8f-7b614de50b3&title=&width=261)
**Remark（重新标记）：解决情况二出现的问题**
当对象的引用被改变时，会为该对象加一个写屏障（只要对象的引用发生改变，写屏障的指令（把C加入到队列中，并且标记C为未处理状态）就会被执行）。在重新标记阶段，遍历队列中的对象，为对象重新打上标记。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682421318245-79485fbf-4d08-4669-89e9-e78acc2b14e8.png#averageHue=%23dcdcdc&clientId=u5500d316-9aa7-4&from=paste&height=468&id=u96393a74&originHeight=468&originWidth=391&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42186&status=done&style=none&taskId=uc45cc0dc-a5d5-4a61-8fde-7e0bfaf2bd4&title=&width=391)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682421267799-834831ef-40ee-4668-ac80-67801fc50045.png#averageHue=%23ededed&clientId=u5500d316-9aa7-4&from=paste&height=466&id=ua15e7533&originHeight=544&originWidth=893&originalType=binary&ratio=1&rotation=0&showTitle=false&size=71012&status=done&style=none&taskId=ufd8d6dde-b210-40b7-bbbd-898b800cec1&title=&width=765)
### JDK 8u20字符串去重
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682422460672-b91281d7-74c7-421e-957f-7868668bb3e7.png#averageHue=%23faf9f8&clientId=u5500d316-9aa7-4&from=paste&height=741&id=u0b2d9a63&originHeight=741&originWidth=1184&originalType=binary&ratio=1&rotation=0&showTitle=false&size=383053&status=done&style=none&taskId=ue5640dec-d98d-4fc8-933d-3a818c00308&title=&width=1184)
### JDK 8u40 并发标记类卸载
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682422778613-03ed053a-f505-4326-8f48-65fe31dc8140.png#averageHue=%23f2f1f0&clientId=u5500d316-9aa7-4&from=paste&height=185&id=u42328f09&originHeight=185&originWidth=1369&originalType=binary&ratio=1&rotation=0&showTitle=false&size=141676&status=done&style=none&taskId=ubabfe04e-be8d-46b6-8498-87c74b01e81&title=&width=1369)
类加载器类加载器（ClassLoader）是 Java 虚拟机（JVM）的一个重要组成部分，它负责加载 Java 类的字节码文件。在 Java 程序运行时，如果需要使用一个类，类加载器就会在其类路径下查找该类的字节码文件，如果找到了就加载到 JVM 中并创建该类的 Class 对象供程序使用。类加载器在 Java 程序的运行期间动态加载 Java 类，因此也被称为动态加载器。
Java 中的类加载器主要有三种类型：

1. 引导类加载器（Bootstrap ClassLoader）：也称为根加载器，它是 JVM 自身的一部分，用于加载 Java 核心库，如 java.lang 包中的类等。由于引导类加载器涉及 JVM 内部实现细节，因此不能在 Java 程序中直接获取其引用。
2. 扩展类加载器（Extension ClassLoader）：也称为系统扩展类加载器，它是用来加载 Java 的扩展库，如 $JAVA_HOME/lib/ext 目录下的类。
3. 应用程序类加载器（Application ClassLoader）：也称为系统类加载器，它负责加载应用程序的类，即 classpath 路径下的类。应用程序类加载器是最常用的类加载器。
### JDK 8u60 回收巨型对象
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682423151573-60b23f71-dd54-48f6-9dcd-60a10bf6418f.png#averageHue=%23efebe7&clientId=u5500d316-9aa7-4&from=paste&height=367&id=u6ff521c7&originHeight=689&originWidth=1238&originalType=binary&ratio=1&rotation=0&showTitle=false&size=255830&status=done&style=none&taskId=u16a9f204-1367-4a16-b261-7c4cd8cc9ff&title=&width=659)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682423230861-a2d5ea7c-b356-4a8b-b61f-d619af24e747.png#averageHue=%23f8f8f7&clientId=u5500d316-9aa7-4&from=paste&height=288&id=u20043fa2&originHeight=288&originWidth=1329&originalType=binary&ratio=1&rotation=0&showTitle=false&size=169037&status=done&style=none&taskId=uc1b12f52-04d4-41fa-8e12-20408224a96&title=&width=1329)
incoming引用incoming引用通常指的是对象内部的引用，用于指向其他对象。具体来说，如果一个对象A有一个incoming引用指向另一个对象B，则意味着A依赖于B，即A的状态和行为可能会受到B的影响。在垃圾回收过程中，为了判断一个对象是否可达，需要检查所有incoming引用，以确定对象是否还被其他对象引用，从而避免误判对象为垃圾而被回收。
### JDK9 并发标记起始时间调整
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682423883835-912f669a-3e45-4cd8-9049-876eae2ed905.png#averageHue=%23fbfaf9&clientId=u5500d316-9aa7-4&from=paste&height=361&id=u44ac8245&originHeight=361&originWidth=1296&originalType=binary&ratio=1&rotation=0&showTitle=false&size=196439&status=done&style=none&taskId=uacb1bced-2676-45ca-8468-a52a580c184&title=&width=1296)
## 3.6 垃圾回收调优
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682424588540-0660becd-9e64-4b80-908a-b518ccf50731.png#averageHue=%23fbfbfa&clientId=u5500d316-9aa7-4&from=paste&height=252&id=ucdc438d3&originHeight=252&originWidth=1235&originalType=binary&ratio=1&rotation=0&showTitle=false&size=111545&status=done&style=none&taskId=u3b63d812-3787-4c9a-ab78-65b50879054&title=&width=1235)
### 调优领域
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682424743106-1ff544ff-2381-43ed-9ff6-f3600cce5b63.png#averageHue=%23fdfdfd&clientId=u5500d316-9aa7-4&from=paste&height=222&id=u128a85f0&originHeight=222&originWidth=1068&originalType=binary&ratio=1&rotation=0&showTitle=false&size=23360&status=done&style=none&taskId=u27e8e7e3-4032-4476-aea8-8cdff9414d3&title=&width=1068)
### 确定目标
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682424790738-5b997dac-206c-4637-8f7e-07327103247b.png#averageHue=%23fbfbfb&clientId=u5500d316-9aa7-4&from=paste&height=163&id=ud4236a77&originHeight=163&originWidth=1207&originalType=binary&ratio=1&rotation=0&showTitle=false&size=60648&status=done&style=none&taskId=ue1623666-7b85-483e-bd4e-a45c8549f4f&title=&width=1207)
### 最快的GC是不发生GC
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682425157391-a1d73d8f-780d-439e-bdf3-b3b5f2c2fb3e.png#averageHue=%23fbfbfb&clientId=u5500d316-9aa7-4&from=paste&height=444&id=u5296ddcf&originHeight=602&originWidth=1069&originalType=binary&ratio=1&rotation=0&showTitle=false&size=194632&status=done&style=none&taskId=ub7c9995b-76e5-49eb-8d0c-a500d33809a&title=&width=788)
### 新生代调优
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682425633242-901b8ec5-eb87-4639-857f-d1aec2974f36.png#averageHue=%23faf9f9&clientId=u5500d316-9aa7-4&from=paste&height=328&id=u10e914d9&originHeight=328&originWidth=908&originalType=binary&ratio=1&rotation=0&showTitle=false&size=138751&status=done&style=none&taskId=ua143460d-f4c5-42d9-9eeb-741fb79d98e&title=&width=908)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682425822026-31b398ef-0f0b-4aba-a071-7bd400f28d03.png#averageHue=%23e6e0d8&clientId=u5500d316-9aa7-4&from=paste&height=319&id=u74c0cf27&originHeight=319&originWidth=1305&originalType=binary&ratio=1&rotation=0&showTitle=false&size=310914&status=done&style=none&taskId=u90cb467a-f968-439c-a9c9-bdd6d908ef4&title=&width=1305)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682426040510-575987d3-b722-4205-ba66-765c4fd1d3ee.png#averageHue=%23cac5bd&clientId=u5500d316-9aa7-4&from=paste&height=73&id=ud9623981&originHeight=73&originWidth=837&originalType=binary&ratio=1&rotation=0&showTitle=false&size=44283&status=done&style=none&taskId=uf01bd779-efd8-415d-8ec7-83d34c584b5&title=&width=837)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682426100760-fba7c178-517b-4d48-9874-bca375e620b5.png#averageHue=%23e1e1da&clientId=u5500d316-9aa7-4&from=paste&height=78&id=uce20fa5a&originHeight=78&originWidth=670&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45688&status=done&style=none&taskId=ue09b9cc3-55c7-44e8-afa9-443b6f1dab6&title=&width=670)
如果幸存区的空间设置过小，那么可能本来一些存活时间较短的对象会被晋升到老年代中(JVM自动调升阈值)，而这些存活时间较短的对象只能等到老年代垃圾回收时才能被回收掉，这延长了本该很早回收的对象在内存中的存活时间
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682426177767-fbef888d-c912-43d9-94a0-d09ce83c6aa6.png#averageHue=%23fcfbfb&clientId=u5500d316-9aa7-4&from=paste&height=413&id=ucc4dc4fe&originHeight=413&originWidth=1351&originalType=binary&ratio=1&rotation=0&showTitle=false&size=205185&status=done&style=none&taskId=u525953a1-0452-4139-bef4-2f370e0e1ef&title=&width=1351)
### 老年代调优
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682426609322-d04b9d0c-66fb-4723-ad61-adaafb55b358.png#averageHue=%23f6f6f5&clientId=u5500d316-9aa7-4&from=paste&height=294&id=ud7d1bde6&originHeight=294&originWidth=1188&originalType=binary&ratio=1&rotation=0&showTitle=false&size=173725&status=done&style=none&taskId=u50b48232-82bc-4628-b0a7-22a4e250566&title=&width=1188)
### 案例
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682426758086-e11675b0-3db9-4b58-b459-c037c45d0a4c.png#averageHue=%23faf9f8&clientId=u5500d316-9aa7-4&from=paste&height=185&id=uaac4fc3c&originHeight=185&originWidth=1159&originalType=binary&ratio=1&rotation=0&showTitle=false&size=111739&status=done&style=none&taskId=u250e6dac-e096-4118-8542-441d9237884&title=&width=1159)
# 4 类加载
## 4.1 类文件结构
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1682483029914-0b46b9e2-cfe2-4db8-807f-3e1817ec4401.jpeg)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682427195593-b02282c6-7b85-421b-8ab6-dfb1553307f3.png#averageHue=%23f9f9f9&clientId=u5500d316-9aa7-4&from=paste&height=425&id=u0da917a1&originHeight=425&originWidth=1409&originalType=binary&ratio=1&rotation=0&showTitle=false&size=108028&status=done&style=none&taskId=u35a1d853-d0d7-4f61-b29d-4b85f340eee&title=&width=1409)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682427200493-a0d194f1-ae54-45f4-b0f1-b7e370c93292.png#averageHue=%23fbfbfb&clientId=u5500d316-9aa7-4&from=paste&height=57&id=u8ec126d7&originHeight=57&originWidth=1383&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22486&status=done&style=none&taskId=u9d8d6e13-0ab6-446e-a82b-10320ccd193&title=&width=1383)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682427256865-c9a30b4a-70ac-40cf-890d-1e9e740c02fb.png#averageHue=%23f6f5f5&clientId=u5500d316-9aa7-4&from=paste&height=797&id=ub60698be&originHeight=797&originWidth=927&originalType=binary&ratio=1&rotation=0&showTitle=false&size=531849&status=done&style=none&taskId=udad15f92-9159-400c-a51b-235c6b252e1&title=&width=927)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682427277395-c9a27c13-e5f8-4f7d-b262-fe460c23def9.png#averageHue=%23fcfcfc&clientId=u5500d316-9aa7-4&from=paste&height=784&id=ue54b3137&originHeight=784&originWidth=1418&originalType=binary&ratio=1&rotation=0&showTitle=false&size=238903&status=done&style=none&taskId=u2c304f1d-bfd9-4efb-8179-8b47f775e80&title=&width=1418)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682427519400-9678fd4c-b963-4712-8445-935bcacf1990.png#averageHue=%23fcfcfc&clientId=u5500d316-9aa7-4&from=paste&height=253&id=u33b498e9&originHeight=253&originWidth=1343&originalType=binary&ratio=1&rotation=0&showTitle=false&size=76298&status=done&style=none&taskId=u54d04ba1-5b71-474e-8f82-1b2823d1614&title=&width=1343)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682427593439-a4517d8e-1c46-4a65-87ca-205b2f7dac5f.png#averageHue=%23fbfafa&clientId=u5500d316-9aa7-4&from=paste&height=230&id=u3cc8b341&originHeight=230&originWidth=1059&originalType=binary&ratio=1&rotation=0&showTitle=false&size=76075&status=done&style=none&taskId=u9bebbcfd-4368-4f76-809a-6b84ed29917&title=&width=1059)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682427641574-73e5b64f-97e9-4af3-a5d6-7f5b29be9702.png#averageHue=%23fdfdfd&clientId=u5500d316-9aa7-4&from=paste&height=1029&id=u868c7e9d&originHeight=1029&originWidth=1395&originalType=binary&ratio=1&rotation=0&showTitle=false&size=228115&status=done&style=none&taskId=uc983c336-e0b5-4584-9234-30db4ed2af3&title=&width=1395)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682427659469-7812ad2c-fe78-4929-8241-534604d0ba28.png#averageHue=%23e9e5df&clientId=u5500d316-9aa7-4&from=paste&height=130&id=uc442c073&originHeight=130&originWidth=1206&originalType=binary&ratio=1&rotation=0&showTitle=false&size=97457&status=done&style=none&taskId=u7acd26c9-43c8-4994-8426-fde4aa62dd6&title=&width=1206)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682428485542-e85ca4eb-8b8d-42cf-9a14-7fc124d5a53d.png#averageHue=%23fbfaf9&clientId=u5500d316-9aa7-4&from=paste&height=137&id=u7b07d87a&originHeight=174&originWidth=1476&originalType=binary&ratio=1&rotation=0&showTitle=false&size=128725&status=done&style=none&taskId=u394348f3-d0a9-42fb-88ae-ae38d6c0565&title=&width=1165)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682475733962-03570f78-1eae-4bd4-a8d3-043560eb88ed.png#averageHue=%23e7e2db&clientId=u5500d316-9aa7-4&from=paste&height=197&id=u1d9b74d2&originHeight=197&originWidth=927&originalType=binary&ratio=1&rotation=0&showTitle=false&size=112260&status=done&style=none&taskId=u8e6875d6-916c-4586-9e59-d28404368e3&title=&width=927)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682475768786-f30f1a2f-df51-454e-9214-68520617c921.png#averageHue=%23e7e3db&clientId=u5500d316-9aa7-4&from=paste&height=196&id=ucc7c9486&originHeight=196&originWidth=923&originalType=binary&ratio=1&rotation=0&showTitle=false&size=109074&status=done&style=none&taskId=u93ba541b-20d0-4f2b-b2b3-7e3e474365c&title=&width=923)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682475854474-85f8425f-b783-4ef7-b3c2-daca1e33afa1.png#averageHue=%23e7e4de&clientId=u5500d316-9aa7-4&from=paste&height=126&id=u4d99cd88&originHeight=126&originWidth=907&originalType=binary&ratio=1&rotation=0&showTitle=false&size=82848&status=done&style=none&taskId=ubb288a8e-fcd7-4df5-9890-f19c9789d12&title=&width=907)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682475892559-988a95e6-1fe5-4d0c-b529-1a425ecced7d.png#averageHue=%23e5dfd8&clientId=u5500d316-9aa7-4&from=paste&height=115&id=u9462db1e&originHeight=115&originWidth=957&originalType=binary&ratio=1&rotation=0&showTitle=false&size=77792&status=done&style=none&taskId=u6bd46e4d-4877-431c-a93c-983adf19ade&title=&width=957)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682475933694-1602def4-5299-4c4e-a611-80122f51e006.png#averageHue=%23faf9f8&clientId=u5500d316-9aa7-4&from=paste&height=182&id=u36bb1bd7&originHeight=182&originWidth=1134&originalType=binary&ratio=1&rotation=0&showTitle=false&size=122967&status=done&style=none&taskId=u8b0135bb-b40f-4144-b4ac-bf16c521fb1&title=&width=1134)

## 4.2 字节码指令
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682488534328-8f9ce6b3-290a-4f4d-bbec-3d923b5ea6ca.png#averageHue=%23fafaf9&clientId=u5500d316-9aa7-4&from=paste&height=488&id=u4572f1c4&originHeight=488&originWidth=1374&originalType=binary&ratio=1&rotation=0&showTitle=false&size=281771&status=done&style=none&taskId=u7f86635b-85e4-4ead-93bd-3d1cf6fdc58&title=&width=1374)
把class文件中的常量池信息载入到运行时常量池中
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682489525901-a1ee8698-3ff8-4c07-8f35-8fc6ec17dce1.png#averageHue=%23e0f7c9&clientId=u5500d316-9aa7-4&from=paste&height=397&id=u63fa3109&originHeight=623&originWidth=1316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=180492&status=done&style=none&taskId=u0d13d363-8ad7-475e-8e7e-fa9c2083f75&title=&width=838)
方法字节码指令都会载入到方法区中
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682489614653-7b832fc1-885a-4257-9a12-6e58adc8a6a9.png#averageHue=%23e4f7c9&clientId=u5500d316-9aa7-4&from=paste&height=392&id=u785e87ef&originHeight=626&originWidth=1335&originalType=binary&ratio=1&rotation=0&showTitle=false&size=238533&status=done&style=none&taskId=u6e71e10c-ad15-4a1b-9d38-8664c20e5fc&title=&width=836)

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682489894913-7e781995-4933-48dc-a3fc-f2e6bf6be008.png#averageHue=%23ddf3c1&clientId=u5500d316-9aa7-4&from=paste&height=628&id=ubb96432b&originHeight=715&originWidth=1324&originalType=binary&ratio=1&rotation=0&showTitle=false&size=283452&status=done&style=none&taskId=ua992261a-0456-4961-8744-1eec226c0c0&title=&width=1163)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682490138614-71b82a7b-7df5-437d-bde0-52cbf623b515.png#averageHue=%23e0f2c6&clientId=u5500d316-9aa7-4&from=paste&height=858&id=ua90e9492&originHeight=979&originWidth=1332&originalType=binary&ratio=1&rotation=0&showTitle=false&size=473905&status=done&style=none&taskId=ucb27c1ca-72f1-4b43-ba65-8d0d7a91d3e&title=&width=1167)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682490266868-ad35eb8c-cbd6-4d07-9d3a-3e063d913164.png#averageHue=%23d6f2be&clientId=u5500d316-9aa7-4&from=paste&height=901&id=ud74b56a4&originHeight=1028&originWidth=1330&originalType=binary&ratio=1&rotation=0&showTitle=false&size=463594&status=done&style=none&taskId=uba6eaebf-4c25-44b7-9b79-030ec6dcf06&title=&width=1166)
如何确定一个方法的局部变量栈的数量一个方法的局部变量栈的数量可以通过该方法的字节码文件确定。在字节码文件中，会对该方法的局部变量表的最大容量进行定义。例如，对于以下Java方法：
```java
javaCopy code
    public void exampleMethod(int a, long b, String c) {
        int d = a + 1;
        long e = b * 2;
        String f = c + " world";
        System.out.println(f);
    }
```
该方法的字节码文件中会定义该方法的局部变量表的最大容量为3，即：int a, long b, String c三个参数加上新增的三个局部变量int d, long e, String f，共计6个局部变量，但是在exampleMethod方法执行的过程中，由于在方法内部只有一个线程在执行，所以可以将这些局部变量存放在该方法对应的局部变量栈中，每个局部变量使用一个槽位（slot）来存储。因此，该方法的局部变量栈的数量为6。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682490721568-d9fa9efd-4d7d-41f2-8b4e-5d144585e6fc.png#averageHue=%23dff3c3&clientId=u5500d316-9aa7-4&from=paste&height=517&id=u36ba4128&originHeight=744&originWidth=1305&originalType=binary&ratio=1&rotation=0&showTitle=false&size=363025&status=done&style=none&taskId=uc64c514e-37fd-4987-8387-3a364fb6533&title=&width=906)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682490781605-bf600e05-34c1-46a9-868c-782abf731060.png#averageHue=%23def3c2&clientId=u5500d316-9aa7-4&from=paste&height=637&id=u417ef0e3&originHeight=637&originWidth=1329&originalType=binary&ratio=1&rotation=0&showTitle=false&size=263534&status=done&style=none&taskId=u5c31f711-4614-4ba8-a4aa-c6738172a11&title=&width=1329)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682490801760-6e39f590-d77a-4f9b-83d6-912103432c62.png#averageHue=%23d7f2c0&clientId=u5500d316-9aa7-4&from=paste&height=540&id=u43123468&originHeight=540&originWidth=1284&originalType=binary&ratio=1&rotation=0&showTitle=false&size=236100&status=done&style=none&taskId=u29e701ab-ead5-481f-a62b-98c80a54afe&title=&width=1284)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682490868351-16a9ac84-32c9-4762-9c8e-0319c6cca940.png#averageHue=%23d7f3bf&clientId=u5500d316-9aa7-4&from=paste&height=625&id=uaa45dbeb&originHeight=625&originWidth=1287&originalType=binary&ratio=1&rotation=0&showTitle=false&size=246585&status=done&style=none&taskId=u0ffe55c9-0f23-4f5c-b0af-725fa9f88de&title=&width=1287)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682490877750-b4b64346-8fd0-4ffc-9ac5-f854226aa3ff.png#averageHue=%23d8f2c0&clientId=u5500d316-9aa7-4&from=paste&height=540&id=ue6e7ade9&originHeight=540&originWidth=1315&originalType=binary&ratio=1&rotation=0&showTitle=false&size=236404&status=done&style=none&taskId=u7f85ca59-c5c7-481f-af2f-417c2524c4d&title=&width=1315)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682490896408-6f4e67f2-e5df-446b-b542-0d9021cb33a6.png#averageHue=%23d8f2c0&clientId=u5500d316-9aa7-4&from=paste&height=628&id=u73057e30&originHeight=628&originWidth=1311&originalType=binary&ratio=1&rotation=0&showTitle=false&size=272909&status=done&style=none&taskId=u1a4cf359-7f74-4b08-984d-338bf415d1a&title=&width=1311)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682490911035-87a40464-8557-4b53-b3fc-56b9eec312d2.png#averageHue=%23cdf2c1&clientId=u5500d316-9aa7-4&from=paste&height=548&id=u217e70b4&originHeight=548&originWidth=1278&originalType=binary&ratio=1&rotation=0&showTitle=false&size=240950&status=done&style=none&taskId=ue04df81b-9098-4be1-8955-fe6b0a1a855&title=&width=1278)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682491267760-2c25e7c2-92b2-4d1c-82ab-b299cf070265.png#averageHue=%23def3c4&clientId=u5500d316-9aa7-4&from=paste&height=654&id=u6c887f4b&originHeight=654&originWidth=1351&originalType=binary&ratio=1&rotation=0&showTitle=false&size=293542&status=done&style=none&taskId=u9d9d3843-5fb9-4b66-a898-deda5b8d25a&title=&width=1351)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682491281684-7de851f0-5896-4b4d-a852-658c68278cdb.png#averageHue=%23d2f3c1&clientId=u5500d316-9aa7-4&from=paste&height=556&id=u7c45b823&originHeight=556&originWidth=1303&originalType=binary&ratio=1&rotation=0&showTitle=false&size=267298&status=done&style=none&taskId=u3fbef7f4-e88a-427d-a9c9-a6600c57f70&title=&width=1303)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682491301062-6c91ab03-163e-4ef5-a9df-18e3734a08a9.png#averageHue=%23d9f3c1&clientId=u5500d316-9aa7-4&from=paste&height=624&id=u438aefd6&originHeight=624&originWidth=1336&originalType=binary&ratio=1&rotation=0&showTitle=false&size=285824&status=done&style=none&taskId=uc865a2a6-9def-4092-8d32-777192fa791&title=&width=1336)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682491328131-37f7a453-53da-41bf-965b-1d50c7e73da5.png#averageHue=%23d8f3c1&clientId=u5500d316-9aa7-4&from=paste&height=550&id=u18f36616&originHeight=550&originWidth=1303&originalType=binary&ratio=1&rotation=0&showTitle=false&size=268301&status=done&style=none&taskId=ucec714f2-94d2-427f-a57c-59866c642d6&title=&width=1303)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682491421084-e8a9e497-0c4e-4e04-b3dd-cdf8ae5b3a68.png#averageHue=%23e3f1cc&clientId=u5500d316-9aa7-4&from=paste&height=1062&id=u8bb73ae5&originHeight=1062&originWidth=1484&originalType=binary&ratio=1&rotation=0&showTitle=false&size=539016&status=done&style=none&taskId=u938aef23-b76e-4bfa-a061-4dc50ae797b&title=&width=1484)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682491504993-a2748ce6-3545-4236-b08d-8c76fbf6244e.png#averageHue=%23dff3c6&clientId=u5500d316-9aa7-4&from=paste&height=839&id=u7f7675cb&originHeight=839&originWidth=1376&originalType=binary&ratio=1&rotation=0&showTitle=false&size=323792&status=done&style=none&taskId=u05c0a3bf-daf1-4c7b-9844-59ead08be71&title=&width=1376)
#### 案例
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682491648132-bf5e8dff-e475-4d5f-810e-36d07d5082ee.png#averageHue=%23fcfcfc&clientId=u5500d316-9aa7-4&from=paste&height=731&id=u7d4ad340&originHeight=731&originWidth=1458&originalType=binary&ratio=1&rotation=0&showTitle=false&size=202235&status=done&style=none&taskId=ue0b73f86-0c1b-47c4-b4bf-913b8b40388&title=&width=1458)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682491669177-9dbfa832-e1df-4c3f-a920-14d03b39fb49.png#averageHue=%23ddf3c2&clientId=u5500d316-9aa7-4&from=paste&height=799&id=u86ecb29a&originHeight=799&originWidth=1240&originalType=binary&ratio=1&rotation=0&showTitle=false&size=269579&status=done&style=none&taskId=u4bc4a4ad-d83b-4e9a-a31e-16245fb0713&title=&width=1240)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682492368201-d27ea92d-62b4-4c59-8389-a02ca12c830c.png#averageHue=%23fbfbfa&clientId=u5500d316-9aa7-4&from=paste&height=1016&id=u8137f057&originHeight=1016&originWidth=1406&originalType=binary&ratio=1&rotation=0&showTitle=false&size=322216&status=done&style=none&taskId=u4def2d5a-435d-449b-87a5-c14a6999716&title=&width=1406)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682492552519-dc9f6d81-5de0-4ae9-a2c1-61ecc8439a6a.png#averageHue=%23fbfafa&clientId=u5500d316-9aa7-4&from=paste&height=1066&id=u7c07ca68&originHeight=1066&originWidth=1301&originalType=binary&ratio=1&rotation=0&showTitle=false&size=501950&status=done&style=none&taskId=u5b9bf8cd-8916-42a7-ae75-f4af9231a45&title=&width=1301)
## 4.3 编译器处理
## 4.4 类加载阶段
### 加载
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682493171024-e832d811-b222-4711-864f-5b2d452efef6.png#averageHue=%23fafaf9&clientId=u5500d316-9aa7-4&from=paste&height=694&id=ub38ad3cd&originHeight=694&originWidth=1304&originalType=binary&ratio=1&rotation=0&showTitle=false&size=326775&status=done&style=none&taskId=u7a71e3b7-5efd-4f8f-9d27-41f8b3fda22&title=&width=1304)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682493216641-24d7fd2b-ea5c-4bf0-8a04-322f2ef3de3d.png#averageHue=%23e8edb9&clientId=u5500d316-9aa7-4&from=paste&height=811&id=uf1331a9f&originHeight=811&originWidth=1326&originalType=binary&ratio=1&rotation=0&showTitle=false&size=369316&status=done&style=none&taskId=u91071960-6646-466b-b9e6-fd507bcd6bc&title=&width=1326)
### 链接
#### 验证
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682493446590-fb2a90f4-3c11-4d27-977b-b0f97ca73f39.png#averageHue=%23e9e5df&clientId=u5500d316-9aa7-4&from=paste&height=995&id=u8f42d162&originHeight=995&originWidth=1306&originalType=binary&ratio=1&rotation=0&showTitle=false&size=859231&status=done&style=none&taskId=u96436a07-20a9-428c-96bf-f11706b03f7&title=&width=1306)
#### 准备
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682494063635-6d751734-ab6b-4633-a397-21ce05dbe49c.png#averageHue=%23e7e6df&clientId=u5500d316-9aa7-4&from=paste&height=273&id=u875ea2a9&originHeight=273&originWidth=1321&originalType=binary&ratio=1&rotation=0&showTitle=false&size=328307&status=done&style=none&taskId=u3bb3ad2e-f9d8-4df0-b16c-d883aa399ba&title=&width=1321)
#### 解析
将常量池中的符号引用解析为直接引用
#### 初始化
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682494946744-f77f5a1d-e05d-4124-8e06-a82e0e00bdc6.png#averageHue=%23f7f7f6&clientId=u5500d316-9aa7-4&from=paste&height=1027&id=u14ff2097&originHeight=1027&originWidth=1039&originalType=binary&ratio=1&rotation=0&showTitle=false&size=436712&status=done&style=none&taskId=u7c8e18dd-a9e0-463f-93de-aa259703430&title=&width=1039)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682495008908-f6ea8c50-18a6-458e-831d-4e85d4c14a32.png#averageHue=%23dbd5cd&clientId=u5500d316-9aa7-4&from=paste&height=352&id=u98248ee6&originHeight=352&originWidth=1028&originalType=binary&ratio=1&rotation=0&showTitle=false&size=187282&status=done&style=none&taskId=ub40e8e76-1678-437d-98f1-e8f405754b8&title=&width=1028)
## 4.5 类加载器
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1682495187151-0dc9f289-b858-4cab-b9d2-de78d6f606e7.png#averageHue=%23fafaf9&clientId=u5500d316-9aa7-4&from=paste&height=390&id=ue99cba31&originHeight=390&originWidth=1285&originalType=binary&ratio=1&rotation=0&showTitle=false&size=205238&status=done&style=none&taskId=u421197a1-4027-4a5f-a65c-88ce2919ad5&title=&width=1285)

## 4.6 运行期优化

