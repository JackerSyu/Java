# J08  使用List - 篩選資料

## (1) 輸出國文成績>=平均國文成績的資料

```
Java專案
   |__ <com.abc>
   |       |__ Score.java
   |
   |__ Main.java
   |       
   |__ exams.csv (輸入檔)
   |__ out.csv   (輸出檔)
```


### (1-1) Score.java

```java
package com.abc;

public class Score{
    //=====================
    // 成員    
    //=====================    
    private String stuNo;
    private String stuName;    
    private String gender;
    private int chi;
    private int eng;
    private int stat;
    private int comp;  
    
    //=====================    
    // 建構元(1)
    //=====================    
    public Score(String stuNo, String stuName, String gender, int chi, int eng, int stat, int comp){
        this.stuNo = stuNo;
        this.stuName = stuName;
        this.gender = gender;
        this.chi = chi;
        this.eng = eng;
        this.stat = stat;
        this.comp = comp;        
    }
    
    //=====================    
    // 建構元(2)    
    //=====================    
    public Score(){
        this.stuNo = null;
        this.stuName = null;
        this.gender = null;
        this.chi = 0;
        this.eng = 0;
        this.stat = 0;
        this.comp = 0;        
    }

    //=====================
    // getters
    //=====================    
    public String getStuNo(){return stuNo;}
    public String getStuName(){return stuName;}    
    public String getGender(){return gender;}
    public int getChi(){return chi;}
    public int getEng(){return eng;}
    public int getStat(){return stat;}
    public int getComp(){return comp;}
    
    //=====================    
    // setters
    //=====================    
    public void setStuNo(String stuNo){this.stuNo = stuNo;}
    public void setStuName(String stuName){this.stuName = stuName;}
    public void setGender(String gender){this.gender = gender;}
    public void setChi(int chi){this.chi = chi;}
    public void setEng(int eng){this.eng = eng;}
    public void setStat(int stat){this.stat = stat;}
    public void setComp(int comp){this.comp = comp;}
    
    //=====================    
    // 方法(總分)    
    //=====================    
    public int total(){
        return  chi + eng + stat + comp;                 
    }       
    //=====================    
}
```



### (1-2) Main.java

```java
package p36;

import java.io.*;
import java.util.ArrayList;
import java.util.List;
import com.abc.Score;

class Main {    
    public static void main(String[] args) throws IOException {
        // 宣告一個ArrayList用來儲存所有成績物件
        List<Score> list = new ArrayList<>();
        
        // 宣告檔案讀取及寫出變數
        BufferedReader br = null;
        BufferedWriter bw = null;        
   
        try{   
            // 建立檔案讀取及寫出物件  
            br = new BufferedReader(new FileReader(new File("d:/exams.csv"))); 
            bw = new BufferedWriter(new FileWriter(new File("d:/out.csv")));            
      
            // 逐行讀入檔案內容, 加入list中          
            String line;                 
            double totChi = 0;
            int cnt = 0;            
            
            while ((line = br.readLine()) != null) {    
                // 顯示輸入資料
                System.out.println(line);  
                
                // 切割欄位內容
                String items[] = line.split(",");
                
                String stuNo = items[0].trim();
                String stuName = items[1].trim();
                String gender = items[2].trim();
                int chi = Integer.parseInt(items[3].trim());
                int eng = Integer.parseInt(items[4].trim());                
                int stat = Integer.parseInt(items[5].trim());
                int comp = Integer.parseInt(items[6].trim());                

                //----------------------
                // 輸入資料的計算
                //----------------------               
                totChi+=chi;
                cnt++;
                
                // 產生一個成績物件並將資料透過建構元放入其中
                Score score = new Score(stuNo, stuName, gender, chi, eng, stat, comp);
                
                // 將成績物件加入ArrayList中
                list.add(score);                 
            }                                        
            
            
            // 將list中的成績物件依條件寫到檔案中
            boolean firstLine = true;  

            //----------------------   
            // 計算輸出條件
            //----------------------                        
            double avgChi = totChi / cnt;  
            
            System.out.println("國文平均:" + avgChi);
            
            for(Score s : list){
                //---------------------------                
                // 符合條件的資料再輸出    
                //---------------------------                
                if(s.getChi() >= avgChi){
                    String data = s.getStuNo() + "," + s.getStuName() + "," + s.getGender() + "," + s.getChi() + "," + s.getEng() + "," + s.getStat() + "," + s.getComp() + "," + s.total();
                
                    if(firstLine){
                        bw.write(data);
                        firstLine=false;
                    }else{
                        bw.write(("\n"));
                        bw.write(data);                
                    }                        
                }   
            }
            //----------------------------------------------           
        }catch(IOException e){
            System.out.println("發生錯誤, 原因: " + e);                     
            return;
        }finally{
            // 關閉reader
            if(br != null){
                br.close();              
            }  
            
            // 關閉writer
            if(bw != null){
                bw.close();              
            }              
        }       
    }    
}
```


