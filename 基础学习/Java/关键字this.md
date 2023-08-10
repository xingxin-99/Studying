### this  

在还没有学习this关键字时，我们在类中定义方法时会去刻意回避参数名和属性名一致的情况，但一般参数的名字我们希望见名知其意，因此就借助this关键字来实现。

```java
// 刻意回避方法形参和属性名字相同，看到n和i并不能见名知意
public class student{
    String name;
    int ID;
    public void setName(String n){
        name = n;
    }
    public String getName(){
        return name;
    }
    public void setID(int i){
        ID = i;
    }
    public int getName(){
        return ID;
    }    
}
```

this关键字可以用来修饰类的属性、方法以及构造器

==this用来表示当前对象==

在类的方法中，可以使用“this.属性”或“this.方法”的方式来调用当前对象的属性或方法。但是通常情况下会选择省略this。只有当方法的形参和类的属性同名时就必须显示的使用“this.属性”的方式

**this修饰属性**

```java
// 使用this关键字来消除此种情况
//this修饰属性
public class student{
    String name;
    int ID;
    public void setName(String name){
        this.name = name;
    }
    public String getName(){
        return name;
    }
    public void setID(int ID){
        this.ID = ID;
    }
    public int getName(){
        return ID;
    }    
}
```

**this修饰构造器**

 在类的构造器中可以使用"this(形参列表)"的方式来调用本类中的其他构造器，如果多个构造器都需要执行相同的代码，那么通过这种方式可有效减少冗余代码

```java
//this修饰构造器
public class student{
    String name;
    int ID;
    public student(){
        System.out.println("+++");
    }
    public student(String name){
        this(); //调用无参构造器
        this.name = name;
    }
    public student(int ID){
        this();
        this.ID=ID;
    }
    public student(String name,int ID){
        this(name);//调用student(String name)构造器
        this.name = name;
        this.ID = ID;
    }
}
```

注意：

1. this(形参列表)只能声明在构造器的第一行，因此一个构造器最多只能声明一个“this(形参列表)”
2. 构造器不能使用“this(形参列表)”来调用自己

### package

- 使用package可以更好实现项目中类的管理


- 使用package声明类或接口所属的包，声明在源文件的首行


-  如果在包的命名中含有.，每.一次表示一层文件目录
- 包的命名要符合规范(xxxyyyzzz)，另外要见名知意

注意：同一个包下不能命名同名的接口和类，不同的包下可以命名同名的接口和类

![image-20211202170044345](%E5%85%B3%E9%94%AE%E5%AD%97this.assets/image-20211202170044345.png)

### import

在源文件中使用import结构导入指定包下的类、接口

声明位置：在包的声明和类的声明之间

使用xxx.*的方式导入xxx包下的所有结构

如果在源文件中使用了不同包下的同名类，那么至少有一个类需要以全类名的方式给出

如果使用类或接口是本包下定义的，则可以省略import结构

import static：导入指定类或接口中的静态结构（属性或方法）

