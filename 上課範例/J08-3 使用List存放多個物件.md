# J08-3  使用List存放多個物件


## (1) 用ArrayList實作

```java
//----------------
// 匯入必要套件
//----------------
import java.util.List;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        //----------------------------------------------    
        // 宣告一個存放String的list,
        // 這個list的實際結構是ArrayList
        //
        // 若將ArrayList和LinkedList比較,          
        // ArrayList的查詢速度較快, 新增/刪除的速度較慢    
        //----------------------------------------------        
        List<String> list = new ArrayList();
        
        //----------------------------------------------  
        // 將String物件加入list中
        //----------------------------------------------      
        list.add("資料1");
        list.add("資料2");
        list.add("資料3");
        list.add("資料4");
        list.add("資料5");

        //----------------------------------------------      
        // 依序取出list的元素個數
        //---------------------------------------------- 
        System.out.println("list長度:" + list.size());
        
        //----------------------------------------------      
        // 依序取出list中的字串
        //----------------------------------------------         
        for(String s : list){
            System.out.println(s);
        }
        //----------------------------------------------   
    }    
}
```


<br/>

## (2) 用LinkedList實作

```java
//----------------
// 匯入必要套件
//----------------
import java.util.List;
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        //----------------------------------------------    
        // 宣告一個存放String的list,
        // 這個list的實際結構是ArrayList
        //
        // 若將ArrayList和LinkedList比較,          
        // LinkedList的查詢速度較慢, 新增/刪除的速度較快    
        //----------------------------------------------        
        List<String> list = new LinkedList();
        
        //----------------------------------------------  
        // 將String物件加入list中
        //----------------------------------------------      
        list.add("資料1");
        list.add("資料2");
        list.add("資料3");
        list.add("資料4");
        list.add("資料5");
        
        //----------------------------------------------      
        // 依序取出list的元素個數
        //---------------------------------------------- 
        System.out.println("list長度:" + list.size());        
        
        //----------------------------------------------      
        // 依序取出list中的字串
        //----------------------------------------------              
        for(String s : list){
            System.out.println(s);
        }
        //---------------------------------------------- 
    }    
}
```
