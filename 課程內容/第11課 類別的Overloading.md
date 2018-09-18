# 不管是計算 2 個數或是 3 個數總合, 計算的方法都稱為「相加」


## 類別方法的 Overloading
Overloading 的意義是: 相同目的的方法可以賦予相同名稱, 藉由傳入參數之不同而呼叫不同的方法.
比方說, 在 jdk 的 Math 類別中提供了 4 個回傳兩個參數中較大值的方法, 這 4 個方法的名稱都是 max, 由傳入參數決定那個方法被呼叫.
jdk 文件關於 Math 類別的 max 方法說明如下:
 
```
static double max(double a, double b)
              Returns the greater of two double values.
				
static float  max(float a, float b)
              Returns the greater of two float values.
				
static int    max(int a, int b)
              Returns the greater of two int values.
				
static long   max(long a, long b)
              Returns the greater of two long values.
```

以上方法當我們傳入 2 個 double 參數時, 第一個方法被呼叫; float參數呼叫第二個方法; int 及 long 則是三及四. 
這 4 個方法不必宣告成 4 個不同名稱, 對於使用者或設計者都可減輕名稱龐雜的負擔.<p>


以下是另一個 Overloading 的例子, 找出三個參數中的最大值, 當傳入不同參數時將呼叫不同方法.
```javascript
class MyMath{
	public static double max(double a, double b, double c){
		return Math.max(Math.max(a, b), c);
	}
	
	public static int max(int a, int b, int c){
		return Math.max(Math.max(a, b), c);
	}
}
```

呼叫不同的方法:
```javascript
System.out.println(MyMath.max(10, 3, 9));
System.out.println(MyMath.max(10.5, 20.4, 15.3));
```


## 不同參數個數的 Overloading
假設一個例子: 公司中有兩種計算薪水的方法分別適用於正職員工及兼職員工. 正職員工依其職等不同領不同的底薪, 另外可算加班費; 
兼職員工依每月工作時數領鐘點費. 如下:
 
```
class Employee{
	//正職員工的薪水計算
	public static int salary(char rank, int overHours){
		int baseSalary;
		
		if(rank=='A')
			baseSalary=30000;
		else
			baseSalary=25000;
			
		return baseSalary + 150*overHours;	//月薪=底薪+每小時150元加班費
	}
	
	//兼職員工的薪水計算
	public static int salary(int hours){
		return 125*hours;  //薪水每小時125元
	}
}
```

使用 Employee 的 salary 方法時, 如傳入 char及int 者, 即呼叫正職員工的薪水計算; 
如傳入 int 者, 即呼叫兼職員工的薪水計算.

```javascript
System.out.println(Employee.salary('A', 20));
System.out.println(Employee.salary(180));
```



## 建構元的 Overloading
建構元的寫法也可以用 Overloading. 假設立方體 Cube 物件生成時, 傳入不同的參數將以不同方式設定其長寬高, 以下是一個程式例子:

```javascript
class Cube{
	double length, width, height;
	
	//未傳入參數
	public Cube(){
		length=0;
		width=0;
		height=0;
	}
	
	//傳入1個double
	public Cube(double i){
		length=i;
		width=i;
		height=i;
	}
	
	//傳入3個double
	public Cube(double length, double width, double height){
		this.length=length;
		this.width=width;
		this.height=height;
	}
	
	public double volumn(){
		return length*width*height;
	}
}
```

使用範例如下:
```javascript
Cube a=new Cube();
Cube b=new Cube(10);
Cube c=new Cube(5, 6, 7);
		
System.out.println(a.volumn());
System.out.println(b.volumn());
System.out.println(c.volumn());
```