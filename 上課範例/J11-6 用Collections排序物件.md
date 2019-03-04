# J11-6 用Collections排序物件

## (1) Score中有國文, 英文及總分. 用何標準排序應寫在sort()內的Comparator物件中.

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
        return "國文:" + this.getChi() + ", 英文:" + this.getEng() + ", 總分:" + this.total();
    }
    //---------------------       
}
```


### (1-2) Main.java

```java
import java.util.Collections;
import java.util.ArrayList;
import java.util.List;

import com.abc.Score;

public class Main {
    public static void main(String[] args) {
        //----------------------------
        // 存放資料的List物件
        //----------------------------
        List<Score> list = new ArrayList();

        //----------------------------
        // 將資料加入List物件,
        // int自動被包裝成Integer,
        // 稱為auto boxing.
        //----------------------------        
        list.add(new Score(86, 67));
        list.add(new Score(96, 87));
        list.add(new Score(46, 47));
        list.add(new Score(76, 69));
        list.add(new Score(77, 76));
        list.add(new Score(74, 79));
        list.add(new Score(96, 97));
        list.add(new Score(66, 87));
        list.add(new Score(98, 99));
        list.add(new Score(100, 95));

        //============================
        // 以國文成績排序
        //============================ 
        Collections.sort(list, (x, y) -> {
            return y.getChi() - x.getChi();
        });

        //----------------------------
        // 輸出list內容
        //----------------------------          
        list.forEach(d -> {
            System.out.println(d.toString());
        });
        //----------------------------          
    }    
}
```


<br/>

## (2) Score中有國文, 英文及總分, 可選用多個排序欄位.

```
Java專案
   |__ com.abc
   |      |__ Score.java
   |
   |__ Main.java
```

### (2-1) Score.java

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
        return "國文:" + this.getChi() + ", 英文:" + this.getEng() + ", 總分:" + this.total();
    }
    //---------------------       
}
```


### (2-2) Main.java

```java
import java.util.Collections;
import java.util.ArrayList;
import java.util.List;

import com.abc.Score;

public class Main {
    public static void main(String[] args) {
        //----------------------------
        // 存放資料的List物件
        //----------------------------
        List<Score> list = new ArrayList();

        //----------------------------
        // 將資料加入List物件,
        // int自動被包裝成Integer,
        // 稱為auto boxing.
        //----------------------------        
        list.add(new Score(86, 67));
        list.add(new Score(96, 87));
        list.add(new Score(46, 47));
        list.add(new Score(76, 69));
        list.add(new Score(77, 76));
        list.add(new Score(74, 79));
        list.add(new Score(96, 97));
        list.add(new Score(66, 87));
        list.add(new Score(98, 99));
        list.add(new Score(100, 95));

        //============================
        // 以總分成績排序,
        // 同分時再用國文,
        // 接著是英文.
        //============================ 
        Collections.sort(list, (x, y) -> {
            if(x.total() != y.total()){
                return y.total() - x.total();
            }else if(x.getChi() != y.getChi()){
                return y.getChi() - x.getChi();
            }else{
                return y.getEng() - x.getEng();
            }    
        });

        //----------------------------
        // 輸出list內容
        //----------------------------          
        list.forEach(d -> {
            System.out.println(d.toString());
        });
        //----------------------------          
    }    
}
```

