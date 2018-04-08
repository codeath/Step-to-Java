
#Map:

>实现Map接口的类用来存储键-值对    
>Map接口的实现类有HashMap和TreeMap等    <url>https://www.cnblogs.com/skywang12345/p/3310835.html</url>
>Map类中存储的键值对通过键标识，所以键不能重复


#Auto-boxing/unboxing
>自动将<b>基本类型</b>转换为对象    
>自动将对象转换为基本类型    
>只能在基本类型与包装类之间进行

<pre><code>
import java.util.*;

public class MapClass {
	public static void main(String[] args) {
		Map m1 = new HashMap();
		Map m2 = new TreeMap();

		m1.put("one", new Integer(1));
    //m2.put("one",1);//auto-boxing
		// String temp = new String();
		// temp = 2;  //complier: 不兼容的类型
		m1.put("two", new Integer(2));

		m2.put("A", new Integer(65));
		m2.put("B", new Integer (200));
		m2.put("C", new Integer(67));

		System.out.println(m1.size());
		System.out.println(m1.containsKey("one"));
		System.out.println(m2.size());
		System.out.println(m2.containsValue(new Integer(200)));

		if (m1.containsKey("two")) {
			int i = ((Integer)m1.get("two")).intValue();
			System.out.println(i);
		}

		Map m3 = new HashMap(m1);
		m3.putAll(m2);
		System.out.println(m3);
                                                                   
	}
}
</pre></code>

#泛型Generic
<pre><code>
Map<String, String> m = new HashMap<String, String>();
m.put("key","value");
String s = new String();
s = m.get("key"); //s = (String)m.get("key");
</code></pre>


