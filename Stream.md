#Stream

#节点流类型
<table>
  <tr>
    <td>类型</td>
    <td>字符流</td>
    <td>字节流</td>
  </tr>
  <tr>
    <td>File</td>
    <td>
      <ul>
        <li>FileReader</li>
        <li>FileWirter</li>      </ul>
    </td>
    <td>
      <ul>
        <li>FileInputSteam</li>
        <li>FileOutputStream</li>
      </ul>
    </td>
  </tr>
   <tr>
    <td>Memory Array</td>
    <td>
      <ul>
        <li>CharArrayReader</li>
        <li>CharArrayWriter</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>ByteArrayInputStream</li>
        <li>ByteArrayOutputStream</li>
      </ul>
    </td>
  </tr>
   <tr>
    <td>Memory String</td>
    <td>
      <ul>
        <li>StringReader</li>
        <li>StringWriter</li>
      </ul>
    </td>
    <td></td>
  </tr>
   <tr>
    <td>Pipe</td>
    <td>
      <ul>
        <li>PipedReader</li>
        <li>PipedWriter</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>PipedInputStream</li>
        <li>PipedOutputStream</li>
      </ul>
    </td>
  </tr>
</table>

#处理流类型
<table>
  <tr>
    <td>处理类型</td>
    <td>字符流</td>
    <td>字节流</td>
  </tr>
  <tr>
    <td>Buffering</td>
    <td>
      <ul>
        <li>BufferedReader</li>
        <li>BufferedWriter</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>BufferedInputStream</li>
        <li>BufferedOutputStream</li>
      </ul>
    </td>
  </tr>
   <tr>
    <td>Filtering</td>
    <td>
      <ul>
        <li>FilterReader</li>
        <li>FilterWriter</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>FilterInputStream</li>
        <li>FilterOutputStream</li>
      </ul>
    </td>
  </tr>
   <tr>
    <td>Converting between bytes and character</td>
    <td>
      <ul>
        <li>InputStreamReader</li>
        <li>OutputStreamWriter</li>
      </ul>
    </td>
    <td></td>
  </tr>
   <tr>
    <td>Ojbect Serialization</td>

<td> </td>
    <td>
      <ul>
        <li>ObjectInputStream</li>
        <li>ObjectOutputStream</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Data conversion</td>
    <td> </td>
    <td>
      <ul>
        <li>DataInputStream</li>
        <li>DataOutputStream</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Counting</td>
    <td>LineNumberReader </td>
    <td>LineNumberInputStream</td>
</tr>
  <tr>
    <td>Peeking ahead</td>
    <td>PushbackReader </td>
    <td>PushbackInputStream</td>
  </tr>
  <tr>

<td>Printing</td>
    <td>PrintWriter </td>
    <td>PrintSteam</td>
  </tr>
</table>

#转换流
> InputStreamReader 和 OutputStreamWriter 用于字节数据到字符数据之间的转换    
> InputStreamReader 与 InputStream 套接
> OutputStreamWriter 与 OutputStream 套接    
> 转换流在构造时可以指定其编码集合 InputStream isr = new InputStreamReader(System.in, "ISO8859_1");

<pre><code>
import java.io.*;

public class TransformStream {
  public static void main(String[] args) {
    InputStreamReader isr = new InputStreamReader(System.in); //创建一个从标准输入设备输入的输入流对象
    BufferedReader br = new BufferedReader(isr);//isr引用的对象加一层buffer，缓冲流
    String s = null;
    try {
      s = br.readLine();
      while (s != null) {
        if (s.equalsIgnoreCase("exit") break;
        System.out.println(s.toUpperCase());
        s = br.readLine();
      }
      br.close();
    } catch (IOException e) {
      e.printStackTrace();
    }
  }
}
</code></pre>

#数据流    
>DataInputStream 和 DataOutputStream，提供可以存取与机器无关的Java原始类型数据的方法。    
>属于处理流，分别套接在InputStream 和 OutputStream类型的节点流上    

#Print流    
>PrintWriter 和PrintStream 输出流，分别针对字符与字节        
>PrintWriter 和PrintStream提供了重载的print    
>PrintWriter 和PrintStream 的输出操作不会抛出IOException    
>PrintWriter和PrintStream有自动flush功能     

#Ojbect流    
>直接将Object写入写出    
>transient关键字    
>>修饰的成员变量，不予序列化。 

>serializable接口：        
>>标记化接口，无重写方法；        
>>可序列化的。    

>externalizable接口            
>>readExternal(ObjectInput in);//           
>>writeExternal（ObjectOutput out);//按重写的方法序列化object  
