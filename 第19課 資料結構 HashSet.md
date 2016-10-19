# 這個袋子中, 不會有兩個相同顏色的球


## 使用 HashSet
存在 java.util 套件中的 HashSet 類別物件可以存放多個資料, 每個資料也是一個物件. 
但相同內容的資料在 HashSet 中只會儲存一份. 
以下是一個使用 HashSet 的例子, 我們使用 add 方法加入兩個字串, 再利用 contains 方法是否某字串存在 HashSet 物件中. 


```javascript
import java.util.*;

class Main {
    public static void main(String[] args) {
        HashSet hs=new HashSet();		
        
        hs.add("Hello");
        hs.add("你好");

        //使用contains方法, 判斷一物件是否存在HashSet中		
        System.out.println(hs.contains("Hello"));
        System.out.println(hs.contains("早安"));
    }
}
```

## 使用迭代器
以下是另一個例子, 我們使用迭代器 Iterator 將 HashSet 中的資料逐一印出. 關於迭代器的使用, 將以另一講次說明. 

```javascript
import java.util.*;

class Main {
    public static void main(String[] args) {
        HashSet hs=new HashSet();		
        
        hs.add("Hello");
        hs.add("你好");
        printInfo(hs);
        
        hs.add("Hello");
        hs.add("早安");
        printInfo(hs);
    }
    
    private static void printInfo(HashSet hs){
        System.out.println("儲存資料共:" + hs.size() + "個");
        
        //使用迭代器將HashSet物件中的資料印出
        Iterator iterator = hs.iterator();       
        while (iterator.hasNext()){
            System.out.println(iterator.next());  
        }	
        
        System.out.println();
    }
}
```
 
## HashSet 在文章處理的應用
以下是一個用 HashSet 計算一篇文章中用了那些英文單子的例子, 
此類程式在文字探勘的應用中常用來作為原始資料的前置處理. 程式如下:  

```javascript
import java.util.*;

class Main {
    public static void main(String[] args) {
        //小s的內容是一篇文章
        String s= "From the red fox to the fennec fox, foxes look adorable. Because of this, people are sometimes tempted to keep them as pets. However, those who have tried have struggled. Unlike dogs and cats, the different species of fox have not been domesticated. Domestication only happens over a long period of time through selective breeding. Cats and dogs were domesticated by humans thousands of years ago to be pets and companions. Sheep, goats and other animals were domesticated for food. But there may be more to it than that. People who have tried to simply tame individual foxes often speak of a stubborn wildness that is impossible to get rid of. This suggests that foxes harder to tame than other animals. However, one extraordinary experiment has found a way to domesticate foxes. This one study could help us understand how our ancestors domesticated other animals, and indeed what domestication is.";

        System.out.println(s);	
        System.out.println();
		
        //將文章中的標點符號改成空白
        s=s.replaceAll("[.,;?!]", " ");
		
        //以空白切割文章的單字
        String k[]=s.split("\\s+");
		
        //將單字加入HashSet物件中, 重覆內容只存一份
        HashSet hs=new HashSet();		
        for(int i=0; i<k.length; i++){
            hs.add(k[i]);	
        }	
		
        //使用迭代器將HashSet物件中的資料一一取出
        Iterator iterator = hs.iterator();       
        while (iterator.hasNext()){
            System.out.println(iterator.next());  
        }
		
        //印出存在HashSet物件中的資料個數
		System.out.println();
		System.out.println("共有:" + hs.size() + "個不重覆單字");
    }
}
```

這個程式用了正規表示式 regular expression, 我們亦將以另一講次說明. 