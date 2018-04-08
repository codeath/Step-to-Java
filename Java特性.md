

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
          Father f = new Son("son","strong");//System.out.print(f);-->Son@xxxxx;运行时判定为Son对象          f.commonMethod();//Son's object implement.
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
