![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683357556966-69658380-e291-4ea0-87ed-3ee85bbe50aa.png#averageHue=%23faf7f7&clientId=u05b937fa-89df-4&from=paste&height=475&id=u4ef374ba&originHeight=475&originWidth=1100&originalType=binary&ratio=1&rotation=0&showTitle=false&size=112520&status=done&style=none&taskId=u201ecb79-1701-4224-936d-29d27ba160e&title=&width=1100)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683357591554-c3c5256a-927c-4bcd-ad1e-5b8d396d8d25.png#averageHue=%23f5eae8&clientId=u05b937fa-89df-4&from=paste&height=372&id=u03a03415&originHeight=372&originWidth=1484&originalType=binary&ratio=1&rotation=0&showTitle=false&size=321248&status=done&style=none&taskId=u88db8508-bcb8-4f8f-8c78-e5d0fa82544&title=&width=1484)
# SpringMVC简介
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683357636967-18061642-4516-48a4-858b-1f60ab918843.png#averageHue=%23f7f1f0&clientId=u05b937fa-89df-4&from=paste&height=510&id=u3158b26d&originHeight=510&originWidth=953&originalType=binary&ratio=1&rotation=0&showTitle=false&size=123791&status=done&style=none&taskId=uc0b78f02-8ac2-4201-a5bc-22ed7230ea4&title=&width=953)
## 请求响应模式演进过程
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683358191411-b405314b-0f66-4e86-b713-be2f2b9a99d1.png#averageHue=%23efdcd9&clientId=u05b937fa-89df-4&from=paste&height=424&id=u7d69df03&originHeight=673&originWidth=421&originalType=binary&ratio=1&rotation=0&showTitle=false&size=48131&status=done&style=none&taskId=u99ef50a2-3787-48dc-b040-a459959d5a6&title=&width=265)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683358302622-ee8212e7-0c88-4656-844a-b066cdaccd77.png#averageHue=%23ecd3cf&clientId=u05b937fa-89df-4&from=paste&height=413&id=u11af5c01&originHeight=661&originWidth=485&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78259&status=done&style=none&taskId=u4c21e6ad-18bb-45f0-ab62-02877b07edb&title=&width=303)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683358429106-66fcea5e-a819-4979-884c-1a7c9cdd0f0e.png#averageHue=%23f3e4e1&clientId=u05b937fa-89df-4&from=paste&height=707&id=u3004f294&originHeight=707&originWidth=1386&originalType=binary&ratio=1&rotation=0&showTitle=false&size=153798&status=done&style=none&taskId=ua179fbb6-f4d1-4847-9c7d-f5ed6ff899f&title=&width=1386)
## springMVC

- SpringMVC是一种基于**Java**实现MVC模型的轻量级Web框架
- springMVC主要负责**controller功能的开发**以及**将操作完的数据转换成json形式**（后端服务器操作完的数据通常为对象形式，但这不能被前端页面所识别，因此需将对象封装为json形式）
**问题：SpringMVC控制com.itheima.controller下的bean，而Spring控制com.itheima下的bean，这样Spring就会对controller包下的bean进行管理，如何避免这种情况？**![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683523755282-f2b948b8-f8f3-4491-8077-1f4a14a0315d.png#averageHue=%23fbfaf8&clientId=u05b937fa-89df-4&from=paste&height=789&id=enGTF&originHeight=789&originWidth=1499&originalType=binary&ratio=1&rotation=0&showTitle=false&size=427153&status=done&style=none&taskId=u13ced90b-eda2-4591-beeb-6d479fb0366&title=&width=1499)
方式一：
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683523381509-474ed134-aa9f-47fe-bf07-d542bb58cff3.png#averageHue=%23fdfcf9&clientId=u05b937fa-89df-4&from=paste&height=254&id=nFi9P&originHeight=254&originWidth=834&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27917&status=done&style=none&taskId=u66eff578-c31d-465f-8858-4574db81265&title=&width=834)
方式二：
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683523480693-12161293-9e14-4d5f-8219-de89d273459a.png#averageHue=%23faf9f3&clientId=u05b937fa-89df-4&from=paste&height=147&id=YqOTz&originHeight=147&originWidth=791&originalType=binary&ratio=1&rotation=0&showTitle=false&size=65195&status=done&style=none&taskId=u3dfa15be-218c-46b7-aca4-8d59b4e4d61&title=&width=791)
## Spring及SpringMVC如何加载bean？
### @ComponentScan
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683523945560-53b6d1cc-6409-4d98-88d8-eb2070ddcc51.png#averageHue=%23fbfaee&clientId=u05b937fa-89df-4&from=paste&height=656&id=u5fc23fc5&originHeight=656&originWidth=1557&originalType=binary&ratio=1&rotation=0&showTitle=false&size=297615&status=done&style=none&taskId=ucbd3efc8-0ec7-4cf1-b37a-97f7f54c486&title=&width=1557)
### 加载配置
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683524061509-b44cb99c-702d-47cd-8aaf-ad049f7c6e3f.png#averageHue=%23f9f7de&clientId=u05b937fa-89df-4&from=paste&height=716&id=u9e023c36&originHeight=716&originWidth=1537&originalType=binary&ratio=1&rotation=0&showTitle=false&size=397455&status=done&style=none&taskId=u46745448-5848-4f37-bf35-57fa71d6e93&title=&width=1537)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683524216464-888147af-0ff4-4831-b769-9aa49bf5e264.png#averageHue=%23fbf9df&clientId=u05b937fa-89df-4&from=paste&height=591&id=u84e954cd&originHeight=591&originWidth=1535&originalType=binary&ratio=1&rotation=0&showTitle=false&size=285289&status=done&style=none&taskId=u21924d79-7769-4e91-92b3-06a75368850&title=&width=1535)
## PostMan简介
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683524375524-f52be3e8-984f-4ab5-83b0-9f01d5198c2e.png#averageHue=%23fcfaf9&clientId=u05b937fa-89df-4&from=paste&height=498&id=u6beafccf&originHeight=498&originWidth=1345&originalType=binary&ratio=1&rotation=0&showTitle=false&size=131797&status=done&style=none&taskId=u61fd8167-19d8-41b2-a089-fd8b5cef6d4&title=&width=1345)
# 请求
## 请求路径
问题：在开发过程中，多个XxxController类中，设置的请求路径相同如何处理？![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683525698614-c49b8e2a-441d-4a28-a2e7-282e413f9871.png#averageHue=%23f9f9f7&clientId=u05b937fa-89df-4&from=paste&height=202&id=u12c75dee&originHeight=702&originWidth=1030&originalType=binary&ratio=1&rotation=0&showTitle=false&size=336094&status=done&style=none&taskId=u05006610-0075-41b1-a6f5-65e3d67af8c&title=&width=296)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683525714638-29ea03b8-d672-4a58-ada8-83613e4a40d4.png#averageHue=%23eceae1&clientId=u05b937fa-89df-4&from=paste&height=202&id=ub44fd447&originHeight=553&originWidth=1014&originalType=binary&ratio=1&rotation=0&showTitle=false&size=299005&status=done&style=none&taskId=ue86e1b6d-e09b-4eed-80e8-0cf81748df5&title=&width=371)
设置请求路径以/模块/请求路径
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683525780067-138c3c57-23ed-4a30-8b1e-07f9edbf165e.png#averageHue=%23f8f8f6&clientId=u05b937fa-89df-4&from=paste&height=296&id=uadb8011e&originHeight=679&originWidth=671&originalType=binary&ratio=1&rotation=0&showTitle=false&size=219868&status=done&style=none&taskId=ud38a8d5e-3e75-427a-bc03-e17ca19c0fb&title=&width=293)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683525665815-b1b166fd-4cbe-4565-98ef-6f38c4e005a2.png#averageHue=%23fbfaef&clientId=u05b937fa-89df-4&from=paste&height=795&id=uda3602d9&originHeight=795&originWidth=1562&originalType=binary&ratio=1&rotation=0&showTitle=false&size=357197&status=done&style=none&taskId=u5e09749c-5ebc-49a2-86fe-be175957ea7&title=&width=1562)
## 请求传参
### 普通参数
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683525954346-4528f369-b24f-4a89-909a-c8862b075ebe.png#averageHue=%23eeeeee&clientId=u05b937fa-89df-4&from=paste&height=66&id=ua9f76d2f&originHeight=66&originWidth=1103&originalType=binary&ratio=1&rotation=0&showTitle=false&size=18207&status=done&style=none&taskId=u13eb51cc-9c0d-4a2b-9f65-81bfed3879c&title=&width=1103)
在请求路径中传递的参数，在XxxController中直接在方法的形参中接收普通参数（地址参数名与形参变量名相同）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683526078505-8c48032f-c5b1-48cf-be24-8bd7ed2566c0.png#averageHue=%23f9f8f6&clientId=u05b937fa-89df-4&from=paste&height=391&id=ufcb92a5a&originHeight=391&originWidth=784&originalType=binary&ratio=1&rotation=0&showTitle=false&size=164156&status=done&style=none&taskId=udb92197d-7ec4-4b14-a695-4a476077103&title=&width=784)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683526291066-93ffb99d-233f-442a-b53e-d4f2d126aebc.png#averageHue=%23fafaf2&clientId=u05b937fa-89df-4&from=paste&height=785&id=u6f21a2f7&originHeight=785&originWidth=1558&originalType=binary&ratio=1&rotation=0&showTitle=false&size=308731&status=done&style=none&taskId=ufa32caf3-f35b-4f37-b5c6-ce6232e767d&title=&width=1558)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683526431313-14b63f98-92c8-48b2-8beb-e06dc6103a15.png#averageHue=%23faf8f1&clientId=u05b937fa-89df-4&from=paste&height=790&id=u54bebcb1&originHeight=790&originWidth=1565&originalType=binary&ratio=1&rotation=0&showTitle=false&size=364235&status=done&style=none&taskId=u1bd7933c-e314-4b53-bd2f-d5d17a65697&title=&width=1565)
问题1：在form表单post传参时，若发送的数据中含有中文，则会出现乱码问题，如何解决？![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683526788672-2fcf07e4-d53f-4a2d-b7f3-0efcba4d9b97.png#averageHue=%23faf9f8&clientId=u05b937fa-89df-4&from=paste&height=81&id=u3d3c4e5c&originHeight=81&originWidth=676&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27736&status=done&style=none&taskId=u6b573860-dad3-424d-947d-660afcc3c8d&title=&width=676)
**解决：**
设置过滤器（此种方法只适合处理post请求发送的数据，对于get请求发送的中文数据不适用(仍为乱码)）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683526840553-ad62fe2f-ac3b-4eef-a38a-50534f314156.png#averageHue=%23e5e4df&clientId=u05b937fa-89df-4&from=paste&height=432&id=u90526690&originHeight=432&originWidth=1189&originalType=binary&ratio=1&rotation=0&showTitle=false&size=244555&status=done&style=none&taskId=u6c8fd2e2-55f3-438e-bea7-da57ec7a912&title=&width=1189)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683527496913-bb7786a6-989e-4f6d-aac5-27e1f4fe5e7c.png#averageHue=%23faf9e8&clientId=u05b937fa-89df-4&from=paste&height=590&id=u7158386f&originHeight=590&originWidth=1567&originalType=binary&ratio=1&rotation=0&showTitle=false&size=301069&status=done&style=none&taskId=u5a83d065-522a-4f18-b863-30aea44c78e&title=&width=1567)
问题2：若请求参数名和形参变量名不一致，该如何解决？若请求参数名和形参变量名不一致，则无法将请求参数的值传递给形参变量
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683527788489-70b0fcfa-bb29-4d26-9338-6a7eaffc9129.png#averageHue=%23ede3da&clientId=u05b937fa-89df-4&from=paste&height=108&id=ub2630e39&originHeight=108&originWidth=752&originalType=binary&ratio=1&rotation=0&showTitle=false&size=46568&status=done&style=none&taskId=u14b0c7ac-c019-474d-9f70-977ac380d40&title=&width=752)
解决：
在形参变量名前使用`@RequestParam(请求参数名)`将请求参数名与形参变量名绑定
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683527920404-f6a6a414-c705-4ee3-9ad6-4fc093373f56.png#averageHue=%23f2f0e7&clientId=u05b937fa-89df-4&from=paste&height=189&id=u0124c713&originHeight=189&originWidth=1088&originalType=binary&ratio=1&rotation=0&showTitle=false&size=124222&status=done&style=none&taskId=u730b3ecf-7048-4c63-b75e-fabb3b0171b&title=&width=1088)
### POJO参数
情况一：若请求参数名与形参的实体类的属性名一致，则自动将请求参数封装成实体类传入
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528086854-159857f3-f7df-4fda-bb80-4fe523e2f4c6.png#averageHue=%23eeeeee&clientId=u05b937fa-89df-4&from=paste&height=82&id=u76f5c9c2&originHeight=82&originWidth=760&originalType=binary&ratio=1&rotation=0&showTitle=false&size=16532&status=done&style=none&taskId=u8a7e55b7-8f89-4a92-9dba-691e2127814&title=&width=760)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528134279-59eb70b6-39da-4a87-8bd6-c2b296df6698.png#averageHue=%23fcfbfa&clientId=u05b937fa-89df-4&from=paste&height=302&id=u849e9d16&originHeight=350&originWidth=463&originalType=binary&ratio=1&rotation=0&showTitle=false&size=67318&status=done&style=none&taskId=u82148016-f2b2-4b32-8795-6fd7f416803&title=&width=399)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528156240-1a670919-0841-42e0-b359-36c849e088f8.png#averageHue=%23fbfaf7&clientId=u05b937fa-89df-4&from=paste&height=231&id=u4e96fbb5&originHeight=240&originWidth=668&originalType=binary&ratio=1&rotation=0&showTitle=false&size=87850&status=done&style=none&taskId=u5c68f53f-ef57-4470-811d-be912f440a4&title=&width=642)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528218267-0c2c406a-a8f9-418d-843a-4848191f07ae.png#averageHue=%23eaebe7&clientId=u05b937fa-89df-4&from=paste&height=233&id=ue588f962&originHeight=233&originWidth=965&originalType=binary&ratio=1&rotation=0&showTitle=false&size=155168&status=done&style=none&taskId=ubaf2439c-3d9d-4c0d-a18c-ce2929e993e&title=&width=965)
### 嵌套POJO参数
一个POJO类的属性为另一个POJO类，则请求参数名需要设置属性名.属性名
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528435511-15b2dacf-8cb6-4ba9-b5ae-97b4b92bef2e.png#averageHue=%23f8f5ec&clientId=u05b937fa-89df-4&from=paste&height=134&id=u1d81fffd&originHeight=179&originWidth=469&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36983&status=done&style=none&taskId=u4800e7cb-771f-417e-a1f7-38a7621dfb9&title=&width=350)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528455880-f2e9e1b6-acc7-48bf-9ceb-8b06d90ef583.png#averageHue=%23f6f5ee&clientId=u05b937fa-89df-4&from=paste&height=88&id=u01090aad&originHeight=102&originWidth=424&originalType=binary&ratio=1&rotation=0&showTitle=false&size=32749&status=done&style=none&taskId=u95bb4ef1-de87-4838-99d7-77d277a16f5&title=&width=365)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528518975-6ee37c65-34ef-493a-9b98-0fc9dab82557.png#averageHue=%23f9f9f9&clientId=u05b937fa-89df-4&from=paste&height=561&id=u4a64d859&originHeight=561&originWidth=1283&originalType=binary&ratio=1&rotation=0&showTitle=false&size=124030&status=done&style=none&taskId=u18fae320-59df-443c-bfe6-32192b6054a&title=&width=1283)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528360232-98f70969-987c-4623-beeb-4e4ae5a10d55.png#averageHue=%23f3f1e6&clientId=u05b937fa-89df-4&from=paste&height=223&id=ue53868c4&originHeight=223&originWidth=762&originalType=binary&ratio=1&rotation=0&showTitle=false&size=109328&status=done&style=none&taskId=ubc19c968-cd70-48eb-ac2e-9eff72da692&title=&width=762)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528380870-b72b1a64-e20b-48d0-9ec2-07fa296bbe0e.png#averageHue=%23ebeae5&clientId=u05b937fa-89df-4&from=paste&height=277&id=u1c98e190&originHeight=277&originWidth=1626&originalType=binary&ratio=1&rotation=0&showTitle=false&size=232259&status=done&style=none&taskId=u9f5e819d-eb8f-4da1-b466-c6b5a2b0993&title=&width=1626)
### 数组参数
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528719188-43232665-c2c8-4b6a-9484-c1eff09e2496.png#averageHue=%23fafaf9&clientId=u05b937fa-89df-4&from=paste&height=538&id=ud0b37fea&originHeight=538&originWidth=1282&originalType=binary&ratio=1&rotation=0&showTitle=false&size=106406&status=done&style=none&taskId=ud63561df-619b-48a3-a904-bb284c514a1&title=&width=1282)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528745240-948d65b9-6bae-4266-90ce-75c885f15bb6.png#averageHue=%23fbfaf7&clientId=u05b937fa-89df-4&from=paste&height=218&id=udf3f9831&originHeight=218&originWidth=871&originalType=binary&ratio=1&rotation=0&showTitle=false&size=101312&status=done&style=none&taskId=u59afe992-bbf1-47c0-a176-4f03d0d7c70&title=&width=871)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528768955-4ba35a97-b966-4581-81cf-8f8589d2708b.png#averageHue=%23e5e2dc&clientId=u05b937fa-89df-4&from=paste&height=184&id=ude316f99&originHeight=184&originWidth=1606&originalType=binary&ratio=1&rotation=0&showTitle=false&size=194940&status=done&style=none&taskId=u56847e05-3ff4-466f-8518-5ce02f7457a&title=&width=1606)
 
### 集合参数
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683528973997-3f03f106-3f8e-44be-865f-2496a1be061e.png#averageHue=%23f9f9f9&clientId=u05b937fa-89df-4&from=paste&height=433&id=u06e4f04d&originHeight=433&originWidth=1124&originalType=binary&ratio=1&rotation=0&showTitle=false&size=73072&status=done&style=none&taskId=ua504bd95-30ac-442a-8549-27d4a8db75b&title=&width=1124)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529308740-0f9387f7-1ea7-4399-b4c8-c120773ed1e3.png#averageHue=%23f5f2ec&clientId=u05b937fa-89df-4&from=paste&height=196&id=u5b0f15ba&originHeight=196&originWidth=1451&originalType=binary&ratio=1&rotation=0&showTitle=false&size=201649&status=done&style=none&taskId=u12481f45-2a5f-4f8b-99c0-ff1ef301cfd&title=&width=1451)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529206939-d2c1e8bf-3999-42d3-8d2d-71120f32ab9f.png#averageHue=%23fbf9f6&clientId=u05b937fa-89df-4&from=paste&height=261&id=u1ea43f52&originHeight=261&originWidth=794&originalType=binary&ratio=1&rotation=0&showTitle=false&size=101707&status=done&style=none&taskId=u9bc821dd-30e9-4cf4-8cc6-a9f3a0039ed&title=&width=794)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529234036-e9037d95-5570-48f1-97f6-3e8bd30b9755.png#averageHue=%23eeeeeb&clientId=u05b937fa-89df-4&from=paste&height=206&id=u845f40e0&originHeight=206&originWidth=1237&originalType=binary&ratio=1&rotation=0&showTitle=false&size=178896&status=done&style=none&taskId=u8ddd84a6-6e9e-4c97-90fe-cc183062881&title=&width=1237)
### JSON参数

1. **导入json坐标**

为了让java可以访问和解析JSON数据，因此需要先导入JSON坐标
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529785397-cc1cbc2d-dc70-43e8-8fd4-80776033b887.png#averageHue=%23f1efe9&clientId=u05b937fa-89df-4&from=paste&height=158&id=ud7e5c2ae&originHeight=158&originWidth=704&originalType=binary&ratio=1&rotation=0&showTitle=false&size=73926&status=done&style=none&taskId=u78defc6c-0fff-4963-90de-f6d9b69c2d5&title=&width=704)

2. **如何在postman中发送json数据**

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683530066573-c2a43548-49f7-46a6-9af2-d421657e0334.png#averageHue=%23fcfbfb&clientId=u05b937fa-89df-4&from=paste&height=463&id=uf24772ec&originHeight=463&originWidth=843&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33784&status=done&style=none&taskId=ude5cfe45-f36b-41c3-a90f-ab7824f1bf9&title=&width=843)

3. **开启json数据转化为对象的功能**

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683530171493-77f18542-ac29-4f25-adcb-cce0da4be798.png#averageHue=%23f7f6f5&clientId=u05b937fa-89df-4&from=paste&height=512&id=u500edcfe&originHeight=512&originWidth=1054&originalType=binary&ratio=1&rotation=0&showTitle=false&size=265087&status=done&style=none&taskId=ua271d3db-44ac-40f3-a6f2-5476951f3a0&title=&width=1054)

4. **在要接受json数据的形参前加上**`**@RequestBody**`

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683530350632-251a53a1-87a0-4896-b8c2-cfef1232e278.png#averageHue=%23f5f3e8&clientId=u05b937fa-89df-4&from=paste&height=235&id=u1f660056&originHeight=235&originWidth=879&originalType=binary&ratio=1&rotation=0&showTitle=false&size=123468&status=done&style=none&taskId=u3ca8e8d5-cbf1-4dc1-9b89-e0bce0dbfee&title=&width=879)
#### 演示
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683531001560-0e8cbc42-01bf-4d77-b1ae-441988b813a0.png#averageHue=%23fbfaef&clientId=u05b937fa-89df-4&from=paste&height=710&id=u0d7c9df6&originHeight=710&originWidth=1575&originalType=binary&ratio=1&rotation=0&showTitle=false&size=301809&status=done&style=none&taskId=u4ec2e809-3747-46ce-8960-6654f257175&title=&width=1575)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683530969973-35f3585a-0c2c-447b-8029-22f2fd3bf885.png#averageHue=%23fbfaef&clientId=u05b937fa-89df-4&from=paste&height=709&id=ub9f494d3&originHeight=709&originWidth=1545&originalType=binary&ratio=1&rotation=0&showTitle=false&size=340671&status=done&style=none&taskId=u21d93173-e903-4bd8-82b5-60c4d9bc8e6&title=&width=1545)
### 日期类型参数
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683532423117-bb4d2a22-e5bb-445e-b354-9dc40bfdc8cb.png#averageHue=%23faf9eb&clientId=u05b937fa-89df-4&from=paste&height=721&id=u511f9852&originHeight=721&originWidth=1582&originalType=binary&ratio=1&rotation=0&showTitle=false&size=507576&status=done&style=none&taskId=u3556fb94-6df9-4033-a40a-a94f50aa1d5&title=&width=1582)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683532264130-425c3887-3c29-49ab-9770-0f2c1fdef3b1.png#averageHue=%23e9e9e6&clientId=u05b937fa-89df-4&from=paste&height=102&id=ud656ea39&originHeight=102&originWidth=783&originalType=binary&ratio=1&rotation=0&showTitle=false&size=87174&status=done&style=none&taskId=u3765f372-056e-44df-ab14-47dfdab9256&title=&width=783)
底层使用了Converter接口的实现类实现日期格式转换
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683532592538-0cebf44d-c7ca-400d-a777-830383d9e8c7.png#averageHue=%23fcfcf4&clientId=u05b937fa-89df-4&from=paste&height=671&id=ua78b5568&originHeight=671&originWidth=1572&originalType=binary&ratio=1&rotation=0&showTitle=false&size=171997&status=done&style=none&taskId=u113da448-e686-4352-82ac-3cb3230883f&title=&width=1572)
### 注解
#### @RequestParam
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529439330-e20c4696-e985-450f-96a6-6a1124dfb6a1.png#averageHue=%23fbfaf3&clientId=u05b937fa-89df-4&from=paste&height=761&id=u2626b74c&originHeight=761&originWidth=1588&originalType=binary&ratio=1&rotation=0&showTitle=false&size=384090&status=done&style=none&taskId=u849a815c-a8e8-4dd0-bef8-122c4b559dd&title=&width=1588)
#### @RequestBody 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683530908553-e3a5dfde-59e1-4ea7-b480-5276770539c4.png#averageHue=%23faf9ec&clientId=u05b937fa-89df-4&from=paste&height=588&id=u71fe07d4&originHeight=588&originWidth=1551&originalType=binary&ratio=1&rotation=0&showTitle=false&size=318492&status=done&style=none&taskId=u8095da80-18b6-4c4c-801a-d24f5c8f7f7&title=&width=1551)
#### @EnableWebMvc 
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683530838698-cd9405a5-ed30-45e7-810c-3a57ad567f72.png#averageHue=%23fcfaee&clientId=u05b937fa-89df-4&from=paste&height=537&id=ub6aa3075&originHeight=537&originWidth=1565&originalType=binary&ratio=1&rotation=0&showTitle=false&size=178678&status=done&style=none&taskId=u231e8e53-7340-4438-8c55-f157ecbf0a5&title=&width=1565)
#### @DateTimeFormat
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683532495468-46d6188e-6600-4ed6-9641-cea67d033d08.png#averageHue=%23fcfbee&clientId=u05b937fa-89df-4&from=paste&height=638&id=u77bea4e8&originHeight=638&originWidth=1563&originalType=binary&ratio=1&rotation=0&showTitle=false&size=256300&status=done&style=none&taskId=u19a6e459-aeba-487e-89fd-f39e832aa05&title=&width=1563)
#### @RequestBody与@RequestParam的区别
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683531128912-7f79c345-e15a-4523-a86e-50b836f36bd9.png#averageHue=%23fafaf9&clientId=u05b937fa-89df-4&from=paste&height=436&id=u25cab242&originHeight=436&originWidth=1274&originalType=binary&ratio=1&rotation=0&showTitle=false&size=221773&status=done&style=none&taskId=u3fdbe2d3-ae99-4c1c-aac6-8adad06ffb7&title=&width=1274)
### 总结
如果名称匹配，则直接传参；如果名称不匹配，则通过`@RequestParam`绑定关系
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529497213-b5a16178-9eb1-46f4-8bed-85743962f11d.png#averageHue=%23fbfaf3&clientId=u05b937fa-89df-4&from=paste&height=804&id=uccb59aa5&originHeight=804&originWidth=1611&originalType=binary&ratio=1&rotation=0&showTitle=false&size=301098&status=done&style=none&taskId=u87291684-7976-45e5-85eb-4ca2a5284a9&title=&width=1611)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529516058-ee0aa59d-43af-45ea-8faa-a2a3c7f83c9d.png#averageHue=%23fbfbf3&clientId=u05b937fa-89df-4&from=paste&height=768&id=uebae055a&originHeight=768&originWidth=1591&originalType=binary&ratio=1&rotation=0&showTitle=false&size=382838&status=done&style=none&taskId=u718aa36b-24c4-4d7e-9fd8-8144e51d3d4&title=&width=1591)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529536706-220c3af4-ae22-4f41-af09-aad41d9b885f.png#averageHue=%23fafaf1&clientId=u05b937fa-89df-4&from=paste&height=827&id=u35f2ada7&originHeight=827&originWidth=1575&originalType=binary&ratio=1&rotation=0&showTitle=false&size=258778&status=done&style=none&taskId=u1bd7c11a-1277-4540-a4e8-e3de011134d&title=&width=1575)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529562371-665dd095-5285-4117-89ae-aed94e82c6f0.png#averageHue=%23faf9f3&clientId=u05b937fa-89df-4&from=paste&height=820&id=u5e30c205&originHeight=820&originWidth=1537&originalType=binary&ratio=1&rotation=0&showTitle=false&size=336584&status=done&style=none&taskId=u1c5371d1-20c2-4b78-945b-c9e44b3bc92&title=&width=1537)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529579599-6cb3c792-2117-468d-ba67-114671b3bbbe.png#averageHue=%23faf9f2&clientId=u05b937fa-89df-4&from=paste&height=726&id=ub10e08e3&originHeight=726&originWidth=1548&originalType=binary&ratio=1&rotation=0&showTitle=false&size=288205&status=done&style=none&taskId=ua4aa3c60-ba1f-4a65-879b-b6c95fbbf18&title=&width=1548)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683529595793-9fb09e67-8fc0-4ce4-a27b-9419559b6e8c.png#averageHue=%23faf9f2&clientId=u05b937fa-89df-4&from=paste&height=704&id=ud73ac048&originHeight=704&originWidth=1531&originalType=binary&ratio=1&rotation=0&showTitle=false&size=279140&status=done&style=none&taskId=u9d22ab12-d4eb-4f14-836e-e3ef096f61f&title=&width=1531)
# 响应
## 响应页面
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683532894144-8409ce8b-a3a6-44b6-84a5-eb4894a1f2a4.png#averageHue=%23fcfcfa&clientId=u05b937fa-89df-4&from=paste&height=202&id=ua2be3ff8&originHeight=202&originWidth=738&originalType=binary&ratio=1&rotation=0&showTitle=false&size=68879&status=done&style=none&taskId=uf882fb04-d79f-4fb5-a6e1-1f55244d949&title=&width=738)
## 响应文本数据
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683533035406-d1ed670e-7414-4ae7-83c8-2ed5e3287b99.png#averageHue=%23fbfaf6&clientId=u05b937fa-89df-4&from=paste&height=235&id=uf075326a&originHeight=235&originWidth=694&originalType=binary&ratio=1&rotation=0&showTitle=false&size=82687&status=done&style=none&taskId=u6278e4a6-1bbe-4747-9d80-753ff74157e&title=&width=694)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683533107726-d3727cc8-3627-4cf8-8bfd-77f972544187.png#averageHue=%23ddd5cc&clientId=u05b937fa-89df-4&from=paste&height=31&id=u09613cf9&originHeight=31&originWidth=1135&originalType=binary&ratio=1&rotation=0&showTitle=false&size=21185&status=done&style=none&taskId=ub5cc470f-c4a7-431a-9335-1da22dd255e&title=&width=1135)
## 响应json数据（POJO对象转json）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683533218089-6b37846d-7896-4376-9f77-4b6ec624ecd5.png#averageHue=%23fcfcfa&clientId=u05b937fa-89df-4&from=paste&height=304&id=u0db04df4&originHeight=304&originWidth=956&originalType=binary&ratio=1&rotation=0&showTitle=false&size=102050&status=done&style=none&taskId=ud97d9473-7db7-4326-a49a-13da3d9a045&title=&width=956)
## 响应json数据（POJO集合对象转json）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683533293898-16061198-832a-4c00-a271-21e3c3fffbd3.png#averageHue=%23eceae2&clientId=u05b937fa-89df-4&from=paste&height=564&id=uc7f8d96e&originHeight=564&originWidth=560&originalType=binary&ratio=1&rotation=0&showTitle=false&size=184575&status=done&style=none&taskId=ua38e58d1-1742-4029-8e9a-921b85cec09&title=&width=560)
## 注解
### @ResponseBody
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683533461448-7e248871-4f70-41e2-8435-dd20f01b4514.png#averageHue=%23fcfbf0&clientId=u05b937fa-89df-4&from=paste&height=718&id=udbe7a3ea&originHeight=718&originWidth=1571&originalType=binary&ratio=1&rotation=0&showTitle=false&size=198709&status=done&style=none&taskId=u5f47edeb-69b8-437f-86e5-ca9f42855b8&title=&width=1571)如果返回值为String类型，则直接返回作为响应体；若返回值为对象类型，则将对象解析为json数据再作为响应体。与日期类型转换不同的是，它不是使用Convert接口进行类型转换，而是使用HttpMessageConverter接口进行转换
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683533635023-696437ec-6e19-437b-a254-344f2160b92b.png#averageHue=%23f7f5db&clientId=u05b937fa-89df-4&from=paste&height=543&id=ud9083ca7&originHeight=543&originWidth=1571&originalType=binary&ratio=1&rotation=0&showTitle=false&size=337747&status=done&style=none&taskId=u863ec4dc-af74-4ad7-ac9c-7f126e4bb0f&title=&width=1571)
# Rest风格
## Rest简介
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683534290049-698dda6b-6c14-4fbf-aaa1-c0cb18b71de6.png#averageHue=%23fcfcfb&clientId=u05b937fa-89df-4&from=paste&height=556&id=u42d201c3&originHeight=556&originWidth=1491&originalType=binary&ratio=1&rotation=0&showTitle=false&size=226614&status=done&style=none&taskId=u1ff9f36a-6e48-4a28-bc5c-58c41c38e1b&title=&width=1491)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683534421342-8c668150-f3c2-450b-a942-764ceca5e00b.png#averageHue=%23f9f8f7&clientId=u05b937fa-89df-4&from=paste&height=487&id=u987bfbf8&originHeight=487&originWidth=1291&originalType=binary&ratio=1&rotation=0&showTitle=false&size=254308&status=done&style=none&taskId=u9724d0a9-e6ef-45bb-b1e3-da46f272d68&title=&width=1291)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683534622179-971bc7fc-a5ca-4149-94d5-de237035b35a.png#averageHue=%23f6f5f4&clientId=u05b937fa-89df-4&from=paste&height=401&id=uffccd178&originHeight=401&originWidth=1575&originalType=binary&ratio=1&rotation=0&showTitle=false&size=155277&status=done&style=none&taskId=u5e938220-223b-4e9f-908a-507d989bf3d&title=&width=1575)
通过路径+请求行为确定操作
## Rest入门案例
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683534839598-021029ab-14a2-459a-b8a4-8bbbc1b9c689.png#averageHue=%23fbfaf6&clientId=u05b937fa-89df-4&from=paste&height=207&id=ubcd8e07f&originHeight=207&originWidth=620&originalType=binary&ratio=1&rotation=0&showTitle=false&size=71410&status=done&style=none&taskId=u2575d0bd-0f4b-4eb9-82bd-523177d63bf&title=&width=620)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683534855881-1ed3566f-0664-487e-9b09-d9a5aa8cb7ab.png#averageHue=%23faf9f6&clientId=u05b937fa-89df-4&from=paste&height=174&id=u022a1b17&originHeight=174&originWidth=650&originalType=binary&ratio=1&rotation=0&showTitle=false&size=69027&status=done&style=none&taskId=u6fa4ed77-99e7-434b-a2c2-7a0bd5c416f&title=&width=650)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683535039604-30de34b8-0134-43fe-b6b0-e1c2fc63420f.png#averageHue=%23f6f6f6&clientId=u05b937fa-89df-4&from=paste&height=72&id=u1fec3551&originHeight=72&originWidth=640&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9464&status=done&style=none&taskId=u1dbec5fa-fbb0-4eeb-9986-d11569bc3a8&title=&width=640)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683535004592-1f9d0445-9261-49b5-8f54-35a2709d3d43.png#averageHue=%23faf9f5&clientId=u05b937fa-89df-4&from=paste&height=192&id=u775c1689&originHeight=192&originWidth=912&originalType=binary&ratio=1&rotation=0&showTitle=false&size=103357&status=done&style=none&taskId=u932a5935-4566-4c17-ad57-8dbbc4f2997&title=&width=912)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683535276325-31fbefc9-670d-44c8-9242-92e933f019c8.png#averageHue=%23faf7dd&clientId=u05b937fa-89df-4&from=paste&height=803&id=u9faf052c&originHeight=803&originWidth=1582&originalType=binary&ratio=1&rotation=0&showTitle=false&size=337302&status=done&style=none&taskId=ubf34d062-dbcb-420e-a1c5-d10eea7ca3e&title=&width=1582)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683535292258-e14f66cd-f4f6-475c-9ae4-1c5d1774b4a4.png#averageHue=%23faf8de&clientId=u05b937fa-89df-4&from=paste&height=382&id=u49af05c4&originHeight=382&originWidth=1589&originalType=binary&ratio=1&rotation=0&showTitle=false&size=175182&status=done&style=none&taskId=ua7bb31ca-7fd5-40a4-9147-92d5960abe6&title=&width=1589)
### 注解
#### @RequestMapping  
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683535336739-3d6d0090-3895-4de7-a3a4-b3fc6577cec1.png#averageHue=%23fbfaf0&clientId=u05b937fa-89df-4&from=paste&height=729&id=u1ebd7705&originHeight=729&originWidth=1549&originalType=binary&ratio=1&rotation=0&showTitle=false&size=308252&status=done&style=none&taskId=u9d3b94d7-8c81-491e-9af7-5a08e35977d&title=&width=1549)
#### @PathVariable  
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683535365780-d97e5703-cc73-49ee-8e1a-70c49ecc63df.png#averageHue=%23fbf9ec&clientId=u05b937fa-89df-4&from=paste&height=605&id=ud8e81aaf&originHeight=605&originWidth=1572&originalType=binary&ratio=1&rotation=0&showTitle=false&size=295010&status=done&style=none&taskId=ubbd6447c-f8ab-47d6-8478-0bb80a0b382&title=&width=1572)
#### @RequestBody、@RequestParam及@PathVariable的区别
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683535924218-1ab6d3fa-7ccf-4a77-8b7d-851a5da19095.png#averageHue=%23f9f9f9&clientId=u05b937fa-89df-4&from=paste&height=567&id=u5f457eac&originHeight=567&originWidth=1555&originalType=binary&ratio=1&rotation=0&showTitle=false&size=331637&status=done&style=none&taskId=ud6455ed7-3d59-4f8f-88d9-6e8a4834159&title=&width=1555)
### 
## Rest快速开发
### 代码简化
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683536278819-4e1bf864-919c-4a36-a24b-1d861b7a430b.png#averageHue=%23e8e6d6&clientId=u05b937fa-89df-4&from=paste&height=350&id=BkJ2n&originHeight=350&originWidth=826&originalType=binary&ratio=1&rotation=0&showTitle=false&size=142145&status=done&style=none&taskId=ud7b9520e-73ac-4350-8cfa-3b46fcbe7a1&title=&width=826)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683536339446-7a5ffb49-7b1d-4735-ba31-57e458707040.png#averageHue=%23f1ecdf&clientId=u05b937fa-89df-4&from=paste&height=97&id=KvM26&originHeight=97&originWidth=638&originalType=binary&ratio=1&rotation=0&showTitle=false&size=51758&status=done&style=none&taskId=u82c1bb76-f10b-42ad-b346-5ce3f2a084f&title=&width=638)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683536370307-b8af68f7-dd3c-43b8-8d8d-e3cc2b2d0af8.png#averageHue=%23f2f0e4&clientId=u05b937fa-89df-4&from=paste&height=218&id=CINVj&originHeight=218&originWidth=824&originalType=binary&ratio=1&rotation=0&showTitle=false&size=106895&status=done&style=none&taskId=u01720d0b-4287-4bdc-879c-43bd9466bf6&title=&width=824)
## 注解
### @RestController  
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683536483842-4b663baa-ef82-4c67-aba8-eaad4f69bf8d.png#averageHue=%23fbfbf3&clientId=u05b937fa-89df-4&from=paste&height=563&id=u12866f19&originHeight=563&originWidth=1574&originalType=binary&ratio=1&rotation=0&showTitle=false&size=216010&status=done&style=none&taskId=ubb4c6db9-999e-49da-b553-f08e62b84f3&title=&width=1574)
### @GetMapping  
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683536511411-4f723087-b89c-4d9d-bf26-2c765830499e.png#averageHue=%23fbfaef&clientId=u05b937fa-89df-4&from=paste&height=657&id=u51ce4b27&originHeight=657&originWidth=1572&originalType=binary&ratio=1&rotation=0&showTitle=false&size=343568&status=done&style=none&taskId=ueadb2fb0-0679-43a4-8d73-2ac216a87c0&title=&width=1572)
## 基于Restful的页面数据交互
**问题：如何放行非SpringMVC的请求？**配置静态资源处理器，将请求映射到相应的静态资源。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683542503553-6d84dfa9-8aa9-4027-92c1-d82f648834bb.png#averageHue=%23fbfaf7&clientId=u05b937fa-89df-4&from=paste&height=325&id=u8f5b3417&originHeight=325&originWidth=817&originalType=binary&ratio=1&rotation=0&showTitle=false&size=50050&status=done&style=none&taskId=u3f2865f6-a752-4ca5-aa79-15d1a48b67d&title=&width=817)
另外，需要注意，声明SpringMvcSupport类后，需要在SpringMvcConfig中进行配置
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683542706616-5a813b15-75b3-4607-a127-18b359e7b139.png#averageHue=%23fdfcfa&clientId=u05b937fa-89df-4&from=paste&height=222&id=uda5664eb&originHeight=222&originWidth=537&originalType=binary&ratio=1&rotation=0&showTitle=false&size=15217&status=done&style=none&taskId=udda97874-f777-434b-98cf-d64bd612b15&title=&width=537)
经过上述设置后，放在webspp下的静态资源即可正常访问
**问题：Pojo类不设置无参构造器将报错**在某些情况下，可能会遇到以下错误：

1. 反射实例化：当使用反射机制实例化一个类时，如果该类没有显式定义无参构造器，那么使用 Class 的 **newInstance()** 方法将会抛出 **InstantiationException** 异常。
2. 框架要求无参构造器：某些框架或库要求类必须具有无参构造器，以便能够通过反射机制实例化对象。如果类没有无参构造器，则可能会导致框架或库无法正常工作或抛出异常。

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683543729071-4191e821-0cae-49d3-9cc9-8fc96fca8e48.png#averageHue=%23f9f6dd&clientId=u05b937fa-89df-4&from=paste&height=844&id=u30c42c0e&originHeight=844&originWidth=1606&originalType=binary&ratio=1&rotation=0&showTitle=false&size=511917&status=done&style=none&taskId=u565b401c-02c6-4276-97ab-a84276de716&title=&width=1606)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683543769663-4adf84d1-69a4-4020-8294-34acfd355b41.png#averageHue=%23f7f6dd&clientId=u05b937fa-89df-4&from=paste&height=589&id=ud3db5a40&originHeight=589&originWidth=1563&originalType=binary&ratio=1&rotation=0&showTitle=false&size=421647&status=done&style=none&taskId=ua0f5a4d1-30f0-4ac2-8431-54f4f26f7fe&title=&width=1563)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683543792326-e779dba8-e282-4fc8-928c-27f88b903592.png#averageHue=%23fcfae0&clientId=u05b937fa-89df-4&from=paste&height=698&id=u32198540&originHeight=698&originWidth=1563&originalType=binary&ratio=1&rotation=0&showTitle=false&size=170736&status=done&style=none&taskId=ue0053c99-4ef6-4b29-b431-7667ea75b01&title=&width=1563)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683543822705-9d78941a-d7dd-4190-a999-b5cf69340cc4.png#averageHue=%23f7f4f4&clientId=u05b937fa-89df-4&from=paste&height=560&id=u83a6f5b5&originHeight=560&originWidth=1463&originalType=binary&ratio=1&rotation=0&showTitle=false&size=257741&status=done&style=none&taskId=u9e54a19b-9199-49ff-87b4-fb5eda62fa8&title=&width=1463)
# SSM整合
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683544868384-ca04385f-08cb-41dd-ad7a-577d5a599e1b.png#averageHue=%23fbfbfb&clientId=u05b937fa-89df-4&from=paste&height=882&id=u476205cd&originHeight=882&originWidth=1264&originalType=binary&ratio=1&rotation=0&showTitle=false&size=238658&status=done&style=none&taskId=u64a1c21d-73e8-4cc0-814e-b85d5abc582&title=&width=1264)
## 创建工程
### 创建Module
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683545198499-c3688cba-0446-4948-a9c3-0c02d13780c4.png#averageHue=%23f5f5f5&clientId=u05b937fa-89df-4&from=paste&height=401&id=uaa25f2f1&originHeight=825&originWidth=784&originalType=binary&ratio=1&rotation=0&showTitle=false&size=51596&status=done&style=none&taskId=u36178193-675a-456b-a6a5-56b543e86bd&title=&width=381)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683545228666-9cc4218f-85c0-458f-b741-e8f1055a7e25.png#averageHue=%23f5f4f4&clientId=u05b937fa-89df-4&from=paste&height=397&id=u63ba0994&originHeight=449&originWidth=389&originalType=binary&ratio=1&rotation=0&showTitle=false&size=20997&status=done&style=none&taskId=u0875ea45-169a-475e-b072-0571999bd9c&title=&width=344)
### 导入依赖
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683545618945-b4b1b64d-9fb2-4cc6-b7e5-aa59b6269b1e.png#averageHue=%23f9f8f6&clientId=u05b937fa-89df-4&from=paste&height=315&id=u51014c79&originHeight=394&originWidth=442&originalType=binary&ratio=1&rotation=0&showTitle=false&size=32051&status=done&style=none&taskId=ue44bce88-5eea-4c92-8589-508a277c809&title=&width=353)![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683545701755-35677bcc-23ee-4e49-8f68-7d0fe2f19312.png#averageHue=%23fdfdfb&clientId=u05b937fa-89df-4&from=paste&height=237&id=u3d2dab9a&originHeight=317&originWidth=482&originalType=binary&ratio=1&rotation=0&showTitle=false&size=28035&status=done&style=none&taskId=u51b510be-2dc2-40d6-8ae2-832adc13318&title=&width=360)
### 配置tomcat运行环境
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683597916763-db922363-af32-42b4-ab65-bfff96f49bba.png#averageHue=%23f4f4f3&clientId=u05b937fa-89df-4&from=paste&height=674&id=ue5b49c83&originHeight=674&originWidth=1036&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40121&status=done&style=none&taskId=ud4cbd0ef-d41d-4513-b750-eb5fcdcf2dd&title=&width=1036)
## SSM整合
### 整合配置类
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683548140541-6f32163e-750f-4aa2-bbe8-9934ef74296d.png#averageHue=%23faf9f7&clientId=u05b937fa-89df-4&from=paste&height=836&id=u99e28224&originHeight=836&originWidth=1021&originalType=binary&ratio=1&rotation=0&showTitle=false&size=153009&status=done&style=none&taskId=u294b4abc-4b18-4e50-8d41-3c5a7b16b8f&title=&width=1021)
```java
package com.star.config;

import com.alibaba.druid.pool.DruidDataSource;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;

import javax.sql.DataSource;

public class JdbcConfig {

    @Value("${jdbc.driver}")
    private String driver;
    @Value("${jdbc.url}")
    private String url;
    @Value("${jdbc.username}")
    private String username;
    @Value("${jdbc.password}")
    private String password;

    @Bean
    public DataSource dataSource(){
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driver);
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        return dataSource;
    }
}

```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683548151893-7f2cbffb-d4b1-4389-a6f3-0fb81a0bb98d.png#averageHue=%23faf9f7&clientId=u05b937fa-89df-4&from=paste&height=733&id=uc091641c&originHeight=733&originWidth=1141&originalType=binary&ratio=1&rotation=0&showTitle=false&size=135177&status=done&style=none&taskId=u342b899e-8f12-46ee-a190-8cd2869baea&title=&width=1141)
```java
package com.star.config;

import org.apache.ibatis.session.SqlSessionFactory;
import org.mybatis.spring.SqlSessionFactoryBean;
import org.mybatis.spring.mapper.MapperScannerConfigurer;
import org.springframework.context.annotation.Bean;

import javax.sql.DataSource;

public class MybatisConfig {
    @Bean
    public SqlSessionFactoryBean sqlSessionFactory(DataSource dataSource){
        SqlSessionFactoryBean factoryBean = new SqlSessionFactoryBean();
        factoryBean.setDataSource(dataSource);
        factoryBean.setTypeAliasesPackage("com.star.domain");
        return factoryBean;
    }
    @Bean
    public MapperScannerConfigurer mapperScannerConfigurer(){
        MapperScannerConfigurer msc = new MapperScannerConfigurer();
        msc.setBasePackage("com.itheima.dao");
        return msc;
    }
}

```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683548243320-97e6ffd3-ac71-4beb-85c1-a920759b4024.png#averageHue=%23fafaf9&clientId=u05b937fa-89df-4&from=paste&height=758&id=u4bed5fa4&originHeight=758&originWidth=1409&originalType=binary&ratio=1&rotation=0&showTitle=false&size=112916&status=done&style=none&taskId=u67b25afa-6ea9-4143-b2d0-ddb8aaa9b44&title=&width=1409)
```java
package com.star.config;

import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

public class ServleConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }

    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
}

```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683548266817-b191e960-f832-4637-94e0-c3578b7f576b.png#averageHue=%23fbfaf9&clientId=u05b937fa-89df-4&from=paste&height=609&id=u140e39e3&originHeight=609&originWidth=1240&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86421&status=done&style=none&taskId=u17c09a0e-ec3b-4053-a619-8d8a8c12f11&title=&width=1240)
```java
package com.star.config;

import org.springframework.context.annotation.*;
import org.springframework.stereotype.Controller;

@Configuration
@ComponentScan(value = "com.star",
excludeFilters = @ComponentScan.Filter(
        type = FilterType.ANNOTATION,
        classes = Controller.class
)
)
@PropertySource("jdbc.properties")
@Import({JdbcConfig.class,MybatisConfig.class})
public class SpringConfig {
}

```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683548287936-6431ac87-9514-4ee6-9410-3b853d415a44.png#averageHue=%23fbfbfa&clientId=u05b937fa-89df-4&from=paste&height=661&id=ud7e271ba&originHeight=661&originWidth=1308&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78527&status=done&style=none&taskId=u5bf2e0a8-c6e0-4d16-9f8e-a20815eb27e&title=&width=1308)
```java
package com.star.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;

@Configuration
@ComponentScan("com.star.controller")
@EnableWebMvc
public class SpringMvcConfig {

}

```
### 整合各模块
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683549604737-ae0fe5a5-821c-474a-81b6-d12e42ed9fbe.png#averageHue=%23fcfaf8&clientId=u05b937fa-89df-4&from=paste&height=275&id=ud5e6890a&originHeight=275&originWidth=832&originalType=binary&ratio=1&rotation=0&showTitle=false&size=92971&status=done&style=none&taskId=u7f8e48a1-1d01-4378-8d71-e1132b9d262&title=&width=832)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683549653007-fa692bd6-1c40-4e7d-9216-b6f454b3eb71.png#averageHue=%23edeae2&clientId=u05b937fa-89df-4&from=paste&height=450&id=u2f1a69b0&originHeight=450&originWidth=1197&originalType=binary&ratio=1&rotation=0&showTitle=false&size=262369&status=done&style=none&taskId=ua611775b-935d-4639-b2b8-97c3258ecec&title=&width=1197)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683550875950-306ccda7-6a32-4159-8522-8bb0dd062744.png#averageHue=%23f3f3f2&clientId=u05b937fa-89df-4&from=paste&height=783&id=u7ed18488&originHeight=783&originWidth=647&originalType=binary&ratio=1&rotation=0&showTitle=false&size=249948&status=done&style=none&taskId=ue247539d-43d3-4008-817b-a870cc94acf&title=&width=647)
### 测试两阶段
#### 业务层开发完毕
测试业务层功能
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599003087-42bca332-2461-4796-889e-80a47087efb2.png#averageHue=%23fcfaf9&clientId=u05b937fa-89df-4&from=paste&height=721&id=ufb3d1ec5&originHeight=721&originWidth=583&originalType=binary&ratio=1&rotation=0&showTitle=false&size=83630&status=done&style=none&taskId=u2db342d8-4afd-4d55-b138-95830023e6b&title=&width=583)
#### 表现层开发完毕
通过postman工具测试表现层功能
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599057811-5368568d-b39f-496f-b135-d617f66c1860.png#averageHue=%23fcfcfc&clientId=u05b937fa-89df-4&from=paste&height=758&id=ud747118c&originHeight=758&originWidth=884&originalType=binary&ratio=1&rotation=0&showTitle=false&size=43722&status=done&style=none&taskId=u62595627-dd83-43d9-8815-7eca9aa6cc0&title=&width=884)
### 配置事务
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599362389-d2a930b3-fa39-4dfc-b342-4760eedd9916.png#averageHue=%23f9f8f6&clientId=u05b937fa-89df-4&from=paste&height=374&id=u096685df&originHeight=374&originWidth=919&originalType=binary&ratio=1&rotation=0&showTitle=false&size=68196&status=done&style=none&taskId=u00a5bc39-f74c-4581-b21e-5b7d3ed9a1d&title=&width=919)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599409416-e3886494-dbb7-480d-b7c9-e57a900e1cb6.png#averageHue=%23fbfaf8&clientId=u05b937fa-89df-4&from=paste&height=642&id=u1591055e&originHeight=642&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121195&status=done&style=none&taskId=ud95e1fa6-61dd-4fc7-9c6c-e032c9b9c91&title=&width=1200)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599460620-6c5fd48f-7771-44b7-a835-018032ea668f.png#averageHue=%23faf9f8&clientId=u05b937fa-89df-4&from=paste&height=684&id=ud29d5823&originHeight=684&originWidth=1063&originalType=binary&ratio=1&rotation=0&showTitle=false&size=105155&status=done&style=none&taskId=ua9a31a5e-50e3-4259-8da0-6df89350e1f&title=&width=1063)
### 总结
#### Spring 整合Mybatis
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599578025-fa70ec29-cb62-4bf8-8c84-ba2c1c659992.png#averageHue=%23fdfdfd&clientId=u05b937fa-89df-4&from=paste&height=822&id=u4933bcf5&originHeight=822&originWidth=1201&originalType=binary&ratio=1&rotation=0&showTitle=false&size=155520&status=done&style=none&taskId=u6bbc680e-6d1d-459d-8b04-c7d43790b23&title=&width=1201)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599610953-c1592258-696b-4e6d-8e3d-f9d161fedf1a.png#averageHue=%23fcfbf3&clientId=u05b937fa-89df-4&from=paste&height=721&id=u3720f7ea&originHeight=721&originWidth=1661&originalType=binary&ratio=1&rotation=0&showTitle=false&size=261547&status=done&style=none&taskId=u2b216bb6-ee85-495f-bbd1-64604e49a02&title=&width=1661)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599626335-cfd670df-ef30-46fe-9c9b-56aff4743838.png#averageHue=%23faf9e9&clientId=u05b937fa-89df-4&from=paste&height=832&id=ua81ed549&originHeight=832&originWidth=1661&originalType=binary&ratio=1&rotation=0&showTitle=false&size=425473&status=done&style=none&taskId=u5a5ba8a8-304f-48b8-b628-e991e570377&title=&width=1661)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599641715-bca30de2-f454-43c3-bb34-671c62d1be53.png#averageHue=%23fdfcf8&clientId=u05b937fa-89df-4&from=paste&height=719&id=u4432a6d3&originHeight=719&originWidth=1651&originalType=binary&ratio=1&rotation=0&showTitle=false&size=230573&status=done&style=none&taskId=u07e0da72-01d8-4dbf-8c60-59f0e99bc3e&title=&width=1651)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599658894-abf67811-06c2-414f-88f5-fb9a8e41d9d0.png#averageHue=%23f9f8e8&clientId=u05b937fa-89df-4&from=paste&height=822&id=u4b895779&originHeight=822&originWidth=1659&originalType=binary&ratio=1&rotation=0&showTitle=false&size=433087&status=done&style=none&taskId=uea94eaf8-ccfc-43d7-9442-0514454b9d7&title=&width=1659)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599673659-0bcbc2ae-bc9d-45a9-8981-e153ce8e4902.png#averageHue=%23fcfcf4&clientId=u05b937fa-89df-4&from=paste&height=729&id=u2dad9c42&originHeight=729&originWidth=1651&originalType=binary&ratio=1&rotation=0&showTitle=false&size=216165&status=done&style=none&taskId=u17901918-6c6a-4fb8-b5d8-be33426dc60&title=&width=1651)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599691025-4d70b1a8-5eac-47da-85ce-29232b52de9b.png#averageHue=%23fbfaec&clientId=u05b937fa-89df-4&from=paste&height=759&id=u86f5b25d&originHeight=759&originWidth=1648&originalType=binary&ratio=1&rotation=0&showTitle=false&size=395982&status=done&style=none&taskId=u15403d88-f1cd-4f72-a0f8-462f6a12ca2&title=&width=1648)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599703889-396b840e-9637-4a51-9a49-f6238f4298de.png#averageHue=%23fcfbf2&clientId=u05b937fa-89df-4&from=paste&height=721&id=u0d3b8f37&originHeight=721&originWidth=1657&originalType=binary&ratio=1&rotation=0&showTitle=false&size=237923&status=done&style=none&taskId=u79e9b1cb-c7df-41a9-ad06-7547bcdba0f&title=&width=1657)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599717626-aa9e2ec6-0c1e-4668-b9d8-e10c9ac80cf7.png#averageHue=%23faf9ed&clientId=u05b937fa-89df-4&from=paste&height=724&id=u0d2ddcc8&originHeight=724&originWidth=1666&originalType=binary&ratio=1&rotation=0&showTitle=false&size=378554&status=done&style=none&taskId=ufc7be318-d653-4198-ae91-1f3f2ba4fe9&title=&width=1666)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599738941-544691e5-0d32-4e9a-805f-775f11cedf4a.png#averageHue=%23faf9e9&clientId=u05b937fa-89df-4&from=paste&height=813&id=u4ba5f623&originHeight=813&originWidth=1660&originalType=binary&ratio=1&rotation=0&showTitle=false&size=363749&status=done&style=none&taskId=uce4b6592-6df3-4075-af4e-d8788d820af&title=&width=1660)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599764198-eeb2deaf-f31e-40ec-8fb0-a2fc8e074a9d.png#averageHue=%23f9f7e5&clientId=u05b937fa-89df-4&from=paste&height=812&id=ue5306361&originHeight=812&originWidth=1635&originalType=binary&ratio=1&rotation=0&showTitle=false&size=362599&status=done&style=none&taskId=u5576da6f-9e7c-4fd8-8a4f-6d2e800042b&title=&width=1635)
#### Spring整合SpringMVC
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599807121-d2ba41fb-5f33-41a9-a19b-09ad8e5ae5a2.png#averageHue=%23f9f7de&clientId=u05b937fa-89df-4&from=paste&height=652&id=u97003052&originHeight=652&originWidth=1579&originalType=binary&ratio=1&rotation=0&showTitle=false&size=378915&status=done&style=none&taskId=u50ad95a9-c5e6-4972-bf3a-a90326acc9c&title=&width=1579)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599863418-e2f25980-1860-491c-8d34-df1096ad1dd1.png#averageHue=%23fdfcee&clientId=u05b937fa-89df-4&from=paste&height=429&id=u0a2e1bf7&originHeight=429&originWidth=1655&originalType=binary&ratio=1&rotation=0&showTitle=false&size=97065&status=done&style=none&taskId=u36e9abd3-deda-486d-9719-537fddf9184&title=&width=1655)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683599848377-c16116f0-3d09-4f3f-9d0a-b94dae589b0e.png#averageHue=%23fcfadf&clientId=u05b937fa-89df-4&from=paste&height=560&id=u32cd3cfb&originHeight=560&originWidth=1575&originalType=binary&ratio=1&rotation=0&showTitle=false&size=173611&status=done&style=none&taskId=u902d4e9f-51d7-4211-b838-2bb55ef167d&title=&width=1575)
## 表现层数据封装
### 为什么封装？
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683600022733-4fcc6a94-b6dd-42eb-9de2-a62493b6b285.png#averageHue=%23fbfaf3&clientId=u05b937fa-89df-4&from=paste&height=838&id=udd4611b6&originHeight=838&originWidth=1670&originalType=binary&ratio=1&rotation=0&showTitle=false&size=302149&status=done&style=none&taskId=ub4716fd8-a519-4791-aa12-7be11df282e&title=&width=1670)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683600108507-74ad2e6f-ecb8-4888-9986-dd2d1304eec2.png#averageHue=%23fcfaee&clientId=u05b937fa-89df-4&from=paste&height=744&id=u3e09233c&originHeight=744&originWidth=1675&originalType=binary&ratio=1&rotation=0&showTitle=false&size=333003&status=done&style=none&taskId=u4d549d21-a9d4-4ee2-b16b-b94aebe17b2&title=&width=1675)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683600235735-2e1df8fa-427f-4dca-bc14-5eb6a8d29800.png#averageHue=%23fcfcf2&clientId=u05b937fa-89df-4&from=paste&height=686&id=u7e29e4f6&originHeight=686&originWidth=1684&originalType=binary&ratio=1&rotation=0&showTitle=false&size=260376&status=done&style=none&taskId=uae7330ec-735d-40e9-85cd-49c4aa58548&title=&width=1684)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683600294798-8f4e7e03-c10d-4120-b82c-094e1586d58d.png#averageHue=%23fcfbee&clientId=u05b937fa-89df-4&from=paste&height=552&id=u46c09b00&originHeight=552&originWidth=1675&originalType=binary&ratio=1&rotation=0&showTitle=false&size=244688&status=done&style=none&taskId=u5bb202d0-20e1-43a9-bc93-887c6cfcbbc&title=&width=1675)
### 如何封装？
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683600325642-dd3952bf-3f72-467e-986a-10db75f98318.png#averageHue=%23fcfbf3&clientId=u05b937fa-89df-4&from=paste&height=808&id=u0401ff1d&originHeight=808&originWidth=1584&originalType=binary&ratio=1&rotation=0&showTitle=false&size=194543&status=done&style=none&taskId=ub157cfa1-4ad3-4a81-afdf-5d5e77b11b8&title=&width=1584)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683600881276-08640f48-9047-449c-900e-f1eb613d58ce.png#averageHue=%23f9f6de&clientId=u05b937fa-89df-4&from=paste&height=679&id=u799d656c&originHeight=679&originWidth=1562&originalType=binary&ratio=1&rotation=0&showTitle=false&size=393941&status=done&style=none&taskId=uc512e5b7-6530-471d-a688-e9b6b76c890&title=&width=1562)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683600933982-ff701867-dde9-4a35-a7b1-d1ffc43ad228.png#averageHue=%23fbf9de&clientId=u05b937fa-89df-4&from=paste&height=652&id=ud6877389&originHeight=652&originWidth=1590&originalType=binary&ratio=1&rotation=0&showTitle=false&size=291193&status=done&style=none&taskId=u01f8a6f3-8346-4c8f-a4e3-8b2dda41628&title=&width=1590)
## 异常处理器
### 引入
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683601084685-2c3ca48b-9564-4905-bd82-e7fcaf3eec3f.png#averageHue=%23f7f7f7&clientId=u05b937fa-89df-4&from=paste&height=485&id=u935ec32a&originHeight=485&originWidth=1555&originalType=binary&ratio=1&rotation=0&showTitle=false&size=293648&status=done&style=none&taskId=uf5d4774e-4aac-43f4-9aa4-1cb9d2ea2ff&title=&width=1555)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683601168613-49880fa3-e16c-4c23-84fb-20785d9fbc33.png#averageHue=%23f5f4f4&clientId=u05b937fa-89df-4&from=paste&height=352&id=ucf9f6e45&originHeight=352&originWidth=1451&originalType=binary&ratio=1&rotation=0&showTitle=false&size=317016&status=done&style=none&taskId=u6559db78-33f3-4ab7-b7f8-b09f8654c3a&title=&width=1451)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683601565478-03d9a713-6008-4677-b795-ee1b22f5edbd.png#averageHue=%23faf6f5&clientId=u05b937fa-89df-4&from=paste&height=492&id=u44aabe1c&originHeight=492&originWidth=1564&originalType=binary&ratio=1&rotation=0&showTitle=false&size=164093&status=done&style=none&taskId=u951d40ff-70f0-4ad0-bf15-a748427095d&title=&width=1564)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683601639614-fe145f06-27e1-4eb5-abdb-e96d7aba4d91.png#averageHue=%23faf7f6&clientId=u05b937fa-89df-4&from=paste&height=531&id=uefc85b4a&originHeight=531&originWidth=1526&originalType=binary&ratio=1&rotation=0&showTitle=false&size=158590&status=done&style=none&taskId=u6bf00060-e9da-4ac1-9e1b-1795e13f864&title=&width=1526)
### 使用
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683601986757-743fb049-3437-4f03-a788-b40741486909.png#averageHue=%23fbfae8&clientId=u05b937fa-89df-4&from=paste&height=502&id=u3f3f20c9&originHeight=502&originWidth=1557&originalType=binary&ratio=1&rotation=0&showTitle=false&size=167107&status=done&style=none&taskId=u4b9fda2e-2e50-4824-93de-f76db92f241&title=&width=1557)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683602103947-f21c2981-be1d-483a-9cb5-c51907dcc545.png#averageHue=%23fbfbfa&clientId=u05b937fa-89df-4&from=paste&height=514&id=ue59ee5e3&originHeight=514&originWidth=1614&originalType=binary&ratio=1&rotation=0&showTitle=false&size=155116&status=done&style=none&taskId=u6551f5dc-ac64-46ef-8706-8880dbaaee4&title=&width=1614)
### 异常处理方案
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683602234014-98edc9f6-bcc0-48e8-ad6d-36e77e147172.png#averageHue=%23f8f7f7&clientId=u05b937fa-89df-4&from=paste&height=673&id=uadd909e0&originHeight=673&originWidth=1669&originalType=binary&ratio=1&rotation=0&showTitle=false&size=187268&status=done&style=none&taskId=u9d4f335c-ee79-4baa-8579-103175223b2&title=&width=1669)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683602276159-1e9551fc-4545-4fc3-9f85-2f0af577f9fa.png#averageHue=%23f9f3e9&clientId=u05b937fa-89df-4&from=paste&height=686&id=u9a206c82&originHeight=686&originWidth=1634&originalType=binary&ratio=1&rotation=0&showTitle=false&size=271185&status=done&style=none&taskId=ud9692eea-b187-4e2e-b4f1-d4e85343f38&title=&width=1634)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683602302649-8597e11a-9e17-490c-a030-7f3cd9b04a14.png#averageHue=%23fcfbfb&clientId=u05b937fa-89df-4&from=paste&height=441&id=u1c37f0a5&originHeight=441&originWidth=1411&originalType=binary&ratio=1&rotation=0&showTitle=false&size=175220&status=done&style=none&taskId=u92321816-5c85-46ef-bedf-135e315492c&title=&width=1411)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683602353976-1f072e96-78e7-4479-8a4a-dcb7d430a37a.png#averageHue=%23fcfcfc&clientId=u05b937fa-89df-4&from=paste&height=605&id=u8748fca9&originHeight=605&originWidth=1482&originalType=binary&ratio=1&rotation=0&showTitle=false&size=230228&status=done&style=none&taskId=u50390ded-4d7b-4e3e-aa6e-c66ab258a1b&title=&width=1482)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683610263986-aefcf139-5368-4355-a0cf-96cbb3158bba.png#averageHue=%23fbf9e0&clientId=u05b937fa-89df-4&from=paste&height=727&id=u5919f505&originHeight=727&originWidth=1545&originalType=binary&ratio=1&rotation=0&showTitle=false&size=306763&status=done&style=none&taskId=u869c11af-86db-41bc-be8d-5f88670691f&title=&width=1545)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683610280665-72a8a9a0-c0fb-4f5b-b1d7-af5c1d4dbfc5.png#averageHue=%23fbf9e0&clientId=u05b937fa-89df-4&from=paste&height=731&id=u0df4f0fa&originHeight=731&originWidth=1567&originalType=binary&ratio=1&rotation=0&showTitle=false&size=310292&status=done&style=none&taskId=u0a549ad6-c588-41e5-bc1c-0a9d26a8f55&title=&width=1567)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683610299281-c129abfd-a2a0-4a65-936f-77b44d32c394.png#averageHue=%23fcfae1&clientId=u05b937fa-89df-4&from=paste&height=432&id=ud344ea74&originHeight=432&originWidth=1567&originalType=binary&ratio=1&rotation=0&showTitle=false&size=222278&status=done&style=none&taskId=u76ccb6ad-ae42-47cb-896d-4fb31872136&title=&width=1567)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683610322755-7999adb8-55ea-42d2-9a66-adf4bf0516b1.png#averageHue=%23fcfae0&clientId=u05b937fa-89df-4&from=paste&height=615&id=u16cfd64d&originHeight=615&originWidth=1571&originalType=binary&ratio=1&rotation=0&showTitle=false&size=216617&status=done&style=none&taskId=u1603d634-3ebd-433f-8356-0ed30e3e651&title=&width=1571)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683610371905-d7cd59ab-184c-4e7b-a7c2-92851173a238.png#averageHue=%23fdfbec&clientId=u05b937fa-89df-4&from=paste&height=657&id=u161efbf0&originHeight=657&originWidth=1569&originalType=binary&ratio=1&rotation=0&showTitle=false&size=200184&status=done&style=none&taskId=u1956021b-222d-4812-bcfc-7e4ef66eaaa&title=&width=1569)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683610354734-0a79a65d-0607-4a2d-88ee-0de264852ba5.png#averageHue=%23f9f7dd&clientId=u05b937fa-89df-4&from=paste&height=722&id=u6bde361a&originHeight=722&originWidth=1542&originalType=binary&ratio=1&rotation=0&showTitle=false&size=497464&status=done&style=none&taskId=u5d85d0fe-fcb7-482f-afd1-02bd580d0de&title=&width=1542)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683602485997-8bd15613-f055-4841-ac3b-a5af926abf2a.png#averageHue=%23fafaf9&clientId=u05b937fa-89df-4&from=paste&height=654&id=u66cfa993&originHeight=654&originWidth=1304&originalType=binary&ratio=1&rotation=0&showTitle=false&size=255372&status=done&style=none&taskId=u82c1b807-9fa8-4389-8f63-e497d9d8752&title=&width=1304)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683602597998-598f7ba1-749a-439d-8332-4e70bef12d1e.png#averageHue=%23ebe9e2&clientId=u05b937fa-89df-4&from=paste&height=626&id=u2e60f9d6&originHeight=626&originWidth=1369&originalType=binary&ratio=1&rotation=0&showTitle=false&size=402858&status=done&style=none&taskId=u1af48db4-1f9d-4047-ba10-ee92f8ac4f0&title=&width=1369)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683602683391-1c7b3d3d-07f0-416b-9a3f-04037f713ca7.png#averageHue=%23fdfcfa&clientId=u05b937fa-89df-4&from=paste&height=302&id=u3311dc2d&originHeight=302&originWidth=1160&originalType=binary&ratio=1&rotation=0&showTitle=false&size=111239&status=done&style=none&taskId=ue1f9e9cc-e862-428c-af33-6ef5a3877d6&title=&width=1160)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683602811366-1a246459-c6bb-42c3-8919-c7dad8837662.png#averageHue=%23fbfbfa&clientId=u05b937fa-89df-4&from=paste&height=290&id=udd2948bb&originHeight=290&originWidth=1123&originalType=binary&ratio=1&rotation=0&showTitle=false&size=135499&status=done&style=none&taskId=u07c0ebed-e020-4bf4-ba27-6683ccc7736&title=&width=1123)
### 注解
#### @ExceptionHandler  
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683602060349-f1925a98-c51c-4928-8476-2b90fd12f0c3.png#averageHue=%23faf9ed&clientId=u05b937fa-89df-4&from=paste&height=734&id=uece0a2e3&originHeight=734&originWidth=1585&originalType=binary&ratio=1&rotation=0&showTitle=false&size=360045&status=done&style=none&taskId=u8563ee6c-f669-4b44-a355-7e3b6cf75a1&title=&width=1585)
## 项目异常处理方案
## 报错
Error creating bean with name 'resourceHandlerMapping' defined in class path resource [org/springframework/web/servlet/config/annotation/DelegatingWebMvcConfiguration.class]![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683597448309-43eded23-5373-4612-9cc7-af4a67326ae5.png#averageHue=%23faf4f1&clientId=u05b937fa-89df-4&from=paste&height=644&id=ua97ba356&originHeight=644&originWidth=1465&originalType=binary&ratio=1&rotation=0&showTitle=false&size=244076&status=done&style=none&taskId=uad0f5798-ba73-42cd-9a01-b6f7e11fb94&title=&width=1465)
**解决：**
设置精确扫描范围
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683597549662-8964fb38-8c51-4b85-a120-8d95779e9957.png#averageHue=%23f9f8f7&clientId=u05b937fa-89df-4&from=paste&height=533&id=u181b9641&originHeight=533&originWidth=1045&originalType=binary&ratio=1&rotation=0&showTitle=false&size=96867&status=done&style=none&taskId=u8410307a-3648-4e13-97e2-6d82f58a657&title=&width=1045)
Unable to process Jar entry [module-info.class] from Jar [jar:file:/E:/JavaRes/Maven/maven_repository/com/fasterxml/jackson/core/jackson-databind/2.11.4/jackson-databind-2.11.4.jar!/] for annotations![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683598433231-db836987-2d4a-45e3-b294-343c5c1e5a0e.png#averageHue=%23fcf8f5&clientId=u05b937fa-89df-4&from=paste&height=328&id=ude028aca&originHeight=328&originWidth=1658&originalType=binary&ratio=1&rotation=0&showTitle=false&size=77621&status=done&style=none&taskId=u30f6a8f9-0a30-4b1c-a8a3-e2008ab88a2&title=&width=1658)
**解决：**
到报错路径下用解压文件**打开**jar包，删除module.info文件![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683598323125-19522f1a-ea52-436f-a7c5-52d371204bdf.png#averageHue=%23f9f8f7&clientId=u05b937fa-89df-4&from=paste&height=611&id=u020586ca&originHeight=611&originWidth=1272&originalType=binary&ratio=1&rotation=0&showTitle=false&size=93454&status=done&style=none&taskId=udfe939d9-7760-4055-a1b0-3855da4093e&title=&width=1272)
# 拦截器
## 概念
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683634467421-fe0fecab-0bb9-4f05-bf7b-6f8d50949aca.png#averageHue=%23e0e7b6&clientId=ue4e9389d-34fb-4&from=paste&height=744&id=uee13ca22&originHeight=744&originWidth=1657&originalType=binary&ratio=1&rotation=0&showTitle=false&size=312182&status=done&style=none&taskId=uda364fa6-7b62-4a40-985f-46b59cf658b&title=&width=1657)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683634625542-89aac9b4-f4dc-4f14-8b49-ff778604fccf.png#averageHue=%23fbfbfb&clientId=ue4e9389d-34fb-4&from=paste&height=338&id=u4b79c1cb&originHeight=338&originWidth=1162&originalType=binary&ratio=1&rotation=0&showTitle=false&size=112878&status=done&style=none&taskId=u8ccb214b-dade-4bb1-be52-89d6728c7e0&title=&width=1162)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683634642591-dc9509c0-289f-4b69-b21a-f6b2e625539c.png#averageHue=%23f6f5f5&clientId=ue4e9389d-34fb-4&from=paste&height=235&id=u3e9c41e0&originHeight=235&originWidth=1174&originalType=binary&ratio=1&rotation=0&showTitle=false&size=128939&status=done&style=none&taskId=ud14e3ca8-2dc9-4f2f-8115-939877f7053&title=&width=1174)
## 入门案例
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635081359-f26fce24-cf10-4d67-bd6b-8f1b33924895.png#averageHue=%23fbf9e0&clientId=ue4e9389d-34fb-4&from=paste&height=724&id=u68dd81cd&originHeight=724&originWidth=1568&originalType=binary&ratio=1&rotation=0&showTitle=false&size=327920&status=done&style=none&taskId=u840d0637-f661-401b-93f6-133416f21d5&title=&width=1568)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635094129-83096541-46d6-4059-a625-0501a0c0ac00.png#averageHue=%23faf8df&clientId=ue4e9389d-34fb-4&from=paste&height=451&id=u8a8b7296&originHeight=451&originWidth=1593&originalType=binary&ratio=1&rotation=0&showTitle=false&size=208225&status=done&style=none&taskId=uc29daa71-ab1b-4c30-be28-8cfca455039&title=&width=1593)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635110352-973b76ae-6aa4-4e21-a056-7dd63138401f.png#averageHue=%23faf8df&clientId=ue4e9389d-34fb-4&from=paste&height=568&id=uf1b3dab8&originHeight=568&originWidth=1589&originalType=binary&ratio=1&rotation=0&showTitle=false&size=283851&status=done&style=none&taskId=u5317d6b4-1c64-41f9-b72c-6b39c1efbd2&title=&width=1589)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635320357-4dc75710-d4a4-42f6-976f-6cfbbc0dd041.png#averageHue=%23faf8de&clientId=ue4e9389d-34fb-4&from=paste&height=625&id=u5541aff9&originHeight=625&originWidth=1592&originalType=binary&ratio=1&rotation=0&showTitle=false&size=316580&status=done&style=none&taskId=uee78d540-f706-46d4-acaf-f13edcc0dc5&title=&width=1592)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635370522-48255e25-b9a2-49c9-9589-100face711bd.png#averageHue=%23fbf9f8&clientId=ue4e9389d-34fb-4&from=paste&height=872&id=uad83a70f&originHeight=872&originWidth=1750&originalType=binary&ratio=1&rotation=0&showTitle=false&size=203201&status=done&style=none&taskId=ubf3d47d5-ba78-477c-af7a-8825799b4a2&title=&width=1750)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635409461-fab3d54b-8325-4754-93f4-9e2fcf2149bd.png#averageHue=%23fbf9f9&clientId=ue4e9389d-34fb-4&from=paste&height=806&id=u568b7b4f&originHeight=806&originWidth=1544&originalType=binary&ratio=1&rotation=0&showTitle=false&size=217144&status=done&style=none&taskId=ud0859ac0-624f-49d7-8035-5d74d4d5504&title=&width=1544)
## 拦截器参数
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635615556-4aba1fc7-963c-497a-b9db-7d1f7af827d4.png#averageHue=%23fbfbf2&clientId=ue4e9389d-34fb-4&from=paste&height=799&id=u92d48237&originHeight=799&originWidth=1592&originalType=binary&ratio=1&rotation=0&showTitle=false&size=297477&status=done&style=none&taskId=ub6cfe446-61ea-473f-b238-956feea1be3&title=&width=1592)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635647761-be4d0754-10e1-493c-96e3-1db41996c464.png#averageHue=%23faf9ea&clientId=ue4e9389d-34fb-4&from=paste&height=492&id=u967dafec&originHeight=492&originWidth=1570&originalType=binary&ratio=1&rotation=0&showTitle=false&size=217497&status=done&style=none&taskId=ufe19f3bf-9493-49ca-9e36-bf3c7c3672f&title=&width=1570)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635665936-6f33f17a-5730-4532-bb71-2b325e1cf295.png#averageHue=%23fbf9ea&clientId=ue4e9389d-34fb-4&from=paste&height=479&id=ua39e92df&originHeight=479&originWidth=1549&originalType=binary&ratio=1&rotation=0&showTitle=false&size=211867&status=done&style=none&taskId=u04ce1a27-ddd7-451c-a7e0-fe7bafeef25&title=&width=1549)
## 多个拦截器执行顺序
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635918021-48e12678-24ce-4204-9a31-1538512d2723.png#averageHue=%23f7f4f2&clientId=ue4e9389d-34fb-4&from=paste&height=872&id=ufe20e7b0&originHeight=872&originWidth=1604&originalType=binary&ratio=1&rotation=0&showTitle=false&size=365788&status=done&style=none&taskId=ub6aaf82a-e6b1-4c57-aa7d-ef581e587f0&title=&width=1604)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683635963749-99d178d7-e6d5-435f-874b-796633559c90.png#averageHue=%23f7f4f3&clientId=ue4e9389d-34fb-4&from=paste&height=515&id=u08bf66fd&originHeight=515&originWidth=1486&originalType=binary&ratio=1&rotation=0&showTitle=false&size=243186&status=done&style=none&taskId=u2c5c0bf5-f662-452a-a95d-09d8cda7a23&title=&width=1486)
