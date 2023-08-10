# 一、Mybatis概述
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1680487655144-40ceb047-3022-4026-bbf3-cda45164060f.jpeg)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1680437065377-d99edf14-e83c-486a-88e0-9bdb41372a58.png#averageHue=%23f9f5f4&clientId=ucc48753e-37e5-4&from=paste&height=660&id=ucb962f66&originHeight=660&originWidth=1625&originalType=binary&ratio=1&rotation=0&showTitle=false&size=496330&status=done&style=none&taskId=u1c93fe35-70ac-4db2-8271-a0d3fb76e3f&title=&width=1625)
# 二、Mybatis入门程序
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1680500855072-ee792ea4-2e94-4dc3-b7b8-5a44922f5a7f.jpeg)
maven中为什么放在resource目录下的资源，等于放在类的根路径下在 Maven 项目中，src/main/resources 目录下的资源文件会被打包进生成的 Jar 或 War 包中，并放在类路径的根目录下。这是因为 Maven 在构建项目时会把 src/main/resources 目录作为类路径的一部分，所以所有放在这个目录下的文件都会被打包进去。
在 Java 项目中，类路径指的是 JVM 用来搜索类和资源文件的路径。类路径的根目录是指能够直接被 JVM 搜索到的目录，这个目录下的文件都可以直接用 ClassLoader 加载。在 Maven 项目中，src/main/resources 目录中的文件就是放在这个根目录下的。
因此，如果我们把某个资源文件放在 src/main/resources 目录下，它就相当于放在了类路径的根目录下，可以直接通过 ClassLoader 加载，无需指定路径。这也是 Maven 中推荐的一种资源文件的组织方式，方便我们在项目中访问和使用这些文件。
```java
public class mybatisTest {
    public static void main(String[] args) {
        SqlSession sqlSession=null;
        try {
            SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
            InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
            SqlSessionFactory sqlSessionFactory =  sqlSessionFactoryBuilder.build(is);
            sqlSession  =sqlSessionFactory.openSession();
            int count = sqlSession.insert("car_insert");
            System.out.println(count);
            sqlSession.commit();
        } catch (IOException e) {
            if(sqlSession!=null){
                sqlSession.rollback();
            }
            throw new RuntimeException(e);
        }finally {
            if(sqlSession!=null){
                sqlSession.close();
            }
        }
    }
}
```
##  Junit介绍
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1680506335553-68c40a50-1f3c-4b52-ad95-a8a6ad5a19d3.jpeg)
```java
public class MathService{
    public int sum(int a, int b){
        return a+b;
    }
}
    
```
```java
public class MathServiceTest{
    MathService mathService = new MathService();
    @Test
    public void Testsum(){
        int actual =  mathService.sum(1,2);
        int expected = 3;
        Assert.assertEquals(expected,actual);
    }
}
```
## 日志框架
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1680506472504-c1acdd8c-c4b7-4411-aca6-655fb1f9153d.jpeg)
```xml
<settings>
  <setting name="logImpl" value="STDOUT_LOGGING" />
</settings>
```
## Mybatis工具类
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1680508228437-3158357f-aeb1-4a2b-abd1-80e25eea0d32.jpeg)
```java
public class mybatisUtil {
    private mybatisUtil(){
    }
    private static SqlSessionFactory sqlSessionFactory;
    static {
        try {
            SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
            sqlSessionFactory = sqlSessionFactoryBuilder.build(Resources.getResourceAsStream("mybatis-config.xml"));
        } catch (IOException e) {
            throw new RuntimeException(e);
        }

    }
    public static SqlSession openSession(){
        return sqlSessionFactory.openSession();
    }
    
}

```
# 三、使用Mybatis完成CRUD
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1680517974389-0d8347e0-c9a4-413b-a0f3-84d0c88aed54.jpeg)
```xml
<mapper namespace="com.star.mybatis">
  <insert id="car_insert">
    insert into t_car(id,car_num,brand,guide_price,produce_time,car_type)
    values (null,#{carNum},#{brand},#{guidePrice},#{produceTime},#{carType})
  </insert>

  <delete id="car_delete">
    delete from t_car where id=#{i}
  </delete>

  <select id="car_select" resultType="com.star.mybatis.introduction.pojo.Car">
    select * from t_car where id=#{id}
  </select>

  <select id="car_selectall" resultType="com.star.mybatis.introduction.pojo.Car">
    select * from t_car
  </select>
</mapper>
```
```java
public class mybatisTest {
    @Test
    public void deletetest(){
        SqlSession sqlSession = mybatisUtil.openSession();
        int count = sqlSession.delete("car_delete",6);
        System.out.println(count);
        sqlSession.commit();
        sqlSession.close();
    }
    @Test
    public void testInsert(){
        Car car = new Car(null,"001","长安",325.00,"2023-04-03","燃油");
        SqlSession sqlSession = mybatisUtil.openSession();
        int count = sqlSession.insert("car_insert",car);
        System.out.println(count);
        sqlSession.commit();
        sqlSession.close();
    }

    @Test
    public void testSelect(){
        SqlSession sqlSession = mybatisUtil.openSession();
        Car car = sqlSession.selectOne("car_select",8);
        System.out.println(car);
    }

    @Test
    public void testSelectAll(){
        SqlSession sqlSession = mybatisUtil.openSession();
        List<Car> cars = sqlSession.selectList("car_selectall");
        cars.forEach(car -> System.out.println(car));

    }
}
```
# 四、Mybatis核心配置文件详解
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1680523257682-8a2d4943-5ab5-4994-8f0b-b8c3234c84ae.jpeg)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1680522258950-c634a153-003f-4159-8076-ff0808bec404.png#averageHue=%23fdfdfb&clientId=ued7fb34b-26a2-4&from=paste&height=453&id=u1c6a1cad&originHeight=453&originWidth=711&originalType=binary&ratio=1&rotation=0&showTitle=false&size=68305&status=done&style=none&taskId=u1d299d85-ebac-4a07-850b-a84c939615f&title=&width=711)
# 五、在WEB中应用Mybatis
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1680612788721-fc4c90df-db3e-40a4-ab04-e8f0c7560300.jpeg)
方法作用域方法作用域是指变量、常量和对象在方法中的可见性和生命周期。在方法内部声明的变量和常量只在方法内部可见，当方法执行结束时，它们也随之消失。对象的作用域可以超出方法，例如一个方法返回一个对象，这个对象在方法外部也可以被使用，直到它被垃圾回收器回收。方法作用域的一个重要特点是，方法内部的变量名或参数名可以与类的成员变量名或参数名相同，但是方法内部的变量或参数会覆盖类的成员变量或参数，直到方法执行结束。
应用作用域应用作用域是指对象的生命周期与应用程序的生命周期相同，即在应用程序启动时创建，在应用程序关闭时销毁。在Spring框架中，应用作用域的对象通常使用单例模式创建。在应用作用域下创建的对象可以在整个应用程序中共享，因此在多个地方使用同一个对象可以提高程序的性能。例如，在Web应用程序中，可以在应用作用域下创建一个共享的数据源对象，以便多个线程共享这个对象，避免了频繁创建和销毁数据源对象的开销。
请求作用域请求作用域是指在一次 HTTP 请求的处理过程中所创建的对象的作用域。它的生命周期是从请求的开始到响应的结束。在一个 HTTP 请求中，通过 **HttpServletRequest** 对象可以获取请求作用域，可以将对象存放在请求作用域中，然后在整个请求处理过程中共享这些对象。通常情况下，请求作用域可以用于在不同的页面之间传递数据。
为什么SqlSessionFactory的作用域为应用作用域MyBatis中的**SqlSessionFactory**是一个重量级的对象，主要负责创建和管理**SqlSession**，其创建过程包含了加载配置文件、解析映射文件、创建数据库连接等操作，因此在创建**SqlSessionFactory**对象时会耗费较多的资源和时间。而且，一个**SqlSessionFactory**对象一般情况下只需要创建一次，并在应用生命周期内持续使用，因此将其作用域设置为应用作用域是比较合适的。
如果将**SqlSessionFactory**的作用域设置为方法或请求作用域，那么每次执行操作都需要重新创建和销毁**SqlSessionFactory**对象，会导致不必要的资源浪费和性能下降。而将其作用域设置为会话作用域也不太合适，因为**SqlSessionFactory**是线程安全的，多个线程可以共享同一个**SqlSessionFactory**对象，因此在会话作用域中可能会造成不必要的资源浪费和线程安全问题。
为什么SqlSession的作用域为请求作用域在使用 MyBatis 进行数据库操作时，每个 SqlSession 都代表了一次对数据库的操作会话。通常情况下，一个请求需要操作数据库多次，因此需要多次创建 SqlSession 对象。由于 SqlSession 是非线程安全的，每次创建一个 SqlSession 对象实例既需要时间又占用内存，所以为了更好地控制资源的开销，将 SqlSession 的作用域设置为请求作用域是比较合适的选择。
将 SqlSession 的作用域设置为请求作用域可以保证每个请求都能获取到一个独立的 SqlSession 实例，避免了线程安全问题和并发访问的冲突。同时，由于每个 SqlSession 对象实例只存在于请求过程中，不会长时间占用内存，能够有效地避免内存泄露的问题，提升了应用程序的稳定性和性能。
# 六、使用javassist生成类
# 七、MyBatis中接口代理机制及使用
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1680779380963-dd2fa5fd-6722-4740-87a9-5e51f9ac3d37.jpeg)
# 八、Mybatis的小技巧
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1680852662243-4d469fdc-96b1-48be-9108-4dccb512a3bd.jpeg)
# 九、Mybatis参数处理
# 十、Mybatis查询语句专题
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1681024141004-771be03d-37b8-4b01-bd6f-af9f435b370f.jpeg)
# 十一、动态SQL 
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1681115128363-72f3157f-9b9d-43e8-a88d-593267156068.jpeg)
# 十一、Mybatis高级映射及延迟加载
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1681130838712-10994ee4-d61e-4114-b77d-47f42a16195f.jpeg)
# 十二、Mybatis缓存
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681197006556-164a5e9b-2298-4ee5-8507-0dae4f5f7172.png#averageHue=%23f8f4f3&clientId=u76eb8fc0-6be5-4&from=paste&height=638&id=u725957cb&originHeight=638&originWidth=1603&originalType=binary&ratio=1&rotation=0&showTitle=false&size=424722&status=done&style=none&taskId=u1ea3d78d-709c-49bb-9da4-b352ba39b39&title=&width=1603)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681197647797-ccea69f2-0e10-48e0-98fe-2327e47f459f.png#averageHue=%232c2c2b&clientId=u76eb8fc0-6be5-4&from=paste&height=263&id=u9a253cd4&originHeight=263&originWidth=1290&originalType=binary&ratio=1&rotation=0&showTitle=false&size=113253&status=done&style=none&taskId=u7e38d526-1771-42ba-95b3-205bf5fd78c&title=&width=1290)
# 十三、Mybatis逆向工程
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1681214819064-04b2f22b-a4e2-443d-9e99-ef4a701de267.jpeg)
# 十四、Mybatis分页插件
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1681216603928-190603d7-c9f4-45a9-a951-fe3428581d4f.jpeg)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32637015/1681215434369-8709d737-e76d-47f5-9ebd-2bc8635bbce5.png#averageHue=%23faf9f8&clientId=u76eb8fc0-6be5-4&from=paste&height=673&id=u08f16258&originHeight=673&originWidth=1624&originalType=binary&ratio=1&rotation=0&showTitle=false&size=389688&status=done&style=none&taskId=uf1df6144-2a93-4a35-90b4-835c8782005&title=&width=1624)
# 十五、Mybatis注解式开发
![](https://cdn.nlark.com/yuque/0/2023/jpeg/32637015/1681217449018-8d6562c0-2059-4762-bdd9-34ad6bd16d9e.jpeg)
# 十六、Mybatis面试问题
Mybatis中的动态SQLMybatis中的动态SQL是指可以根据实际情况生成不同SQL语句的一种特殊语法。通常情况下，动态SQL是用来构建复杂的SQL语句的，例如根据不同条件拼接where语句、根据传入的参数构建不同的查询条件等。Mybatis中提供了一些内置的动态SQL语句，例如if、choose、when、otherwise等，可以根据需要自由组合使用，从而构建出灵活多变的SQL语句。同时，Mybatis也支持使用OGNL表达式来处理动态SQL，可以实现更加灵活的条件组合。掌握动态SQL的使用，可以帮助开发者更加方便地构建出灵活、高效的数据访问逻辑，提升应用的性能和扩展性。
Mybatis中的一对多映射在 Mybatis 中，一对多映射是指一个实体类中包含一个集合属性，该集合属性中包含多个与另一个实体类的对应关系，即一个实体类与另一个实体类是一对多的关系。例如，一个班级实体类包含多个学生实体类，那么班级实体类就是一的一方，学生实体类就是多的一方。
在 Mybatis 中实现一对多映射，需要使用 Mybatis 提供的 association 和 collection 标签。association 标签用于定义单个对象之间的关系，而 collection 标签则用于定义集合对象之间的关系。
具体来说，在映射文件中，需要先定义一的一方的查询语句，并使用 association 标签将多的一方的查询结果映射到一的一方中。然后，再定义多的一方的查询语句，并使用 collection 标签将多的一方的查询结果映射到一的一方的集合属性中。
Mybatis中#{}和${}的区别在Mybatis中，#{}和${}都是用来表示参数占位符的，但是它们的作用是不同的。
#{}用于表示一个占位符，Mybatis会将传入的参数自动进行类型转换，然后将转换后的值安全地插入到SQL语句中。这种方式可以有效地防止SQL注入的风险。
${}也用于表示一个占位符，但是它不会对传入的参数进行处理，直接将传入的字符串嵌入到SQL语句中。这种方式存在SQL注入的风险，应该尽量避免使用。
因此，建议在Mybatis中使用#{}作为参数占位符，以确保系统的安全性。
使用 #{} 时，Mybatis 会将 SQL 语句中的 #{} 替换成一个 ? 占位符，并使用 PreparedStatement 来执行 SQL 语句，这样就可以避免 SQL 注入等安全问题。同时，使用 #{} 还可以自动进行类型转换。
