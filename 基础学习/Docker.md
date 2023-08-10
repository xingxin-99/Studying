# 初识Docker
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683167878465-f3756d84-d455-4fb6-8437-99637333928b.png#averageHue=%23f1f4f1&clientId=u6f21ab87-7e56-4&from=paste&height=837&id=u31062708&originHeight=837&originWidth=1570&originalType=binary&ratio=1&rotation=0&showTitle=false&size=327576&status=done&style=none&taskId=uc9705514-1975-4638-941c-d63d56e433e&title=&width=1570)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683167945058-f384c4f8-147a-4be0-9518-732029a475f1.png#averageHue=%23eff2ef&clientId=u6f21ab87-7e56-4&from=paste&height=609&id=u56f9af32&originHeight=609&originWidth=1501&originalType=binary&ratio=1&rotation=0&showTitle=false&size=289026&status=done&style=none&taskId=u47119f12-c51f-476e-a5ee-fa067c79508&title=&width=1501)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683168042266-e78759f8-4866-4e31-9aa3-e0d78f9395d3.png#averageHue=%23f5f7f4&clientId=u6f21ab87-7e56-4&from=paste&height=748&id=u32022ea5&originHeight=748&originWidth=1290&originalType=binary&ratio=1&rotation=0&showTitle=false&size=322070&status=done&style=none&taskId=u780b70d1-d1b2-46ae-94bf-512932d92f5&title=&width=1290)
总结：如果仅仅把代码打包，那么代码在不同环境下运行可能出现问题（比如开发环境使用JDK8，而测试环境使用JDK7，这样就会可能因为JDK版本不同，而导致代码不能正常运行），因此在打包代码的同时把代码所运行的环境也一并打包，便解决了此问题。而Docker就是装载代码和环境的容器。
## 安装Docker
```shell
# 1、yum 包更新到最新
yum update
# 2、安装需要的软件包， yum-uti1 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的
yum install -y yum-utils device-mapper-persistent-data lvm2
#3、设置yum源
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
# 4、安装docker，出现输入的界面都按 y
yum install -y docker-ce
#5查看docker版本，验证是否验证成功
docker -v
```
## Docker架构
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683173239993-fad0b9fd-fd68-4181-97f7-204f4393a3ed.png#averageHue=%23f1f4f1&clientId=u010e57dd-6025-4&from=paste&height=682&id=u4b0f52c9&originHeight=682&originWidth=1519&originalType=binary&ratio=1&rotation=0&showTitle=false&size=455836&status=done&style=none&taskId=u997c4d0c-23a1-4c48-b0a6-91978164ef0&title=&width=1519)
## 配置Docker镜像加速器
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683173444815-25cb8e9e-f11f-44d9-a5ef-aaac56e71852.png#averageHue=%23f5f8f5&clientId=u010e57dd-6025-4&from=paste&height=675&id=u39bd946a&originHeight=675&originWidth=1578&originalType=binary&ratio=1&rotation=0&showTitle=false&size=322978&status=done&style=none&taskId=uea17788b-40e5-4cf5-ad9f-cde1d2d08ba&title=&width=1578)

- 登录阿里云，打开控制台

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683173723788-f7090821-f7ab-432d-b60e-a1bb6d0e595b.png#averageHue=%23f3f3f1&clientId=u010e57dd-6025-4&from=paste&height=784&id=u86f16d91&originHeight=784&originWidth=1929&originalType=binary&ratio=1&rotation=0&showTitle=false&size=661766&status=done&style=none&taskId=u0d19eff1-3572-4385-b7e9-f0b7297f106&title=&width=1929)

- 在控制台搜索容器镜像服务

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683173790712-48831c65-aea0-4f39-87b3-8bb6bc4fd338.png#averageHue=%23eeecc2&clientId=u010e57dd-6025-4&from=paste&height=937&id=u24c03fa7&originHeight=937&originWidth=1920&originalType=binary&ratio=1&rotation=0&showTitle=false&size=218897&status=done&style=none&taskId=uc2aa17be-14ee-40f2-b49d-0aa4f4a74a7&title=&width=1920)

