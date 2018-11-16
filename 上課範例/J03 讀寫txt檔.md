# J03 讀寫txt檔


## (1) 讀入一個txt檔

```
Java專案
   |__ Main.java
   |__ scores.txt (輸入檔)
```


### Main.java

```java
import java.io.*;

class Main {
    public static void main(String[] args) throws Exception {
        // 建立一個檔案讀取物件      
        File file = new File("scores.txt");
        FileReader fr = new FileReader(file);
        BufferedReader br = new BufferedReader(fr);        

        // 逐行讀入檔案內容
        //------------------------------------            
        String line;        
        while ((line = br.readLine()) != null) {            
            System.out.println(line);
        }
        //------------------------------------  
        
        // 關閉reader
        br.close();         
    }
} 
```


<br/>

## (2) 讀入一個txt檔, 寫出一個txt檔
```
Java專案
   |__ Main.java
   |__ scores.txt (輸入檔)
   |__ out.txt (輸出檔, 程式產生)    
```


### Main.java

```java
import java.io.*;

class Main {
    public static void main(String[] args) throws Exception {
        // 建立一個檔案讀取物件      
        File infile = new File("scores.txt");
        FileReader fr = new FileReader(infile);
        BufferedReader br = new BufferedReader(fr);        

        // 建立一個檔案寫出物件      
        File outfile = new File("out.txt");
        FileWriter fw = new FileWriter(outfile);
        BufferedWriter bw = new BufferedWriter(fw);        

        // 逐行讀入檔案內容
        //------------------------------------              
        String line; 
        boolean firstLine = true;
        
        while ((line = br.readLine()) != null) {            
            // 顯示讀入內容          
            System.out.println(line);

            // 將內容寫出檔案
            if(firstLine){
                bw.write(line);
                firstLine=false;
            }else{
                bw.write(("\n"));
                bw.write(line);                
            }    
        }
        //------------------------------------          

        // 關閉reader及writer, 強制輸出未寫出的暫存內容
        br.close();
        bw.close();      
    }
} 
```


<br/>

## (3) 讀入一個txt檔, 用try...catch捕捉錯誤
```
Java專案
   |__ Main.java
   |__ scores.txt (輸入檔)
```

### Main.java

```java
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        // 宣告檔案讀取變數
        BufferedReader br=null;
        
        //------------------------------------------      
        try{   
            // 建立檔案讀取物件  
            br = new BufferedReader(new FileReader(new File("scores.txt")));            
            
            // 逐行讀入檔案內容
            //---------------------            
            String line;        
            while ((line = br.readLine()) != null) {            
                System.out.println(line);
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
        }  
        //------------------------------------------         
    }    
}
```


<br/>

## (4) 讀入一個txt檔, 寫出一個txt檔, 用try...catch捕捉錯誤

```
Java專案
   |__ Main.java
   |__ scores.txt (輸入檔)
   |__ out.txt (輸出檔, 程式產生)    
```

### Main.java

```java
import java.io.*;

class Main {
    public static void main(String[] args) throws Exception{
        // 宣告輸入及輸出變數
        BufferedReader br = null;
        BufferedWriter bw = null;        

        //------------------------------------------
        try{
            // 建立一個檔案讀取及寫出物件      
            br = new BufferedReader(new FileReader(new File("scores.txt")));   
            bw = new BufferedWriter(new FileWriter(new File("out.txt")));        

            // 逐行讀入檔案內容
            //---------------------
            String line; 
            boolean firstLine = true;                
            
            while ((line = br.readLine()) != null) {            
                // 顯示讀入內容          
                System.out.println(line);

                // 將內容寫出檔案
                if(firstLine){
                    bw.write(line);
                    firstLine=false;
                }else{
                    bw.write(("\n"));
                    bw.write(line);                
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
            
            // 關閉writer, 強制輸出未寫出的暫存內容
            if(bw != null){
                bw.close(); 
            }    
        }  
        //------------------------------------------        
    }
} 
```
