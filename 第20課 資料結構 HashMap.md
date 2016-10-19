# 這個袋子中, 所有的球都是兩個兩個梆在一起


## 使用 HashMap
存在 java.util 套件中的 HashMap 類別物件可以存放多組成對的資料, 每組資料包括 key(鍵) 及 value(值). 
以下以一個英文/中文對應的資料存在 HashMap 中. 由於我們不能在 HashMap 中存放兩筆具有相同 key 值的資料,
因此如果同一個英文有多個中文意義, 儲存中文的資料型態就要改用類以陣列的結構.
以下的例子簡化了一些問題, 當作一個特例看待即可, 如下: 


```javascript
import java.util.*;

class Main {
    public static void main(String[] args) {
        HashMap hm=new HashMap();		
        
        hm.put("school", "學校");
        hm.put("student", "學生");

        //使用containsKey方法, 判斷一物件是否存在HashMap中		
        System.out.println(hm.containsKey("school"));
        System.out.println(hm.containsKey("teacher"));
        
        String s=(String)hm.get("school");
        System.out.println(s);
        
        hm.put("school", "*學校*");
        System.out.println(hm.get("school"));
    }
}
```

## 使用迭代器
以下是另一個例子, 我們使用迭代器 Iterator 將 HashMap 中的資料逐一印出. 關於迭代器的使用, 將以另一講次說明. 

```javascript
import java.util.*;

class Main {
    public static void main(String[] args) {
        HashMap hm=new HashMap();		
        
        hm.put("school", "學校");
        hm.put("student", "學生");
        hm.put("teacher", "老師");
		
        printInfo(hm);
    }
    
    private static void printInfo(HashMap hm){
        System.out.println("儲存資料共:" + hm.size() + "個");
        
        //使用迭代器將 HashMap 物件中的資料印出
        Iterator iterator = hm.entrySet().iterator();
        while (iterator.hasNext()) {
            Map.Entry pair = (Map.Entry)iterator.next();
            System.out.println(pair.getKey() + " = " + pair.getValue());
        }
    }
}
```
 
## HashMap 在文章處理的應用
以下是一個用 HashMap 計算一篇文章中用了那些英文單子的例子, 我們累計了各個出現的英文單字在文章中出現的次數. 
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
		
        //HashMap物件
        HashMap hm=new HashMap();		
        
        //累計英文單字出現次數
        for(int i=0; i<k.length; i++){
            if(!hm.containsKey(k[i])){
                hm.put(k[i], new Integer("1"));           //若單字不存在, 記錄出現1次
            }else{
                Integer m=(Integer)hm.get(k[i]);          //若單字已存在, 記錄累加1次
                Integer n=new Integer(m.intValue() + 1);
                hm.put(k[i], n);
            }
        }	
        
        printInfo(hm);
    }
    
    
    private static void printInfo(HashMap hm){
       System.out.println("儲存資料共:" + hm.size() + "個");
        
        //使用迭代器將 HashMap 物件中的資料印出
        Iterator iterator = hm.entrySet().iterator();
        while (iterator.hasNext()) {
            Map.Entry pair = (Map.Entry)iterator.next();
            System.out.println(pair.getKey() + " 出現 " + pair.getValue() + "次");
        }
    }
}
```

這個程式用了正規表示式 regular expression, 我們亦將以另一講次說明. 