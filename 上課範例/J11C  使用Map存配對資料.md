# J11C  使用Map存配對資料

## Map中的資料以(Key, Value)成對存放

```
Java專案
   |__ <com.abc>
   |       |__ Utility.java   
   |       |__ Argiculture.java
   |
   |__ Main.java
   |       
   |__ argiculture.csv (輸入檔)
   |__ out.csv         (輸出檔)
```


### (1) Utility.java

```java
package com.abc;

import java.io.*;
import java.util.List;
import java.util.ArrayList;

public class Utility{
    //============================================================
    // 從檔案讀入資料, 全部存在List物件中再回傳
    // 傳入: 檔名, String
    // 回傳: 檔案內容, List<String>
    //       失敗時回傳null
    //============================================================
    public static List<String> readData(String fileName) throws Exception{  
        // 存放輸出結果的物件
        List<String> results = new ArrayList();  
        
        //------------------------------------------      
        try{   
            // 建立檔案讀取及寫出物件  
            BufferedReader br = new BufferedReader(new FileReader(new File(fileName))); 
            
            // 逐行讀入檔案內容     
            String line;                 
            
            while ((line = br.readLine()) != null) {               
                // 將讀入資料加入results中
                results.add(line);
            }                              
            
            br.close();                        
        }catch(IOException e){ 
            // 失敗時        
            results = null;                  
        }         
        //------------------------------------------             
        
        // 回傳結果
        return results;
    } 
    

    //============================================================
    // 將List物件寫入檔案, 回傳true表示寫入成功, false表示失敗
    // 傳入: 檔名(String), 待寫資料(List<String>)
    // 回傳: boolean
    //============================================================    
    public static boolean writeData(String fileName, List<String> list) throws Exception{     
        boolean result = true;
        
        //------------------------------------------      
        try{   
            // 建立檔案讀取及寫出物件  
            BufferedWriter bw = new BufferedWriter(new FileWriter(new File(fileName))); 
            
            // 逐行寫出檔案內容  
            boolean firstLine=true;
            
            for(String data : list){
                if(firstLine){
                    bw.write(data);
                    firstLine=false;
                }else{
                    bw.write(("\n"));
                    bw.write(data);                
                }   
            }                            
            
            bw.close();                        
        }catch(IOException e){                
            result = false;                  
        }         
        //------------------------------------------             
        
        // 回傳結果
        return result;
    }     
}
```



### (2) Argiculture.java

```java
package com.abc;

import java.time.LocalDate;

public class Argiculture {
    //---------------------------
    // 成員
    //--------------------------- 
    public LocalDate transDate;
    public String market;
    public String name;
    public double highPrice;
    public double middlePrice;
    public double lowPrice;
    public double avgPrice;
    public double amount;

    //---------------------------  
    // 建構元(1) 傳8個參數
    //--------------------------- 
    public Argiculture(LocalDate transDate, String market, String name, double highPrice, double middlePrice, double lowPrice, double avgPrice, double amount){
        this.transDate = transDate;
        this.market = market;
        this.name = name;
        this.highPrice = highPrice;
        this.middlePrice = middlePrice;
        this.lowPrice = lowPrice;
        this.avgPrice = avgPrice;
        this.amount = amount;
    }
    
    //---------------------------  
    // 建構元(2) 傳0個參數
    //---------------------------           
    public Argiculture(){}

    //---------------------------  
    // getter
    //---------------------------  
    public LocalDate getTransDate(){return this.transDate;}
    public String getMarket(){return this.market;}
    public String getName(){return this.name;}
    public double getHighPrice(){return this.highPrice;}
    public double getMiddlePrice(){return this.middlePrice;}
    public double getLowPrice(){return this.lowPrice;}
    public double getAvgPrice(){return this.avgPrice;}
    public double getAmount(){return this.amount;}

    //---------------------------  
    // setter
    //--------------------------- 
    public void setTransDate(LocalDate transDate){this.transDate = transDate;}
    public void setMarket(String market){this.market = market;}
    public void setName(String name){this.name = name;}
    public void setHighPrice(double highPrice){this.highPrice = highPrice;}
    public void setMiddlePrice(double middlePrice){this.middlePrice = middlePrice;}
    public void setLowPrice(double lowPrice){this.lowPrice = lowPrice;}
    public void setAvgPrice(double avgPrice){this.avgPrice = avgPrice;}
    public void setAmount(double amount){this.amount = amount;} 			
}
```



### (3) Main.java

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Set;
import java.text.DecimalFormat;
import java.util.Map;
import java.util.TreeMap;

import com.abc.Score;
import com.abc.Utility;


class Main {
    public static void main(String[] args) throws Exception{
        //---------------------------------------------- 
        // 呼叫靜態方法讀入的資料, 存在data中
        //---------------------------------------------- 
        // 存放讀入的每行資料
        List<String> lines = Utility.readData("e:/exams.csv");
        
        // 存放待處理所有Score物件
        List<Score> data = new ArrayList();
        
        // 逐行處理資料
        lines.forEach(line -> {
            // 顯示目前處理的資料
            System.out.println(line);
            
            //切割欄位            
            String items[] = line.split(",");
                
            String stuNo = items[0].trim();
            String stuName = items[1].trim();
            int chi = Integer.parseInt(items[2].trim());
            int eng = Integer.parseInt(items[3].trim());                
            int stat = Integer.parseInt(items[4].trim());
            int comp = Integer.parseInt(items[5].trim());    
            
            // 產生成績物件, 加入data中
            data.add(new Score(stuNo, stuName, chi, eng, stat, comp));                       
        });  
        
        //********************************************************
        // 使用Map存放<Key, Value>資料
        //********************************************************
        Map<Integer, Integer> map = new TreeMap();

        // 累加考某個國文成績的人數
        data.forEach(s -> {    
            Integer score = s.getChi();            
            Integer cnt = map.get(score);
            
            if(cnt == null){
                map.put(score, 1);
            }else{
                cnt++;
                map.put(score, cnt);            
            }    
        });                  
        
        // 累加總資料數
        double total = 0;
        
        Set<Integer> keys = map.keySet();
        for(Integer key: keys){
            total += map.get(key);
            total++;
        }

        // 將Map中的物件加入output中
        List<String> output = new ArrayList(); 
        
        DecimalFormat df = new DecimalFormat("#.###");  //設定小數數值輸出格式
        
        for(Integer key: keys){
            String str = key + "," + map.get(key) + "," + df.format(map.get(key) / total);
            output.add(str);
        } 
        //********************************************************       


        //---------------------------------------------- 
        // 呼叫靜態方法, 將output內資料寫到檔案中
        //----------------------------------------------      
        boolean flag = Utility.writeData("e:/out.csv", output);
        
        if(flag){
            System.out.println("寫檔成功");
        }else{
            System.out.println("寫檔失敗");
        }
        //----------------------------------------------       
    }    
}
```
