## J08-1-1 使用List存放多個物件


```java
//----------------
// 匯入必要套件
//----------------
import java.util.List;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        //---------------------------------    
        // 宣告一個存放String的list,
        // 這個list的實際結構是ArrayList
        //---------------------------------        
        List<String> list = new ArrayList();
        
        //--------------------------------- 
        // 將String物件加入list中
        //---------------------------------       
        list.add("A12001");
        list.add("A12002");
        
        //---------------------------------     
        // 依序取出list中的字串
        //---------------------------------       
        for(String s : list){
            System.out.println(s);
        }
    }    
}
```
