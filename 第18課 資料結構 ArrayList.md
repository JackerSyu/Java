# 就像火車車箱一樣, 資料一個跟著一個


## 使用 ArrayList
使用程式設計解決問題時, 難免會遇到需要特別的資料存取方法完成工作. 如果能在套件中找到適合的類別,
程式開發將會事半功倍. 舉例來說, 如果我們需要儲存不定個數的字串, 可以選用存在 java.util 套件中的 ArrayList 類別.
一個 ArrayList 物件可以存放多個資料, 每個資料也是一個物件. 存放在 ArrayList 物件中的資料可以
依序或是隨選的被取存, 也有現成的增加資料及刪除資料功能. 以下是一個增加資料的例子: 
 
 
```javascript
import java.util.*;

class Main {
    public static void main(String[] args) {
        //建立一個ArrayList物件
        ArrayList arrayList = new ArrayList();
        arrayList.add("Hello");
        arrayList.add("你好");
        
        for(int i=0; i<arrayList.size(); i++){
            System.out.println(arrayList.get(i));
        }
    }
}
```

## 泛型資料的特定化
在 JDK 文件中, 我們可以查到 ArrayList 新增及取出資料的方法, 包括 `boolean add(E e)` 及 `E get(int index)`.
在這兩個方法中出現的 E 表示其可以是任意型態的物件, 稱為泛型(Generic).

```
boolean add(E e)
        Appends the specified element to the end of this list.
```

```
E   get(int index)
    Returns the element at the specified position in this list.
```

由於 `E get(int index)` 方法的回傳型態可以是任何型態的物件, 因此如果取出後要進行物件方法的呼叫,
需要進行轉型, 轉代特定型態的物件, 稱為特定化(specialization). 範例如下:

```javascript
import java.util.*;

class Student{
    String stuNo;
    String stuName;
	
    public Student(String stuNo, String stuName){
        this.stuNo=stuNo;
        this.stuName=stuName;
    }
	
    public String info(){
        return "學號:" + stuNo + ", 姓名:" + stuName;
    }
}

class Main {
    public static void main(String[] args) {
        ArrayList arrayList = new ArrayList();
        
        //加入2個Student物件
        arrayList.add(new Student("1001", "王小明"));
        arrayList.add(new Student("1002", "陳小華"));
        
        for(int i=0; i<arrayList.size(); i++){
            //取出物件後, 特定化成Student物件
            Student s=(Student)arrayList.get(i);
            System.out.println(s.info());
        }
    }
}
```
在以上的例子中, 我們生成2個 Student 物件, 並且將生成的物件加入 arrayList 物件中. 當我們以迴圈逐一取出物件後, 
由於我們要呼叫物件的 info() 方法, 因此我們將它先轉型成原來的物件類別, 才有 info() 方法可以呼叫.



## ArrayList 可以放入不同類型的物件

在以下的範例中, 我們將 Student 及 Course 物件加入同一個 arrayList 中. 
為了可以在取出物件後以同一組程式輸出, 我們先製作一個 Printable 介面, 由兩種類別實作. 
因此, Student 物件除了是 Student 物件外, 也是一個 Printable 物件;
Course 物件除了是 Course 物件外, 也是一個 Printable 物件,
接著我們可以用 Printable 介面轉型此兩種物件, 不需寫兩組幾乎相同的程式.

```javascript
import java.util.*;

//一個介面
interface Printable{
    public String info();
}

//實作了 Printable 介面的 Student 類別
class Student implements Printable{
    String stuNo;
    String stuName;
	
    public Student(String stuNo, String stuName){
        this.stuNo=stuNo;
        this.stuName=stuName;
    }
	
    //實作介面的方法
    @Override
    public String info(){
        return "學號:" + stuNo + ", 姓名:" + stuName;
    }
}

//實作了 Printable 介面的 Course 類別
class Course implements Printable{
    String course;
    int credit;
	
    public Course(String course, int credit){
        this.course=course;
        this.credit=credit;
    }
	
    //實作介面的方法
    @Override
    public String info(){
        return "課程:" + course + ", 學分數:" + credit;
    }
}

class Main {
    public static void main(String[] args) {
        ArrayList arrayList = new ArrayList();
        
        //加入2個Student物件
        arrayList.add(new Student("1001", "王小明"));
        arrayList.add(new Student("1002", "陳小華"));
        
        //再加入2個Course物件
        arrayList.add(new Course("國文", 3));
        arrayList.add(new Course("英文", 2));
        
        for(int i=0; i<arrayList.size(); i++){
            //取出物件後, 轉型實作了 Printable 的物件
            Printable s=(Printable)arrayList.get(i);
            System.out.println(s.info());
        }
    }
}
```

在以上的例子中, 我們將 Student 及 Course 兩種不同類型的物件加入 arrayList 中.
取出物件後, 我們先將它轉成兩者共同的 Printable 介面物件, 再以介面的 info() 方法印出資料. 