# J07 Getters及Setters


## (1) 完成Score的private成員取存方法

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
    private int chi;
    private int eng;
    private int stat;
    private int comp;  
    
    //=====================    
    // 建構元(1)
    //=====================    
    public Score(String stuNo, String stuName, int chi, int eng, int stat, int comp){
        this.stuNo = stuNo;
        this.stuName = stuName;
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
    public int getChi(){return chi;}
    public int getEng(){return eng;}
    public int getStat(){return stat;}
    public int getComp(){return comp;}
    
    //=====================    
    // setters
    //=====================    
    public void setStuNo(String stuNo){this.stuNo = stuNo;}
    public void setStuName(String stuName){this.stuName = stuName;}
    public void setChi(int chi){this.chi = chi;}
    public void setEng(int eng){this.eng = eng;}
    public void setStat(int stat){this.stat = stat;}
    public void setComp(int comp){this.comp = comp;}
    
    //=====================    
    // 方法(總分)    
    //=====================    
    public double total(){
        return  chi * 2 + eng * 2 + stat * 1.5 + comp * 2.5;                 
    }   
    
    //=====================    
    // 方法(平均)    
    //=====================    
    public double average(){
        return  total() / 8;                 
    }     
    //=====================    
}
```


### (1-2) Main.java

```java
import java.io.*;
import com.abc.Score;

class Main {
    public static void main(String[] args) throws IOException {
        // 宣告檔案讀取及寫出變數
        BufferedReader br = null;
        BufferedWriter bw = null;
        
        //------------------------------------------      
        try{   
            // 建立檔案讀取及寫出物件  
            br = new BufferedReader(new FileReader(new File("d:/exams.csv"))); 
            bw = new BufferedWriter(new FileWriter(new File("d:/out.csv")));
            
            // 逐行讀入檔案內容
            //--------------------- 
            boolean firstLine = true;            
            String line;     
            
            while ((line = br.readLine()) != null) { 
                // 顯示讀入的資料
                System.out.println(line); 
                
                //切割欄位內容
                String items[] = line.split(",");
                
                String stuNo = items[0].trim();
                String stuName = items[1].trim();
                int chi = Integer.parseInt(items[2].trim());
                int eng = Integer.parseInt(items[3].trim());                
                int stat = Integer.parseInt(items[4].trim());
                int comp = Integer.parseInt(items[5].trim());                

                // 產生成績物件並將資料透過建構元放入物件中
                Score score = new Score(stuNo, stuName, chi, eng, stat, comp); 
                
                // 將物件內容寫至檔案
                String data = score.getStuNo() + "," + score.getStuName() + "," + score.getChi() + "," + score.total() + "," + score.average();
                
                if(firstLine){
                    bw.write(data);
                    firstLine=false;
                }else{
                    bw.write(("\n"));
                    bw.write(data);                
                }                
            }                   
            //---------------------            
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
        //------------------------------------------         
    }    
}
```


<br/>

## (2) Overloading - total()及total(double, double, double, double)

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
    //成員    
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
    public double total(){
        return  chi + eng + stat + comp;                 
    }  
  
    //=====================    
    // 方法(加櫂總分)    
    //=====================    
    public double total(double wChi, double wEng, double wStat, double wComp){
        return  chi * wChi + eng * wEng + stat * wStat + comp * wComp;                 
    }      
  
    //=====================    
    // 方法(平均)    
    //=====================    
    public double average(){
        return  total() / 4;                 
    } 
    
    //=====================    
    // 方法(加櫂平均)    
    //=====================    
    public double average(double wChi, double wEng, double wStat, double wComp){
        return  total(wChi, wEng, wStat, wComp) / (wChi + wEng + wStat + wComp);                 
    } 
    //=====================     
}
```


### (2-2) Main.java

```java
import java.io.*;
import com.abc.Score;

class Main {
    public static void main(String[] args) throws IOException {
        // 宣告檔案讀取及寫出變數
        BufferedReader br = null;
        BufferedWriter bw = null;
        
        //------------------------------------------      
        try{   
            // 建立檔案讀取及寫出物件  
            br = new BufferedReader(new FileReader(new File("d:/exams.csv"))); 
            bw = new BufferedWriter(new FileWriter(new File("d:/out.csv")));
            
            // 逐行讀入檔案內容
            //--------------------- 
            boolean firstLine = true;            
            String line;     
            
            while ((line = br.readLine()) != null) {  
                // 顯示讀入的資料
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

                // 產生成績物件並將資料透過建構元放入物件中
                Score score = new Score(stuNo, stuName, gender, chi, eng, stat, comp);  
                
                //將物件內容寫至檔案
                String data = score.getStuNo() + "," + score.getStuName() + "," + score.getGender() + "," +  "," + score.total(2, 2, 1.5, 2); 
                
                if(firstLine){
                    bw.write(data);
                    firstLine=false;
                }else{
                    bw.write(("\n"));
                    bw.write(data);                
                }                
            }                   
            //---------------------            
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
        //------------------------------------------         
    }    
}
```
