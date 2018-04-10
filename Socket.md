#<b>Socket</b>
* 两个Java应用程序可通过一个双向的网络通信链接实现数据交换，这个双向链路的一端称为Socket
* Socket通常用来实现client-server连接
* java.net包中定义的两个类Socket 和 ServerSocket， 分别用来实现双向链接的client 和server端
* 建立链接时所需的寻址信息为远程计算机的IP地址和端口号（Port number）

<b>TCP</b>
<pre><code>
/**
 * server
 */

import java.net.*;
import java.io.*;

public class TalkServer {
	public static void main(String[] args) throws IOException{

		ServerSocket ss = new ServerSocket(8888);
		Socket socket = ss.accept(); //阻塞式一直等待client，直到有一个client连上该port

		DataInputStream dish = new DataInputStream(socket.getInputStream());
		DataOutputStream dos = new DataOutputStream(socket.getOutputStream());
		DataInputStream dis = new DataInputStream(System.in);

		String message = " ";
		do {
			System.out.print("I: " );
			message = dis.readLine();
			dos.writeUTF(message);						
			System.out.println("Client: " + dish.readUTF());
			if (message.equals("exit")) {
				dos.flush();
				dish.close();
				dis.close();
				dos.close();
				socket.close();
				break;
			}
		} while (true);

	}
}

/**
 * client
 */

import java.net.*;
import java.io.*;

public class TalkClient {
	public static void main(String[] args) {
		try {
import java.net.*;
import java.io.*;
public class UDPClient {
	public static void main(String[] args) throws Exception {

		long n = 1000l;
		ByteArrayOutputStream baos = new ByteArrayOutputStream();
		DataOutputStream dos = new DataOutputStream(baos);
		dos.writeLong(n);
		byte[] buf = baos.toByteArray();

		// byte buf[] = new byte[1024];
		// buf = (new String("123455454535")).getBytes();
		DatagramPacket dp = new DatagramPacket(buf, buf.length,
									 new InetSocketAddress("127.0.0.1", 5678));
		DatagramSocket ds = new DatagramSocket(9999);
		ds.send(dp);
		ds.close();

	}
}			Socket socket = new Socket("127.0.0.1",8888);//连接上指定port的server端

			DataInputStream dish = new DataInputStream(socket.getInputStream());//从socket输入流创建输入流，
			DataInputStream dis = new DataInputStream(System.in);//从标准输入创建输入流
			DataOutputStream dos = new DataOutputStream(socket.getOutputStream());
			String message = null;
			do{
				System.out.println("Server: " + dish.readUTF());//从输入流读取服务端传输的信息、打印
				System.out.print("I: ");
				message = dis.readLine();
				dos.writeUTF(message);//从标准输入流的信息通过输出流向server端传输
				if (message.equals("exit")) {
					dis.close();
					dish.close();
					dos.flush();
					socket.close();	
					break;		
				}
			}while(true);
		} catch (UnknownHostException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}	
	}
}
</code></pre>

<b>UDP</b>
* 不可靠传输
* 效率高
* 数据报/非连接
<pre><code>
import java.net.*;
import java.io.*;

public class UDPServer {
	public static void main(String[] args) throws Exception{
		byte buf[] = new byte[1024];
		DatagramPacket dp = new DatagramPacket(buf, buf.length);
		DatagramSocket ds = new DatagramSocket(5678);

		while(true) {
			ds.receive(dp);
			ByteArrayInputStream bais = new ByteArrayInputStream(buf);
			DataInputStream dis = new DataInputStream(bais);
			System.out.println(dis.readLong());

		}
	}
}
import java.net.*;
import java.io.*;
public class UDPClient {
	public static void main(String[] args) throws Exception {

		long n = 1000l;
		ByteArrayOutputStream baos = new ByteArrayOutputStream();
		DataOutputStream dos = new DataOutputStream(baos);
		dos.writeLong(n);
		byte[] buf = baos.toByteArray();

		// byte buf[] = new byte[1024];
		// buf = (new String("123455454535")).getBytes();
		DatagramPacket dp = new DatagramPacket(buf, buf.length,
									 new InetSocketAddress("127.0.0.1", 5678));
		DatagramSocket ds = new DatagramSocket(9999);
		ds.send(dp);
		ds.close();

	}
}
</code></pre>
