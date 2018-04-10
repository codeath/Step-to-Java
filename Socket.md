#<b>Socket</b>
* 两个Java应用程序可通过一个双向的网络通信链接实现数据交换，这个双向链路的一端称为Socket
* Socket通常用来实现client-server连接
* java.net包中定义的两个类Socket 和 ServerSocket， 分别用来实现双向链接的client 和server端
* 建立链接时所需的寻址信息为远程计算机的IP地址和端口号（Port number）

<pre><code>
/**
 * server
 */

import java.net.*;
import java.io.*;

public class TCPClient {
	public static void main(String[] args) throws Exception {
		Socket s = new Socket("127.0.0.1", 6666);//UnknownedHostException

		OutputStream os = s.getOutputStream();
		DataOutputStream dos = new DataOutputStream(os);
		dos.writeUTF("hello server!");
		dos.flush();
		dos.close();
		s.close();

	}
}

/**
 * client
 */

import java.net.*;
import java.io.*;

public class TCPClient {
	public static void main(String[] args) throws Exception {
		Socket s = new Socket("127.0.0.1", 6666);//UnknownedHostException

		OutputStream os = s.getOutputStream();
		DataOutputStream dos = new DataOutputStream(os);
		dos.writeUTF("hello server!");
		dos.flush();
		dos.close();
		s.close();

	}
}
</code></pre>
