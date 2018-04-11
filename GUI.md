
#GUI
<table>
   <tr>
      <td>Component</td>
      <td>
         <table>
            <tr>
               <td>Container</td>
               <td><table>
                  <tr><td>Window</td>
                     <td><table>
                        <tr><td>Frame</td></tr>
                        <tr><td>Dialog</td></tr>
                        <table></td></tr>
                   <tr><td>Panel</td>
                      <td><table>
                         <tr><td>Applet</td></tr>
                       </table></td>
                   </tr>
               </table></td>
            </tr>
            <tr><td>Button,TextArea    ,Lable,List...</td></tr>
         </table>
      </td>    
    </tr>
 </table>


<b>AWT</b>
>AWT(Abstract Window Toolkit)包括了很多类和接口，用于Java Application的GUI（Graphics User Interface）编程    
>GUI的各种元素（窗口、按钮、文本框）由Java类来实现    
>Container和Component是AWT中的两个核心类

<b>Component & Container</b>

>Java的图形用户界面的最基本的组成部分是Component，Component类及其子类的对象用来描述以 
图形化的方式显示在屏幕上并能与用  户进行交互的GUI元素    
>Component对象不能独立地显示，必须用Container对象转载才可以显示    
>Container是Component子类
>Container对象使用add()添加Component对象      
>Container作为Component子类，也可以添加到其它Container对象中    
>常用Container：
>>Window：顶级窗口   
>>Panel：其对象可容纳其它Component对象，不能独立存在，必须被添加到其它Container中（window 或Applet）


<b>布局管理器</b>
> 管理Component在Container中的布局，不必直接设置Component位置和大小    
>每个Container 都有一个布局管理器对象，当容器需要对某个组件进行定位或判断其大时，就会调用其对应的布局管理器，调用Container的setLayout方法改变其布局管理器对象

AWT提供5种布局管理器类:    
<b>FlowLayout</b>
<ul>
   <li>Panel类的默认布局管理器，默认居中</li>
   <li>对组件逐行定位，从左到右</li>
   <li>不改变组件大小，按组件原有尺寸显示组件，可设置不同的组件间距、行距、对齐方式</li>
</ul> 
<b>BorderLayout</b>
<ul>
   <li>Frame类的默认布局管理器 <li>
   <li>BorderLayout将整个容器布局划分五个区域：AST、WEST、SOUTH、NORTH 、ENTER</li>
   <li>不指定组件加入部位，默认加入CENTER区</li>
   <li>每个区域只能加入一个组件，加入多个会覆盖之前加入的组件</li>
</ul>
<b>GridLayout</b> 
<ul><li>GridLayout型布局管理将空间划分为规则的矩形网格。从左到右、从上到下</li><li>GridLayout（3，4）；将内容分为3行4列</li></ul>
<b>CardLayout</b>    

<b>GridBagLayout</b>    


