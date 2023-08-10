[TOC]

## object类

#### equals方法

##### equals与==对比

**==：**一个比较运算符，即可以判断基本数据类型也可以判断引用数据类型，判断基本数据类型时判断的是其值是否相等，判断引用数据类型时判断的是其地址值是否相等即其是否指向同一个对象

**equals：** Object类中定义的一个方法，只可以判断引用数据类型

##### 重写equals方法

> Object类中的equals方法用于判断两个对象是否相同

```java
//Object类中声明的equals方法
public boolean equals(Object obj) {
        return (this == obj);
    }
```

由于Object为超类，我们所声明的任意一个类都为Object的子类，因此可以在我们声明的类中重写equals方法

> String类中重写了equals方法，用于判断两个字符串是否相等

```java
//String类中重写的equals方法
public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
```

> 定义一个person类，重写equal方法，用于判断声明的两个person对象内容是否相等

```java
public class Test {
    public static void main(String[] args){
        Person p1 = new Person("Jim",18,'0');
        Person p2 = new Person("Marry",22,'1');
        Person p3 = new Person("Marry",22,'1');
        System.out.println(p1.equals(p2));		//返回false
        System.out.println(p3.equals(p2));		//返回true
    }
}
public class Person {
    private String name;
    private int age;
    private char gender;
    public Person(String name,int age,char gender){
        this.age=age;
        this.gender=gender;
        this.name=name;
    }
    @Override
    //重写Object类的equals方法
    public boolean equals(Object obj) {

        if(this==obj){          //this指当前对象
            return false;
        }
        //判断obj的运行类型是否为Person类，如果不为，则直接返回false，如果为，则继续向下判断其内容是否相等
        if(obj instanceof Person){
            Person p =(Person) obj;
            if(this.name.equals(p.name)&& this.age==p.age && this.gender==p.gender){
                return true;
            }
        }
        return false;
    }
```

> 练习题

![image-20211209104005976](https://typora-xing.oss-cn-hangzhou.aliyuncs.com/img/image-20211209104005976.png)



#### hashCode 方法

![image-20211209105308892](https://typora-xing.oss-cn-hangzhou.aliyuncs.com/img/image-20211209105308892.png)

**总结**

1. 该方法可以提高具有哈希结构容器的效率
2. 如果两个引用指向同一个对象，那么哈希值肯定是一样的；如果两个引用指向不同的对象，则哈希值是不一样的（但也有可能一样）
3. 哈希值是通过地址值计算得来，但是不能将哈希值等价于地址

#### toString方法

```java
//Object类中的toString源码
public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }
```

**返回值：**全类名（包名+类名）+@+哈希值的十六进制

子类中一般会对toString方法进行重写，用于返回对象的属性信息

```java
//Person类中重写toString方法，返回类的属性信息（使用快捷键alt+insert选择toString就会默认生成下列语句）
@Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", gender=" + gender +
                '}';
    }
```

当将对象作为输出语句直接输出时，会默认调用"对象.toString()"方法

```java
System.out.println(p1) //默认调用p1.toString()方法
```

<img src="https://typora-xing.oss-cn-hangzhou.aliyuncs.com/img/image-20211209112300726.png" alt="image-20211209112300726" style="zoom:67%;" />

如果在子类中重写了toString()方法，那么将会调用子类重写的方法

![image-20211209112513394](https://typora-xing.oss-cn-hangzhou.aliyuncs.com/img/image-20211209112513394.png)

#### finalize方法

当垃圾回收器确定不存在对象的引用时，由对象的垃圾回收器调用此方法

当对象被回收时，系统自动调用该对象的finalize方法，子类可以重写该方法，做一些释放资源的操作

什么时候被回收：当某个对象没有任何引用时，则jvm就认为这个对象是一个垃圾对象，就会使用垃圾回收机制来销毁对象，在销毁前会调用finalize方法

垃圾回收机制的调用是由系统来决定的，也可以通过System.gc()主动触发垃圾回收机制
