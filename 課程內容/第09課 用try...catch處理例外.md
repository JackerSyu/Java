# 再怎麼說, 都不希望程式執行時彈出錯誤畫面.


## 使用try...catch敘述
在Java程式執行期間有可能發生不預期的錯誤, 比方說, 連結主機時網路不通, 連資料庫時主機未開機, 使用者輸入錯誤值等等情況. 
當不預期狀況發生時, 我們稱其發生了一個例外(Exception), 如果沒有敘述可處理例外, 程式將會停止並顯示執行錯誤訊息. 以下是一個例子:

```javascript
Scanner scanner=new Scanner(System.in);
		
String id = scanner.next();
String gender=id.substring(1,2);
		
if(gender.equals("1")){
	System.out.println("男");
}else if(gender.equals("2")){
	System.out.println("女");
}else{
	System.out.println("輸入錯誤");
}
```

以上的程式使用的 Scanner 類別存在 java.util 套件中, 因此使用前請加入 `import java.util.*;` 指令才能正確引用.
本程式由使用者輸入一個身份證字號字串, 程式根據字串第 2 碼判斷性別. 
在輸入正確時, 程式可以執行無誤; 但如果使用者輸入字串不足 2 碼,
程式將切不到第 2 碼, 並且造成 StringIndexOutOfBoundException 的例外.

為了避免例外導致程式中斷, 以下改寫由 try...catch 捕捉例外.
```javascript 
Scanner scanner=new Scanner(System.in);
String id = scanner.next();
	
try{	
	String gender=id.substring(1,2);
				
	if(gender.equals("1")){
		System.out.println("男");
	}else if(gender.equals("2")){
		System.out.println("女");
	}else{
		System.out.println("輸入錯誤");
	}
}catch(StringIndexOutOfBoundsException e){
	System.out.println("輸入資料長度不足");
	return;
}
```	

以上的程式可捕捉 StringIndexOutOfBoundsException, 但若發生其他種類的例外, 仍會發生程式執行錯誤.

 

## 捕捉不同的例外
使用 try...catch 可以捕捉程式執行時的例外, 也可以透過多個 catch 指令捕捉不同的例外, 以下是一個例子:

```javascript
Scanner scanner=new Scanner(System.in);
String id = scanner.next();
	
try{	
	String gender=id.substring(1,2);
	int k=Integer.parseInt(gender);
				
	if(k==1){
		System.out.println("男");
	}else if(k==2){
		System.out.println("女");
	}else{
		System.out.println("輸入錯誤");
	}
}catch(StringIndexOutOfBoundsException e){
	System.out.println("輸入資料長度不足");
	return;
}catch(NumberFormatException e){
	System.out.println("身份證第二碼應是數字");
	return;		
}
``` 
以上的程式使用兩個 catch 指令, 捕捉 StringIndexOutOfBoundsException 及 NumberFormatException,
並且對此兩種例外分別給予不同訊息.



## 捕捉所有的例外
如果 catch 指令沒有指定特定例外, 那麼當任何例外產生時均被捕捉, 以下是一個例子:

```javascript
Scanner scanner=new Scanner(System.in);
String id = scanner.next();
	
try{	
	String gender=id.substring(1,2);
	int k=Integer.parseInt(gender);
				
	if(k==1){
		System.out.println("男");
	}else if(k==2){
		System.out.println("女");
	}else{
		System.out.println("輸入錯誤");
	}
}catch(Exception e){
	System.out.println("輸入資料長度應足夠且身份證第二碼應是數字");
	return;		
}	
``` 
以上的程式捕捉 Exception, 其他不同的例外都繼承它, 因此所有的例外都會滿足被捕捉的條件.



## 不管有沒有例外, 結束前都到 finally 區塊
如果有指定 finally 敘述, 不管是否發生例外, 程式流程在 try 或 catch 執行完後均會進入 finally 指令執行.

```javascript
Scanner scanner=new Scanner(System.in);
String id = scanner.next();
String msg=null;
	
try{	
	String gender=id.substring(1,2);
	int k=Integer.parseInt(gender);
				
	if(k==1){
		msg="男";
	}else if(k==2){
		msg="女";
	}else{
		msg="輸入錯誤";
	}
}catch(Exception e){
	msg="輸入資料長度應足夠且身份證第二碼應是數字";		
}finally{
	System.out.println(msg);
}
``` 