- 点击镜像工具中的镜像加速器

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683173886906-a299a89c-8a8f-4d5c-9318-a7c6ae0be828.png#averageHue=%23fcfbf9&clientId=u010e57dd-6025-4&from=paste&height=937&id=u9b5c0d02&originHeight=937&originWidth=1920&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86209&status=done&style=none&taskId=u07f9c3af-327f-40fe-93ab-d8cb498678a&title=&width=1920)
```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://24txfn4g.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

- 复制上述代码到Linux

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683174067852-5697b1e0-c807-4985-b35a-ae8686e1e1cf.png#averageHue=%23264458&clientId=u010e57dd-6025-4&from=paste&height=216&id=u2d37984a&originHeight=216&originWidth=839&originalType=binary&ratio=1&rotation=0&showTitle=false&size=203636&status=done&style=none&taskId=ua07a823b-feba-4202-90dc-c09e7b36f3c&title=&width=839)

- 检测镜像是否配置成功：`cat /etc/docker/daemon.json`

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683174437845-5664409a-377b-4225-acbb-3806bec3696c.png#averageHue=%23223c51&clientId=u010e57dd-6025-4&from=paste&height=81&id=u8f98161f&originHeight=81&originWidth=592&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57113&status=done&style=none&taskId=u08d68d9d-bcc5-4646-91e2-2c8d93dad83&title=&width=592)
# Docker命令
## Docker服务相关命令
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683174536442-2fbe66e4-e4a8-4b18-be96-ef18f74856ba.png#averageHue=%23f5f8f5&clientId=u010e57dd-6025-4&from=paste&height=700&id=udd109a79&originHeight=700&originWidth=1373&originalType=binary&ratio=1&rotation=0&showTitle=false&size=282279&status=done&style=none&taskId=u4516284b-51b6-4349-a75e-afdef4a5ae9&title=&width=1373)
启动docker：`systemctl start docker`
查看docker状态：`systemctl status docker`
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683174982763-536d2ae8-683c-4980-8b42-0568a4f5e698.png#averageHue=%23264358&clientId=u010e57dd-6025-4&from=paste&height=425&id=ub13639d2&originHeight=425&originWidth=784&originalType=binary&ratio=1&rotation=0&showTitle=false&size=462805&status=done&style=none&taskId=ub8a7c308-3438-4faf-b5e8-ce03fcff008&title=&width=784)
停止docker：`systemctl stop docker`
重启docker：`systemctl restart  docker`
开机自动启动docker：`systemctl enable docker`
## Docker镜像相关命令
镜像 = 软件 + 软件的环境，通过相应的镜像可以创建对应的容器，因此软件就自动有了
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683175045615-1fb06865-f325-482f-bd9c-3031cd2f8d48.png#averageHue=%23f6f9f6&clientId=u010e57dd-6025-4&from=paste&height=710&id=ub9d5836f&originHeight=710&originWidth=1386&originalType=binary&ratio=1&rotation=0&showTitle=false&size=237376&status=done&style=none&taskId=ue7af0570-54fe-44d2-8ce2-45d9f37d788&title=&width=1386)
查看镜像：`docker images`
搜索镜像：`docker search 镜像名称`
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683175393778-13067d8f-83ea-42d4-a4f7-016e8b2547b9.png#averageHue=%23264358&clientId=u010e57dd-6025-4&from=paste&height=618&id=ufe4210aa&originHeight=618&originWidth=808&originalType=binary&ratio=1&rotation=0&showTitle=false&size=536141&status=done&style=none&taskId=u12b93ed4-a0c1-483d-8c09-2afe7febdf4&title=&width=808)
下载镜像：
`docker pull 镜像名称`（最新）
`docker pull 镜像名称:版本号` （对应版本）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683175478783-2f85ce79-0be4-4158-9809-73fc557ea7fc.png#averageHue=%231f374b&clientId=u010e57dd-6025-4&from=paste&height=226&id=ufda6391b&originHeight=226&originWidth=618&originalType=binary&ratio=1&rotation=0&showTitle=false&size=191263&status=done&style=none&taskId=u7e07acae-9ec0-4259-b709-e4f5e65d771&title=&width=618)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683175502253-655a0cf8-73cb-40f4-85c9-bb12abcddf50.png#averageHue=%23192d40&clientId=u010e57dd-6025-4&from=paste&height=60&id=ub49a94a7&originHeight=60&originWidth=470&originalType=binary&ratio=1&rotation=0&showTitle=false&size=34680&status=done&style=none&taskId=u46ba4076-6c9b-41f6-a4ac-58987593d39&title=&width=470)
如何查询对应镜像的版本都有哪些？[hub.docker.com](https://hub.docker.com)

- 搜索镜像名称

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683176184915-9be6caf2-3d81-414e-9dff-9fc8b75ac786.png#averageHue=%23e8fefd&clientId=u010e57dd-6025-4&from=paste&height=449&id=BwBYC&originHeight=449&originWidth=1613&originalType=binary&ratio=1&rotation=0&showTitle=false&size=172002&status=done&style=none&taskId=u97dec0bf-e156-4de6-a3c4-427a1d8772e&title=&width=1613)

- 对应版本

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683176210847-8a3b8838-85f9-4937-ada1-e63dd6580a78.png#averageHue=%23fdfcfc&clientId=u010e57dd-6025-4&from=paste&height=840&id=TX8En&originHeight=840&originWidth=863&originalType=binary&ratio=1&rotation=0&showTitle=false&size=94944&status=done&style=none&taskId=uffd67d64-61a9-412e-ba64-047e6fa96b2&title=&width=863)
删除镜像：
`docker rmi 镜像id`
`docker rmi 镜像名称:版本号`
删除所有镜像：`docker rmi `docker images -q``
获取所有镜像的id：`docker images -q`
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683176593936-daa8d4b4-18c6-4c8a-b027-714a1ceb2f1f.png#averageHue=%23192c3f&clientId=u010e57dd-6025-4&from=paste&height=43&id=u888171c4&originHeight=43&originWidth=403&originalType=binary&ratio=1&rotation=0&showTitle=false&size=21632&status=done&style=none&taskId=u1009839e-653e-4a1f-9fa3-abdcd491ae3&title=&width=403)
## Docker容器相关命令
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683176716822-a76f79d1-3755-41c5-ae65-410f1a3aa4f4.png#averageHue=%23f5f8f5&clientId=u010e57dd-6025-4&from=paste&height=694&id=u8a855e55&originHeight=694&originWidth=1295&originalType=binary&ratio=1&rotation=0&showTitle=false&size=278206&status=done&style=none&taskId=u10ef3325-84b1-4f62-8920-eef5f52c2b4&title=&width=1295)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683177419654-0b53a417-9ff7-4ef6-9e35-c49fa71005f4.png#averageHue=%23f2f5f2&clientId=u010e57dd-6025-4&from=paste&height=558&id=ue0cc6be3&originHeight=558&originWidth=1471&originalType=binary&ratio=1&rotation=0&showTitle=false&size=265071&status=done&style=none&taskId=u69ae5089-9086-4df8-8e57-1ddf0e0cd39&title=&width=1471)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683178412526-bfac50b0-c528-4353-a10a-ca087ef284aa.png#averageHue=%23eef7f7&clientId=u010e57dd-6025-4&from=paste&height=583&id=u55bacf5b&originHeight=583&originWidth=1311&originalType=binary&ratio=1&rotation=0&showTitle=false&size=159952&status=done&style=none&taskId=u626af1bd-8c9e-4e39-a0e5-c8177c7d316&title=&width=1311)
**创建容器：**`docker -it --name=容器名字 镜像名称:版本号 /bin/bash`
-i：一直运行（没有客户端运行容器也一直保持运行）
-t：分配伪终端
--name=：起名字
指定镜像及版本
/bin/bash：进入容器的初始化指令
使用-it的特点：创建后立马进入容器，exit退出后立马关闭容器
-id：创建后不会立马进入容器，需要输入特定指令后才会进入容器，退出后不会立即关闭容器
特定指令：`docker exec -it 容器名字 /bin/bash`
**退出容器：**`exit`
**查看正在运行的容器：**`docker ps`
-a：查看正在运行以及历史运行的容器
**停止容器：**`docker stop 容器名称`
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683177980503-1f11b681-3c43-4957-9fe0-96096332f466.png#averageHue=%231c3346&clientId=u010e57dd-6025-4&from=paste&height=96&id=uec6093ea&originHeight=96&originWidth=572&originalType=binary&ratio=1&rotation=0&showTitle=false&size=72571&status=done&style=none&taskId=u76e952d1-970c-488f-b629-ce784c7900a&title=&width=572)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683178129455-8bae278d-13bd-4627-a504-40b147106130.png#averageHue=%231a2f43&clientId=u010e57dd-6025-4&from=paste&height=57&id=u0b243f8b&originHeight=57&originWidth=830&originalType=binary&ratio=1&rotation=0&showTitle=false&size=50244&status=done&style=none&taskId=u9eb474e4-eba8-44b0-9760-bc555142bd8&title=&width=830)
重新启动容器：`docker start 容器名称`
删除容器：`docker rm 容器名称/容器ID`
删除所有容器：`docker rm `docker ps -aq``
注意：开启的容器不能被删除
查看容器信息：`docker inspect 容器名称`
# Docker容器的数据卷
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683184235359-c27a4c9b-fab0-4b27-9892-93b628771bdc.png#averageHue=%23f4f6f3&clientId=u010e57dd-6025-4&from=paste&height=541&id=ued5c5dad&originHeight=541&originWidth=1055&originalType=binary&ratio=1&rotation=0&showTitle=false&size=146427&status=done&style=none&taskId=u6b430259-35c0-4a0b-ac9a-ac81a618266&title=&width=1055)
## 数据卷概念
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683178688523-6c38ac11-8be0-4640-8594-bbd589821534.png#averageHue=%23eff2ef&clientId=u010e57dd-6025-4&from=paste&height=729&id=u42cb3795&originHeight=729&originWidth=1496&originalType=binary&ratio=1&rotation=0&showTitle=false&size=281585&status=done&style=none&taskId=ub1e1aef8-d990-49bc-be92-1834a96a352&title=&width=1496)
## 配置数据卷
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683178776731-efd4f3e9-3aff-4868-be3f-c4d8e08d0c69.png#averageHue=%23f6f9f6&clientId=u010e57dd-6025-4&from=paste&height=319&id=u55be7bc3&originHeight=319&originWidth=1324&originalType=binary&ratio=1&rotation=0&showTitle=false&size=118130&status=done&style=none&taskId=u823db43f-7a34-48b6-bbf9-72fee10fe20&title=&width=1324)
## 数据卷容器
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683183894989-3845cbfb-6cbd-4b2e-9acc-c49d7ec921dd.png#averageHue=%23f0f3f0&clientId=u010e57dd-6025-4&from=paste&height=717&id=u68cbd0d0&originHeight=717&originWidth=1496&originalType=binary&ratio=1&rotation=0&showTitle=false&size=167765&status=done&style=none&taskId=u2b46da9e-82e1-44e8-aeaf-49d583b6269&title=&width=1496)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683184194052-875a7c37-e3c4-41ba-b0e4-969328cf5c5a.png#averageHue=%23f2f5f2&clientId=u010e57dd-6025-4&from=paste&height=430&id=ufe513a2c&originHeight=430&originWidth=1288&originalType=binary&ratio=1&rotation=0&showTitle=false&size=183433&status=done&style=none&taskId=u3940a940-cf98-4d08-a841-d2ddf2aef33&title=&width=1288)
# Docker应用部署
## MySQL部署
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683184437041-d7b56623-caf5-4895-8a48-4219a12ba57f.png#averageHue=%23f7faf7&clientId=u010e57dd-6025-4&from=paste&height=596&id=u1ee33dc2&originHeight=596&originWidth=1162&originalType=binary&ratio=1&rotation=0&showTitle=false&size=141937&status=done&style=none&taskId=ua7440905-ddc8-4fdd-bae0-7d4887cdbe0&title=&width=1162)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683184517739-da6510ad-00f6-4340-9455-c1742d8aae8f.png#averageHue=%23f4f7f4&clientId=u010e57dd-6025-4&from=paste&height=714&id=u604d6553&originHeight=714&originWidth=1332&originalType=binary&ratio=1&rotation=0&showTitle=false&size=255967&status=done&style=none&taskId=udb55b4cc-f56b-4bea-859c-bd3996e0842&title=&width=1332)
```shell
# 拉取mysql镜像
docker pull mysql:5.6
# 创建mysql目录存储信息
mkdir ~/mysql
cd ~/mysql
#创建容器
docker run -id 
 -p 3307:3306\
 --name=c_mysql\
 -v $PWD/conf:/etc/mysql/conf.d \
 -v $PWD/logs:/logs \
 -v $PWD/data:/var/lib/mysql \
 -e MYSQL_ROOT_PASSWORD=123456 \
 mysql:5.6