<br/>

## (2) 輸出國文成績>=(平均國文成績+1倍標準差)的資料

```
Java專案
   |__ <com.abc>
   |       |__ Score.java
   |
   |__ Main.java
   |       
   |__ exams.csv (輸入檔)
   |__ out.csv   (輸出檔)
```

### (2-1) Score.java

```java
package com.abc;

public class Score{
    //=====================
    // 成員    
    //=====================    
    private String stuNo;
    private String stuName;    
    private String gender;
    private int chi;
    private int eng;
    private int stat;
    private int comp;  
    
    //=====================    
    // 建構元(1)
    //=====================    
    public Score(String stuNo, String stuName, String gender, int chi, int eng, int stat, int comp){
        this.stuNo = stuNo;
        this.stuName = stuName;
        this.gender = gender;
        this.chi = chi;
        this.eng = eng;
        this.stat = stat;
        this.comp = comp;        
    }
    
    //=====================    
    // 建構元(2)    
    //=====================    
    public Score(){
        this.stuNo = null;
        this.stuName = null;
        this.gender = null;
        this.chi = 0;
        this.eng = 0;
        this.stat = 0;
        this.comp = 0;        
    }

    //=====================
    // getters
    //=====================    
    public String getStuNo(){return stuNo;}
    public String getStuName(){return stuName;}    
    public String getGender(){return gender;}
    public int getChi(){return chi;}
    public int getEng(){return eng;}
    public int getStat(){return stat;}
    public int getComp(){return comp;}
    
    //=====================    
    // setters
    //=====================    
    public void setStuNo(String stuNo){this.stuNo = stuNo;}
    public void setStuName(String stuName){this.stuName = stuName;}
    public void setGender(String gender){this.gender = gender;}
    public void setChi(int chi){this.chi = chi;}
    public void setEng(int eng){this.eng = eng;}
    public void setStat(int stat){this.stat = stat;}
    public void setComp(int comp){this.comp = comp;}
    
    //=====================    
    // 方法(總分)    
    //=====================    
    public int total(){
        return  chi + eng + stat + comp;                 
    }       
    //=====================    
}
```



### (2-2) Main.java

