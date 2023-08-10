**super关键字的使用**

1. super可以理解为：父类的

2. super可以用来调用：属性、方法、构造器

   **super调用属性/方法**

   在子类的方法或构造器中，通过使用super.属性或super.方法来调用父类中的属性或方法，但是通常情况下会省略super。但是当子类和父类中定义了同名的属性或方法时，如果想在子类中调用同名的父类的方法或者属性，就需要显示的使用“super.属性/方法”的方式。

   **super调用构造器**

   1.  可以在子类的构造器中显示的使用“super(形参列表)”的方式来调用父类中指定的构造器

      ```java
      public class person{
          private int ID;
          private String name;
          public person(){
              
          }
          public person(int ID){
              this.ID=ID;
          }
      }
      public class children extends person{
          int sex;
          public children(){
              
          }
          public children(int ID,int sex){
              super.ID=ID;		//由于ID为private类型，因此不能通过this.ID调用
              this.sex=sex;
          }
      }
      ```

   2. “super(形参列表)”只能声明在构造器的首行，因此一个构造器内部只能在首行使用一次“super(形参列表)”或“this(形参列表)”

   3. 如果在构造器的首行没有显示的声明“super(形参列表)”或“this(形参列表)”，那么在首行将会默认调用“super()”

      ```java
      public class person{
          private int ID;
          private String name;
          public person(){
              System.out.println("空参构造器！");
          }
      }
      public class children extends person{
          int sex;
          public children(){
              
          }
      }
      public class KidsTest {
          public static void main(String[] arr){
             Student stu = new Student();		//		打印空参构造器！
          }
      }
      ```

      

   4. 在类的多个构造器中，至少有一个类的构造器中使用了“super(形参列表)”，调用父类的构造器

      

   ![image-20211207135019810](https://typora-xing.oss-cn-hangzhou.aliyuncs.com/img/image-20211207135019810.png)

