# J11__02 用Collections排序Score物件

## (1) Score物件中有國文, 英文, 總分. 用何標準排序應寫在sort()內的Comparator物件中.

```
Java專案
   |__ com.abc
   |      |__ Score.java
   |
   |__ Main.java
```

### (1-1) Score.java

```java
package com.abc;

public class Score {
    //---------------------  
    // 成員
    //---------------------  
    private int chi;
    private int eng;

    //---------------------  
    // 建構元(1)
    //---------------------  
    public Score(int chi, int eng){
        this.chi = chi;
        this.eng = eng;        
    }

    //---------------------  
    // 建構元(2)
    //---------------------  
    public Score(){}
    
    //---------------------  
    // Getters
    //---------------------    
    public int getChi(){return this.chi;}
    public int getEng(){return this.eng;}
    
    //---------------------  
    // Setters
    //---------------------   
    public void setChi(int chi){this.chi = chi;}
    public void setEng(int eng){this.eng = eng;}
    
    //---------------------  
    // 計算總分的方法
    //---------------------    
    public int total(){
        return this.chi + this.eng;
    }
    
    //---------------------  
    // 改寫Object(父親)的
    // toString()方法
    //---------------------    
    @Override
    public String toString(){
        return "國文:" + this.chi + ", 英文:" + this.eng + ", 總分:" + this.total();
    }
    //---------------------       
}
```


### (1-2) Main.java

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
        // 以國文成績排序
        //============================ 
        Collections.sort(list, (x, y) -> {
            return y.getChi() - x.getChi();
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

