#### 解释main方法的形式

```java
public static void main(String[] args){
    
}
```

main方法由虚拟机调用，因此其访问权限需要设置为public，而虚拟机在调用main方法时不需要创建对象，直接通过类名.方法名的形式调用，因此该方法为static

该方法接收String类型的数组参数，该数组中保存执行java命令时传递给所运行的类的参数

![image-20211210143207011](https://typora-xing.oss-cn-hangzhou.aliyuncs.com/img/image-20211210143207011.png)

在main方法中，可以直接调用main方法所在类的静态成员，但是不能直接访问该类的非静态成员，必须创建该类的一个实例对象，才能通过这个对象去访问类中的非静态成员

#### 在idea中给main方法传参数

![image-20211210144117281](https://typora-xing.oss-cn-hangzhou.aliyuncs.com/img/image-20211210144117281.png)

![image-20211210144149584](https://typora-xing.oss-cn-hangzhou.aliyuncs.com/img/image-20211210144149584.png)