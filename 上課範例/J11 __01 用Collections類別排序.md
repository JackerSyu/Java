# J11__01 用Collections類別排序

## (1) Collections類別中有一個sort()靜態方法可以對List物件排序

```
Java專案
   |__ Main.java
```

### Main.java

```java
import java.util.Collections;
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        //----------------------------
        // 存放資料的List物件
        //----------------------------
        List<Integer> list = new ArrayList();

        //----------------------------
        // 將資料加入List物件,
        // int自動被包裝成Integer,
        // 稱為auto boxing.
        //----------------------------        
        list.add(75);
        list.add(87);
        list.add(65);
        list.add(92);
        list.add(97);
        list.add(55);
        list.add(70);
        list.add(76);
        list.add(86);
        list.add(68);

        //----------------------------
        // 用Collections的靜態方法
        // sort()排序.
        //----------------------------  
        Collections.sort(list);

        //----------------------------
        // 輸出list內容
        //----------------------------          
        list.forEach(d ->{
            System.out.println(d);
        });
        //----------------------------          
    }    
}
```

<br/>

## (2) 在sort()靜態方法中, 建立實作了Comparator介面的匿名物件.

```
Java專案
   |__ Main.java
```

### Main.java

```java
import java.util.Collections;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        //----------------------------
        // 存放資料的List物件
        //----------------------------
        List<Integer> list = new ArrayList();

        //----------------------------
        // 將資料加入List物件,
        // int自動被包裝成Integer,
        // 稱為auto boxing.
        //----------------------------        
        list.add(75);
        list.add(87);
        list.add(65);
        list.add(92);
        list.add(97);
        list.add(55);
        list.add(70);
        list.add(76);
        list.add(86);
        list.add(68);

        //============================
        // 用new建立Comparator
        // 匿名物件.
        //============================ 
        Collections.sort(list, new Comparator<Integer>(){
            @Override
            public int compare(Integer x, Integer y){
                return y - x;
            }    
        });

        //----------------------------
        // 輸出list內容
        //----------------------------          
        list.forEach(d ->{
            System.out.println(d);
        });
        //----------------------------          
    }    
}
```



<br/>

## (3) 在sort()靜態方法中, 用lambda建立實作了Comparator介面的物件.

```
Java專案
   |__ Main.java
```

### Main.java

```java
import java.util.Collections;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        //----------------------------
        // 存放資料的List物件
        //----------------------------
        List<Integer> list = new ArrayList();

        //----------------------------
        // 將資料加入List物件,
        // int自動被包裝成Integer,
        // 稱為auto boxing.
        //----------------------------        
        list.add(75);
        list.add(87);
        list.add(65);
        list.add(92);
        list.add(97);
        list.add(55);
        list.add(70);
        list.add(76);
        list.add(86);
        list.add(68);

        //============================
        // 用lambda表示式建立
        // Comparator物件.
        //============================
        Collections.sort(list, (x, y) -> {
            return y - x;
        });

        //----------------------------
        // 輸出list內容
        //----------------------------          
        list.forEach(d ->{
            System.out.println(d);
        });
        //----------------------------          
    }    
}
```
