---

---

```
 https://www.bilibili.com/video/BV1P7411V7nQ?p=226
```

### jvm

#### 内存图首入

![](\png\image001.png)

#### 递归内存图

![](D:\java\typora\png\image002.png)

#### 对象内存图

![](D:\java\typora\png\image003.png)

![](D:\java\typora\png\image004.png)

#### 对象作为实例变量的内存图

![](D:\java\typora\png\image007.png)

**执行javac Test.java生成Test.class，User.class和Address.class，在运行 java Test的时候jvm就有如下内存图**   

![](D:\java\typora\png\image008.png)

#### 值拷贝

**Java中都是值拷贝，不是引用，基本类型是把保存在内存中的值拷贝，引用类型也是把保存在内存中的地址值拷贝**

![](D:\java\typora\png\image009.png)

#### 253静态变量jvm

![1592705572304](png\静态变量.png)

#### 254 空指针异常

```
p1 = null;
重点 空指针异常只有在 空引用访问实例相关
p1.country 访问静态变量也行，其实将p1变成Person.country进行访问了，所以可以空指针访问
```

#### 262 this 内存结构

![1592705656548](png\this内存.png)

#### 311 super内存结构

```java
Public Class SuperTest{
    public static void mian(String[] args){
        CreditAccount ca1 = new CreditAccount();
        CreditAccount ca2 = new CreditAccount("11111", 10000, 0.999);
    }
} 

class Account extends Object{
    private String actno;
    private double balance;
    public Account(){}
    public Account(String actno, double balance){
        this.actno = actno;
        this.balance = balance;
    }
}
class CreditAccount extends Account{
    private double credit;
    public CreditAccount(){}
    public CreditAccount(String actno, double balance, double credit){
        super(actno, balance);
        this.credit = credit;     
    }
}

```

![1592739069864](png\super作用.png)

![1592738917325](png\super内存图.png)

####  super&this调用实例变量

![](png/super理解.png)

![1592740644363](png/super内存图2.png)

#### super. 什么时候不能省略

* 子父类都有重名变量，子类想访问 父类的特征，super.不能省略

 ![1592741163952](png/super子父类变量重名代码.png)

![1592741086618](png/super字父类变量重名.png)



### 类

#### 方法覆盖

##### 方法覆盖条件

![1592705926534](png\方法覆盖.png)

##### 静态方法不存在方法覆盖

```
下图的a.doSome() 还是输出的Animal的doSome()；当然Animal.doSome输出Animal的，Cat的doSome输出Cat的
```

![](/静态方法不存在覆盖.png)

##### 覆盖的返回值类型可不同？

* 如果是基本数据类型返回值，返回值类型必须相同。引用类型，子类的返回值可以变小，但不能变大。实际开发中，返回值类型都写一样的，变小没意义

![1592732429455](/方法覆盖返回值类型.png)

#### 多态

##### 多态运行机制

```
cat,bird extends animal, dog not extends animal
```



![](png\多态运行机制0.png)

![](png\多态运行机制.png)

##### 向下转型风险

![1592727471242](png/向下转型风险.png)

##### 封装，继承，多态关系

* 有了封装这种整体概念之后，对象雨对象才生继承，有了继承之后，才有了方法覆盖，继而有多态。方法覆盖要和多态在一起才有意义。

#### super

##### super和this对比

![1592733346628](png\super&this对比.png)

##### super不是引用

![1592742198836](/png/super不是引用.png)

#### final

1、final 修饰的类无法被继承

2、final 修饰的方法无法被覆盖

3、final修饰的局部变量只能赋一次值

4、final修饰的引用只能指向一个对象，该对象无法被垃圾回收器回收，直到当前方法结束，才会释放空间。但是该对象的内部数据可以修改

```
public static void main(String[] args){
    final int m;
    m = 20;  // right
    m = 30; // error
    
    final Person p = new Person();
    p = new Person() ; // error p = null 也是错的
}
```
5、final 修饰的实例变量必须手动赋值，不能使用使用默认值

* 因为new 对象的时候，构造器会默认初始化实例变量(如this.name = null)，但是因为final修饰的变量只能赋值一次，那这样以后name就无法被赋值了，但是可以写成如下，只要是构造器就显示指定this.name = value;

  ```
  class Person{
      final String name;
      public Person(){
          this.name = "ccc";
      }
      public Person(String name){
          this.name = name;
      }
  }
  ```


6、final修饰的实例变量一般和static联合使用，成为常量，用大写  public static final double PI = 3.14

#### 抽象类

##### 图示抽象类的由来

![1592834992051](png/抽象类.png)

##### 抽象类的性质

1、[修饰符列表] abstract class 类名{ 类体; }

2、抽象类是无法实例化，无法创建对象，所以抽象类是被子类继承的

3、final和abstract不能联合使用，因为final修饰的类无法被继承，而abstract修饰的类需要被继承(当然你写一个抽象类可以不去继承他，写了不继承就可不用写了)

4、抽象类的子类可以是抽象类，也可以是非抽象类

5、**抽象类虽然无法实例化，但是抽象类有构造方法，这个构造方法是供子类使用的**

6、抽象类中可以有抽象方法（没有方法体，以封号结尾）public abstract void doSome();

7、抽象类中不一定有抽象方法，但抽象方法必须出现在抽象类中

8、一个非抽象的类继承抽象类，必须将抽象类中的方法重写

#### 接口



