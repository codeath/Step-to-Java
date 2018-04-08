
<div>
#NumberFormat:
>String format(double number);//根据对象模式将number转化为字符串，并返回改字符串对象</p>
>static NumberFormat getCurrencyInstance();//货币格式格式化；
>static NumberFormat getPercentInstance();//百分比格式化；

#DecimalFormat：
>DecimalFormat(String pattern);// 创建一个具有指定模式的对象
>void applyPattern();//为DecimalFormat对象指定新的格式模式；
>String format(double number);// 与NumberFormat一致；
<pre><code>
import java.util.Scanner;
import java.text.NumberFormat;
import java.text.DecimalFormat;

public class Purchase {
	public static void main(String[] args) {
		NumberFormat currency = NumberFormat.getCurrencyInstance();
		NumberFormat percent = NumberFormat.getPercentInstance();

		System.out.println(currency.format(0.06));//￥0.06
		System.out.println( percent.format(0.06));//6%

		Scanner sc = new Scanner(System.in);
		System.out.print("Please enter number: ");
		int i = sc.nextInt();//2
		System.out.println(currency.format(i));//￥2.00
		System.out.println(percent.format(i));//200%

		DecimalFormat dc = new DecimalFormat();
		System.out.print("Please enter number: ");
		i = sc.nextInt();//2
		System.out.println(dc.format(i * 0.2));//0.4；
		dc.applyPattern("00.####");//
		System.out.println(dc.format(100.5));//100.5

	}
}
</code><pre>

</div>
