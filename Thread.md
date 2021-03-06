#Thread

#线程
>线程是一个程序内部的顺序控制流    
>线程和进程    
>>每个进程都有独立的代码和数据空间，进程间的切换有较大的开销        
>>同一类线程共享代码和数据空间，每个线程有独立的运行栈和程序计数器        
>>多进程：在操作系统中能同时运行多个任务     
>>多线程：同一应用程序中有多个顺序流同时执行    
>
>VM 启动时会有一由主方法（public static void main（）{}）所定义的线程

#线程的创建和启动
>implements:    
>>定义线程类并实现Runnable接口     
>>Thread t = new Thread（tar）；//tar为Runnable接口类型     
>>Runnable接口只有一个 “public void run();" 方法，用以定义线程运行体；    
>>使用Runnable接口可以为多个线程提供共享的数据；    
>>在实现Runnable接口的类的run（）；方法体中"public static Thread currentThread();"可以获取当前executing线程的引用；    
>
>extends：    
>>定义Thread子类 class MyThread extends Thread{public void run(){}};
>>生成子类对象生成线程

<pre><code>
public class ThreadTest {
	public static void main(String[] args) {
		//interface implements
		InterfaceThread it = new InterfaceThread();
		Thread t = new Thread(it);
		t.start();
	
		//extends Thread
		ExtendsThread et = new ExtendsThread();
		et.start();

		for (int i=0; i<100; i++) {
			System.out.println("DefaultThread: " + i);
		}
	}
 }

class InterfaceThread implements Runnable {
	public void run() {
		for (int i=0; i<100; i++) {
			System.out.println("InterfaceThread: " + i);
		}
	}
}

class ExtendsThread extends Thread {
	public void run() {
		for (int i=0; i<100; i++) {
			System.out.println("ExtendsThread: " + i);
		}
	}
}
</code></pre>

#线程控制基本方法
<table>
<tr>
<td>方法</td>
<td>功能</td>
</tr>
<tr>
<td>isAlive()</td>
<td>判断线程是否未终止</td>
</tr>
<tr>
<td>getPriority()/setPriority()</td>
<td>获取/设置优先级</td>
</tr>
<tr>
<td>Thread.sleep()</td>
<td>将当前线程睡眠指定毫秒数/throws InterruptedException</td>
</tr>
<tr>
<td>join()</td>
<td>将当前线程与该线程“合并”，等待该线程结束，再恢复当前线程</td>
</tr>
<tr>
<td>yield()</td>
<td>让出cpu，当前线程进入就绪队列等待调度</td>
</tr>
<tr>
<td>wait()</td>
<td>当前线程进入对象的waitpool</td>
</tr>
<tr>
<td>notify()/notifyAll()</td>
<td>唤醒对象的waitpool中的一个/所有等待线程</td>
</tr>
</table>

#sleep()、currentThread()
<pre><code>
import java.util.Date;

public class ThreadSleep {
	public static void main(String[] args) {
		InterfaceThread it = new InterfaceThread();
		Thread t = new Thread(it);
		t.start();
		System.out.println(Thread.currentThread());//main
		try {
			Thread.sleep(10000);
		} catch (InterruptedException e) {

		}
		t.interrupt();
	}
}

class InterfaceThread implements Runnable {
	public void run() {
		System.out.println(Thread.currentThread());//Thread-		boolean frg = true;
		while(frg) {
			System.out.println(new Date());
			try {
				Thread.currentThread().sleep(1000);
			} catch (InterruptedException e) {
				frg = false;
				System.out.println(Thread.currentThread() + "has been interrupted");
			}
		}
	}
}
</code></pre>

#线程同步（synchronized）
<ul>
	<li>修饰实例方法，作用于当前实例加锁，进入同步代码前要获得当前实例的锁</li>
	<li>修饰静态方法，作用于当前类对象加锁，进入同步代码前要获得当前类对象的锁</li>
	<li>修饰代码块，指定加锁对象，对给定对象加锁，进入同步代码库前要获得给定对象的锁</li>
</ul>
<b>synchronized作用于实例方法</b>
***
>实例对象锁就是用synchronzied修饰实例对象中的实例方法，实例方法不包括静态方法    
<pre><code>
public class AccountingSync implements Runnable {
	public static int i = 0;

	public synchronized void increase() {
		i ++;
	}

	@Override
	public void run() {
		for (int j = 0; j<1000000; j++) {
			increase();
		}
	}

	public static void main(String[] args){
		AccountingSync instance = new AccountingSync();
		Thread t1 = new Thread(instance);
		Thread t2 = new Thread(instance);
		t1.start();
		t2.start();
		System.out.println(i);//200,0000
	}
}
</code></pre>
  开启两个线程操作同一资源，对实例方法increase()使用synchronized修饰，当前线程的锁便是实例对象instance.    
当线程t1获取该对象的锁之后，t2无法获取该对象的锁，也就无法访问该对象的synchronized实例方法。

<pre><code>
	public static void main(String[] args) {
		Thread t1 = new Thread(new AccountingSync());
		Thread t2 = new Thread(new AccountingSync());
		
		t1.start();
		t2.start();
		System.out.println(i);
	}
</code></pre>
  创建两个实例对象，并开启两个线程对共享变量进行操作，得到结果不是期望结果200,0000. 虽然使用了synchronized修饰了increase（）方法，    
  但是new了两个不同的实例对象，也就是存在两个不同的锁，当线程启动时无法保证对共享变量的依次访问，也就是线程安全无法保证。   
  
<b>synchronized作用于静态方法</b>
***
>当synchornized作于静态方法是，锁的就是当前类的class对象。静态成员是类成员不属于任何一个实例对象，因此通过class对象锁可以控制静态    
成员的并非操作。   
  将increase()改为静态方法，synchronized作用的就是当前类对象，只有一个，这样保证锁只有一个。
  <pre><code>public static synchronzied void increase(){ i++; } </code></pre>


<b>synchronized作用于代码块</b>
***
>方法体比较大，同时存在比较耗时的操作，而需要同步的资源只在一小块代码中，此时就可以使用同步代码块的方式对需要同步的代码进行包裹。
<pre><code>
	public void run() {
		synchronized (this) {
			for (int j = 0; j<1000000;j++){
				i++;
			}
		}
	}
</code></pre>
上述代码将synchronized 作用于一个当前实例对象，每次当线程进入synchronized包裹的代码块时，就会要求当前线程持有this对象锁，如果当前有    
其它线程正持有该对象锁，那新到的线程就必须等待。