# 进入容器
 docker exec -it c_mysql /bin/bash

#进入mysql
mysql -uroot -p123456
```
$PWD :当前目录的路径（即~/mysql）
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683185277789-02ff916a-75d7-4ed2-93ac-d5c7a0db6352.png#averageHue=%23f9fcf9&clientId=u010e57dd-6025-4&from=paste&height=345&id=ub1528851&originHeight=345&originWidth=1145&originalType=binary&ratio=1&rotation=0&showTitle=false&size=271922&status=done&style=none&taskId=u3602944d-ed70-48e4-bc48-ef02742703a&title=&width=1145)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683185710541-971b5b94-231f-4503-803c-c35d8b8fa25f.png#averageHue=%2327465a&clientId=u010e57dd-6025-4&from=paste&height=928&id=u7a10f8b5&originHeight=928&originWidth=873&originalType=binary&ratio=1&rotation=0&showTitle=false&size=951804&status=done&style=none&taskId=u3921a78d-3acc-4345-a6cb-671016f700e&title=&width=873)
使用外部机器测试能否连接上宿主机的mysql
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683186161452-8e3a5277-bb93-4af1-923e-c2cf3a8b8efb.png#averageHue=%23fafafa&clientId=u010e57dd-6025-4&from=paste&height=1043&id=u03ccc360&originHeight=1043&originWidth=1914&originalType=binary&ratio=1&rotation=0&showTitle=false&size=75479&status=done&style=none&taskId=u747766f3-0acf-4133-8b19-c91a200fa69&title=&width=1914)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683186177526-5a5d60c0-66d9-4c9c-95de-80fbf5475a53.png#averageHue=%23fafafa&clientId=u010e57dd-6025-4&from=paste&height=1034&id=u62cbc3b3&originHeight=1034&originWidth=1914&originalType=binary&ratio=1&rotation=0&showTitle=false&size=79767&status=done&style=none&taskId=u657e5ad9-0b27-48cb-80c4-9b9a988bb04&title=&width=1914)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683186231551-43210578-3858-4bf7-91bd-8ba1c03042ce.png#averageHue=%23f8f8f7&clientId=u010e57dd-6025-4&from=paste&height=483&id=u0c1bb0e2&originHeight=483&originWidth=862&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36004&status=done&style=none&taskId=u8d349df4-1804-4e29-a5cb-4bdab548d03&title=&width=862)
## Tomcat部署
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683186712246-af32f3a4-41f9-4a92-bc01-249ffc08b981.png#averageHue=%23f8fbf8&clientId=u010e57dd-6025-4&from=paste&height=633&id=u90d0c825&originHeight=633&originWidth=1405&originalType=binary&ratio=1&rotation=0&showTitle=false&size=135606&status=done&style=none&taskId=ud9a684aa-50c0-48ca-9fd3-d59ecd105d0&title=&width=1405)
```shell
# 创建tomcat目录存储信息
mkdir ~/tomcat
cd ~/tomcat
# 创建tomcat容器
docker run -id --name=c_tomcat \
 -p 8080:8080 \
 -v $PWD:/usr/local/tomcat/webapps \
 tomcat