```java
package p36;

import java.io.*;
import java.util.ArrayList;
import java.util.List;
import com.abc.Score;

class Main {    
    public static void main(String[] args) throws IOException {
        //---------------------------------------- 
        // 宣告一個ArrayList儲存所有成績物件
        //----------------------------------------        
        List<Score> list = new ArrayList<>();

        //----------------------------------------          
        // 宣告一個ArrayList儲存所有國文成績
        //----------------------------------------          
        List<Double> chiList = new ArrayList<>();
        
        // 宣告檔案讀取及寫出變數
        BufferedReader br = null;
        BufferedWriter bw = null;        
   
        try{   
            // 建立檔案讀取及寫出物件  
            br = new BufferedReader(new FileReader(new File("d:/exams.csv"))); 
            bw = new BufferedWriter(new FileWriter(new File("d:/out.csv")));            
      
            // 逐行讀入檔案內容, 加入list中          
            String line;                 
            int cnt = 0;            
            
            while ((line = br.readLine()) != null) {    
                // 顯示輸入資料
                System.out.println(line);  
                
                // 切割欄位內容
                String items[] = line.split(",");
                
                String stuNo = items[0].trim();
                String stuName = items[1].trim();
                String gender = items[2].trim();
                int chi = Integer.parseInt(items[3].trim());
                int eng = Integer.parseInt(items[4].trim());                
                int stat = Integer.parseInt(items[5].trim());
                int comp = Integer.parseInt(items[6].trim());                
               
                // 產生一個成績物件並將資料透過建構元放入其中
                Score score = new Score(stuNo, stuName, gender, chi, eng, stat, comp);
                
                // 將成績物件加入ArrayList中
                list.add(score);                 
                
                //-------------------------------------
                // 將國文成績物件加入ArrayList中
                //-------------------------------------                
                chiList.add(new Double(chi));                  
            }                                        
            
            
            //------------------------------------
            // 計算國文成績的平均數
            //------------------------------------
            double totChi = 0;
            double avgChi = 0;
            
            for(Double d : chiList){
                totChi += d;
            }            
            
            avgChi = totChi / chiList.size();
            
            System.out.println("國文平均數:" + avgChi);            
            //------------------------------------

            
            //------------------------------------
            // 計算國文成績的標準差
            //------------------------------------
            double tdChi = 0;
            double stdChi = 0;
            
            for(Double d : chiList){
                tdChi += Math.pow((d-avgChi), 2);
            }            
            
            stdChi = Math.sqrt(tdChi / chiList.size());
            
            System.out.println("國文標準差:" + stdChi);
            //------------------------------------

            
            
            // 將list中的成績物件依條件寫到檔案中
            boolean firstLine = true;                 
            
            for(Score s : list){
                //---------------------------                
                // 符合條件的資料再輸出    
                //---------------------------                
                if(s.getChi() >= (avgChi + stdChi)){
                    String data = s.getStuNo() + "," + s.getStuName() + "," + s.getGender() + "," + s.getChi() + "," + s.getEng() + "," + s.getStat() + "," + s.getComp() + "," + s.total();
                
                    if(firstLine){
                        bw.write(data);
                        firstLine=false;
                    }else{
                        bw.write(("\n"));
                        bw.write(data);                
                    }                        
                }   
            }
            //----------------------------------------------           
        }catch(IOException e){
            System.out.println("發生錯誤, 原因: " + e);                     
            return;
        }finally{
            // 關閉reader
            if(br != null){
                br.close();              
            }  
            
            // 關閉writer
            if(bw != null){
                bw.close();              
            }              
        }       
    }    
}
```



<br/>

## (3) 改寫範例(2)

```
Java專案
   |__ <com.abc>
   |       |__ Score.java
   |
   |__ Main.java
   |       
   |__ exams.csv (輸入檔)
   |__ out.csv   (輸出檔)
```

### (3-1) Score.java

```java
package com.abc;

public class Score{
    //=====================
    // 成員    
    //=====================    
    private String stuNo;
    private String stuName;    
    private String gender;
    private int chi;
    private int eng;
    private int stat;
    private int comp;  
    
    //=====================    
    // 建構元(1)
    //=====================    
    public Score(String stuNo, String stuName, String gender, int chi, int eng, int stat, int comp){
        this.stuNo = stuNo;
        this.stuName = stuName;
        this.gender = gender;
        this.chi = chi;
        this.eng = eng;
        this.stat = stat;
        this.comp = comp;        
    }
    
    //=====================    
    // 建構元(2)    
    //=====================    
    public Score(){
        this.stuNo = null;
        this.stuName = null;
        this.gender = null;
        this.chi = 0;
        this.eng = 0;
        this.stat = 0;
        this.comp = 0;        
    }

    //=====================
    // getters
    //=====================    
    public String getStuNo(){return stuNo;}
    public String getStuName(){return stuName;}    
    public String getGender(){return gender;}
    public int getChi(){return chi;}
    public int getEng(){return eng;}
    public int getStat(){return stat;}
    public int getComp(){return comp;}
    
    //=====================    
    // setters
    //=====================    
    public void setStuNo(String stuNo){this.stuNo = stuNo;}
    public void setStuName(String stuName){this.stuName = stuName;}
    public void setGender(String gender){this.gender = gender;}
    public void setChi(int chi){this.chi = chi;}
    public void setEng(int eng){this.eng = eng;}
    public void setStat(int stat){this.stat = stat;}
    public void setComp(int comp){this.comp = comp;}
    
    //=====================    
    // 方法(總分)    
    //=====================    
    public int total(){
        return  chi + eng + stat + comp;                 
    }       
    //=====================    
}
```



