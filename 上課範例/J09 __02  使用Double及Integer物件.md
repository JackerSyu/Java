# J09__02  使用Double及Integer物件


## (1) Double物件不同於double: 前者是一個物件, 後者是一個原生資料型態.
```
Java專案
   |__ Main.java   
```


### (1) Main.java
```java
import java.util.List;
import java.util.ArrayList;

public class Main {

    public static void main(String[] args) {
        //-----------------------------------
        // 生成一個List物件, 
        // 其中放置的均為Double型態的物件.
        //-----------------------------------        
        List<Double> list = new ArrayList();

        //-----------------------------------
        // 將double資料存入Double物件內, 
        // 稱為boxing.
        //-----------------------------------         
        list.add(33.5);
        list.add(28.3);
        list.add(32.3);
        list.add(40.1);
        list.add(30.8);
        
        //-----------------------------------
        // 用lambda表示式生成一個函式, 
        // 處理list中的每個元素.
        //-----------------------------------
        list.forEach(d -> {
            System.out.println(d);
        });
        //-----------------------------------        
    }    
}
```