```
测试访问：把要部署的项目放在宿主机的~/tomcat目录下，通过宿主机的IP地址：端口号+项目路径访问
## Nginx部署
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683187180722-a3b74c7a-a323-49e8-85b2-90275888a418.png#averageHue=%23f8fbf8&clientId=u010e57dd-6025-4&from=paste&height=594&id=u33ec0750&originHeight=594&originWidth=1342&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121709&status=done&style=none&taskId=u1e82c194-b1f6-40dc-b629-92f6806cb3e&title=&width=1342)
```shell
# 在/root目录下创建nginx目录用于存储nginx数据信息
mkdir ~/nginx
cd ~/nginx
mkdir conf
cd conf
# 在~/nginx/conf/下创建nginx.conf文件,粘贴下面内容
vim nginx.conf
```
```shell
user  nginx;
worker_processes  1;
 
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid
 
events {
    worker_connections  1024;
}
 
 
http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;
 
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                     '$status $body_bytes_sent "$http_referer" '
                     '"$http_user_agent" "$http_x_forwarded_for"';
 
    access_log  logs/access.log  main;
 
    sendfile        on;
    #tcp_nopush     on;
 
    #keepalive_timeout  0;
    keepalive_timeout  65;
 
    # gzip  on;
 
    include /etc/nginx/conf.d/*.conf
}
```
```shell
# 创建nginx容器
docker run -id --name=nginx \
 --privileged=true\
 -p 80:80 \
 -v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf \
 -v $PWD/logs:/var/log/nginx \
 -v $PWD/html:/usr/share/nginx/html \
 -d nginx 

```
```shell
# 创建挂载目录
mkdir ~/nginx
mkdir ~/nginx/conf
mkdir ~/nginx/log
mkdir ~/nginx/html

# 生成容器
docker run --name nginx -p 80:80 -d nginx

# 将容器nginx.conf文件复制到宿主机
docker cp nginx:/etc/nginx/nginx.conf ~/nginx/conf/nginx.conf
docker cp nginx:/etc/nginx/conf.d ~/nginx/conf/conf.d
docker cp nginx:/usr/share/nginx/html ~/nginx/

# 直接执行docker rm nginx或者以容器id方式关闭容器
# 找到nginx对应的容器id
docker ps -a
# 关闭该容器
docker stop nginx
# 删除该容器
docker rm nginx
 

docker run \
-p 80:80 \
--name nginx \
-v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf \
-v $PWD/conf/conf.d:/etc/nginx/conf.d \
-v $PWD/log:/var/log/nginx \
-v $PWD/html:/usr/share/nginx/html \
-d nginx:latest
```
访问nginx：IP:端口
## Redis部署
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683188968227-565df79b-ada2-40fb-beb2-8b3236dca571.png#averageHue=%23f8fbf8&clientId=u010e57dd-6025-4&from=paste&height=609&id=udf3fcff0&originHeight=609&originWidth=1361&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121321&status=done&style=none&taskId=ue98cf5f9-5f44-4551-80a4-52f20677216&title=&width=1361)
```shell
 docker run -id --name=c_redis -p 6379:6379 redis

docker run \
-d \
--name redis \
-p 6370:6370 \
--restart unless-stopped \
-v ~/redis/data:/data \
-v ~/redis/conf/redis.conf:/etc/redis/redis.conf \
redis:bullseye 


docker run \
-v /home/star/redis:/usr/local/etc/redis \
-d --name redis\
-p 6379:6379 \
redis \
redis-server /usr/local/etc/redis/redis.conf

docker run -d -it -p 6379:6379 \
-v /home/star/redis:/usr/local/etc/redis \
--name redis \
redis \
redis-server /etc/redis/redis.conf 
```
测试访问：`redis-cli -h 宿主机ip -p 宿主机端口`
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683189529328-47baedd4-d258-425b-a270-1e9216ab578f.png#averageHue=%232e5167&clientId=uff08bf9b-7dee-4&from=paste&height=94&id=u2e85d892&originHeight=94&originWidth=540&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63386&status=done&style=none&taskId=uba440f9e-053b-4008-8d6d-7177a619be7&title=&width=540)
# Dockerfile
## Docker镜像原理
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683189934004-34bf507f-a038-4ddf-884c-29bcbbbfb76d.png#averageHue=%23f5f8f5&clientId=uff08bf9b-7dee-4&from=paste&height=715&id=u1d5cd48a&originHeight=715&originWidth=1433&originalType=binary&ratio=1&rotation=0&showTitle=false&size=327144&status=done&style=none&taskId=u65824283-aa3e-4e03-8e79-6ed93c9816c&title=&width=1433)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683190086777-c5930544-c25d-498d-bfe0-d94bef755b6a.png#averageHue=%23f1f4f1&clientId=uff08bf9b-7dee-4&from=paste&height=643&id=u8000ee54&originHeight=643&originWidth=1498&originalType=binary&ratio=1&rotation=0&showTitle=false&size=270627&status=done&style=none&taskId=uf5e4b9bd-8901-4a92-ad8c-5d7b4e22188&title=&width=1498)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683190332181-cce121b3-be3d-4b1f-9bf3-9312f6af43f8.png#averageHue=%23eaeee8&clientId=uff08bf9b-7dee-4&from=paste&height=703&id=u878029ec&originHeight=703&originWidth=1508&originalType=binary&ratio=1&rotation=0&showTitle=false&size=509565&status=done&style=none&taskId=u7bf5ead1-67cf-4b74-b724-d6acfe32ae6&title=&width=1508)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683190411457-7bb53b4a-2930-4849-b088-aab0f8ef7cb7.png#averageHue=%23eff2ef&clientId=uff08bf9b-7dee-4&from=paste&height=380&id=u0f53abc1&originHeight=380&originWidth=1467&originalType=binary&ratio=1&rotation=0&showTitle=false&size=237376&status=done&style=none&taskId=u0a7078d7-b33a-4073-ae07-454eb7cc8ae&title=&width=1467)
### 镜像制作
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683190671240-aa0fb661-6777-4423-80e6-b2bb36856e85.png#averageHue=%23f2f6f1&clientId=uff08bf9b-7dee-4&from=paste&height=758&id=u26200d01&originHeight=758&originWidth=1531&originalType=binary&ratio=1&rotation=0&showTitle=false&size=351953&status=done&style=none&taskId=u2cf02452-9290-4781-8ab7-13c96f2f6c9&title=&width=1531)
通过commit将容器转为镜像，挂载的文件（即数据卷中的数据）不会保存到目录中，但是在容器中本身创建的文件存在
## Dockerfile概念及作用
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683191051160-c8b152a2-4ebf-4131-a652-36aaa5d314bb.png#averageHue=%23e9ece9&clientId=uff08bf9b-7dee-4&from=paste&height=606&id=u43087e91&originHeight=606&originWidth=1549&originalType=binary&ratio=1&rotation=0&showTitle=false&size=352649&status=done&style=none&taskId=ue9608a55-efb4-4ac7-84b8-4387afcda6d&title=&width=1549)
## Dockerfile关键字
## 案例
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683193730791-79f01c04-05bd-4c5b-97c4-5a26d41082c3.png#averageHue=%23f6f9f6&clientId=uff08bf9b-7dee-4&from=paste&height=689&id=u8128f88a&originHeight=689&originWidth=1390&originalType=binary&ratio=1&rotation=0&showTitle=false&size=222020&status=done&style=none&taskId=u7801bd73-0618-4ae2-b6c3-7e07f0d9adb&title=&width=1390)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683194539823-900c0c75-f45f-488a-89b8-dde130bc70d0.png#averageHue=%23f6f9f6&clientId=uff08bf9b-7dee-4&from=paste&height=663&id=u4ce6e2ee&originHeight=663&originWidth=1273&originalType=binary&ratio=1&rotation=0&showTitle=false&size=208944&status=done&style=none&taskId=u9ca89596-7b30-4576-88b3-da23857023f&title=&width=1273)
# Docker服务编排
## 服务编排概念
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683194856359-118a0998-a1d9-45ba-b2ba-05c52326d7f9.png#averageHue=%23f4f7f4&clientId=uff08bf9b-7dee-4&from=paste&height=488&id=u0e251c07&originHeight=488&originWidth=1430&originalType=binary&ratio=1&rotation=0&showTitle=false&size=169630&status=done&style=none&taskId=u46f20a9e-6924-4099-a1ef-a65440f67e0&title=&width=1430)
## Docker Compose
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683194979970-69fb6737-6d7e-4b2b-8511-c87b493616b7.png#averageHue=%23f2f5f2&clientId=uff08bf9b-7dee-4&from=paste&height=702&id=u4e8586b5&originHeight=702&originWidth=1390&originalType=binary&ratio=1&rotation=0&showTitle=false&size=247960&status=done&style=none&taskId=ub7551609-c777-43da-911d-9ed0616175d&title=&width=1390)
## 安装
```shell
#安装Docker Compose
curl -L "https://github.com/docker/compose/releases/download/1.29.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
#添加文件可执行权限
chmod +x /usr/local/bin/docker-compose
#查看版本信息
docker-compose --version
#卸载Docker Compose
rm /usr/local/bin/docker-compose
```
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683196090386-3913e8f7-5418-474d-9ffc-bcae2cd0ac6f.png#averageHue=%23f3f7f5&clientId=uff08bf9b-7dee-4&from=paste&height=769&id=u0acec525&originHeight=769&originWidth=1158&originalType=binary&ratio=1&rotation=0&showTitle=false&size=205199&status=done&style=none&taskId=u212d09c3-344c-4c6a-8486-e0ffd6c52e4&title=&width=1158)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1683196302776-0143e1dc-1496-42f8-85db-afc0fbed63eb.png#averageHue=%23f7faf7&clientId=uff08bf9b-7dee-4&from=paste&height=709&id=ua8cc3341&originHeight=709&originWidth=1213&originalType=binary&ratio=1&rotation=0&showTitle=false&size=155829&status=done&style=none&taskId=uf6568975-c343-4a4a-9cc9-2b551de57a6&title=&width=1213)
# Docker私有仓库
P25-P28未看