### (3-2) Main.java

```java
package p36;

import java.io.*;
import java.util.ArrayList;
import java.util.List;
import com.abc.Score;

class Main {    
    public static void main(String[] args) throws IOException {
        //---------------------------------------- 
        // 宣告一個ArrayList儲存所有成績物件
        //----------------------------------------        
        List<Score> list = new ArrayList<>();

        //----------------------------------------          
        // 宣告一個ArrayList儲存所有國文成績
        //----------------------------------------          
        List<Double> chiList = new ArrayList<>();
        
        // 宣告檔案讀取及寫出變數
        BufferedReader br = null;
        BufferedWriter bw = null;        
   
        try{   
            // 建立檔案讀取及寫出物件  
            br = new BufferedReader(new FileReader(new File("d:/exams.csv"))); 
            bw = new BufferedWriter(new FileWriter(new File("d:/out.csv")));            
      
            // 逐行讀入檔案內容, 加入list中          
            String line;                 
            int cnt = 0;            
            
            while ((line = br.readLine()) != null) {    
                // 顯示輸入資料
                System.out.println(line);  
                
                // 切割欄位內容
                String items[] = line.split(",");
                
                String stuNo = items[0].trim();
                String stuName = items[1].trim();
                String gender = items[2].trim();
                int chi = Integer.parseInt(items[3].trim());
                int eng = Integer.parseInt(items[4].trim());                
                int stat = Integer.parseInt(items[5].trim());
                int comp = Integer.parseInt(items[6].trim());                
               
                // 產生一個成績物件並將資料透過建構元放入其中
                Score score = new Score(stuNo, stuName, gender, chi, eng, stat, comp);
                
                // 將成績物件加入ArrayList中
                list.add(score);                 
                
                //-------------------------------------
                // 將國文成績物件加入ArrayList中
                //-------------------------------------                
                chiList.add(new Double(chi));                  
            }                                        
            
            
            //--------------------------------------------
            // 計算國文成績的平均數
            //--------------------------------------------
            double avgChi = average(chiList);
            System.out.println("國文平均:" + avgChi);
            //--------------------------------------------

            
            //--------------------------------------------
            // 計算國文成績的標準差
            //--------------------------------------------
            double stdChi = standardDev(chiList);
            System.out.println("國文標準差:" + stdChi);            
            //--------------------------------------------

            
            
            // 將list中的成績物件依條件寫到檔案中
            boolean firstLine = true;                 
            
            for(Score s : list){
                //---------------------------                
                // 符合條件的資料再輸出    
                //---------------------------                
                if(s.getChi() >= (avgChi + stdChi)){
                    String data = s.getStuNo() + "," + s.getStuName() + "," + s.getGender() + "," + s.getChi() + "," + s.getEng() + "," + s.getStat() + "," + s.getComp() + "," + s.total();
                
                    if(firstLine){
                        bw.write(data);
                        firstLine=false;
                    }else{
                        bw.write(("\n"));
                        bw.write(data);                
                    }                        
                }   
            }
            //----------------------------------------------           
        }catch(IOException e){
            System.out.println("發生錯誤, 原因: " + e);                     
            return;
        }finally{
            // 關閉reader
            if(br != null){
                br.close();              
            }  
            
            // 關閉writer
            if(bw != null){
                bw.close();              
            }              
        }       
    } 
    
    
    //======================================================
    // 計算平均數
    //======================================================
    public static double average(List<Double> data){
        double tot = 0;
            
        for(Double d : data){
            tot += d;
        }            
            
        return tot / data.size(); 
    }
        
    //======================================================
    // 計算標準差
    //======================================================
    public static double standardDev(List<Double> data){
        double tot = 0;           
        double avg = average(data);
        
        for(Double d : data){
            tot += Math.pow((d - avg), 2);
        }            
            
        return Math.sqrt(tot / data.size());
    }    
    //======================================================    
}
```
