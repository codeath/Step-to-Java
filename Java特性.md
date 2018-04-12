

#java基础（10）

1、Java特性：
>###继承：
>>使用extends 关键字实现类的继承；    
>>子类自动拥有了基类（superclass）的所有成员（成员变量和方法）；    
>>Java只支持单继承，不允许多继承（通过多个接口实现多继承？？？）
 <pre><code>
  class Father {
      private String name;
      Father(String name) {
          this.name = name;
      } 
      public void commonMethod() {
          System.out.println("Father's object and subclass's object implement.");
      }
  }
  
  class Son extends Father {
      private String feature;
      Son(String name, String feature) {
         super(name);
         this.feature = feature;
      }
     this.commonMethod();//直接继承自父类方法：Father's object and subclass's object implement.
  }
  </code></pre>
    
>###多态（动态绑定）：程序执行期间判断所引用的对象的实际类型，根据实际类型调用相应的方法。
>>多态的特征：    
>>>有继承关系；           
>>>需要重写；        
>>>父类的引用指向子类的对象。

  <pre><code>
  class Father {
      private String name;
      Father(String name) {
          this.name = name;
      } 
      public void commonMethod() {
          System.out.println("Father's object implement.");
      }
  }
  
  class Son extends Father {
      private String feature;
      Son(String name, String feature) {
         super(name);
         this.feature = feature;
      }
      public void commonMethod() {
          System.out.println("Son's object implement.");
      }
  }
  
  public class DynamicBinding {
      public static vodi main(String[] args) {
          Father f = new Son("son","strong");//System.out.print(f);-->Son@xxxxx;运行时判定为Son对象      
          f.commonMethod();//Son's object implement.
      }
  }
  </code></pre>
>###抽象：
>>用abstract关键字来修饰类时，这个类叫做抽象类；修饰方法时，该方法叫做抽象方法；    
>>含有抽象方法的类必须被声明为抽象类，该类被继承时，抽象方法必须被重写；    
>>抽象类不能被实例化；    
>>抽象方法只需声明，不需实现；    
   <pre><code>
   abstract class AbstractClass {
       private String ivar;
       public abstract void abstractMethod();
   }
   class TempClass extends AbstractClass {
       //AbstractClass a = new AbstractClass();//AbstractClass是抽象的，无法实例化
       public abstract void abstractMethod() {}
   }
   </code></pre>

2、权限修饰符
<table>
 <tr> 
   <td>private</td>     
   <td>类内部</td>
 </tr>
 <tr>
  <td>default</td>
  <td>类内部</td>
  <td>包内部</td>
 </tr>
 <tr>
  <td>protected</td>
  <td>类内部</td>
  <td>包内部</td>
  <td>子类</td>
 </tr>     
 <tr>
  <td>public</td>
  <td>类内部</td>
  <td>包内部</td>
  <td>子类</td>
  <td>任何地方</td>
 </tr>               
 </table>
 
>class 的权限修饰只可以用public 和 default
>>public类可以在任意地方被访问    
>>default类只可以在同一个包内部访问
>
>

<b>Java变量</b>  

Java局部变量
* 局部变量声明在方法、构造方法或者语句块中；
* 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
* 访问修饰符不能用于局部变量；
* 局部变量只在声明它的方法、构造方法或者语句块中可见；
* 局部变量是在栈上分配的。
* 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。

实例变量
* 实例变量声明在一个类中，但在方法、构造方法和语句块之外；
* 当一个对象被实例化之后，每个实例变量的值就跟着确定；
* 实例变量在对象创建的时候创建，在对象被销毁的时候销毁；
* 实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息；
* 实例变量可以声明在使用前或者使用后；
* 访问修饰符可以修饰实例变量；
* 实例变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见；
* 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定；
* 实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObejectReference.VariableName。

类变量（静态变量）
* 类变量也称为静态变量，在类中以static关键字声明，但必须在方法、构造方法和语句块之外。
* 无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。
* 静态变量除了被声明为常量外很少使用。常量是指声明为public/private，final和static类型的变量。常量初始化后不可改变。
* 静态变量储存在静态存储区。经常被声明为常量，很少单独使用static声明变量。
* 静态变量在程序开始时创建，在程序结束时销毁。
* 与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为public类型。
* 默认值和实例变量相似。数值型变量默认值是0，布尔型默认值是false，引用类型默认值是null。变量的值可以在声明的时候指定，也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。
* 静态变量可以通过：ClassName.VariableName的方式访问。
* 类变量被声明为public static final类型时，类变量名称必须使用大写字母。如果静态变量不是public和final类型，其命名方式与实例变量以及局部变量的命名方式一致。

