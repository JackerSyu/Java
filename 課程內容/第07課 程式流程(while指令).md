# 不知有多少個要處理, 但是聽到繼續工作的口令就繼續工作.


## while 迴圈指令的使用
如果有一段程式需要重覆執行, 如果不用 for 迴圈寫, 也可以選擇使用 while 迴圈指令. 
舉例來說, 以下 while 迴圈計算 1~100 的總合.
```javascript
int i=1;
int total=0;

while(i<=100){
	total+=i;
	i++;
}

System.out.println(total);
```
上述的例子中, `while(i<=100)` 指令中的 `(i<=100)` 是執行迴圈的條件, 當條件成立時, 迴圈內的指令就依序執行,
等到迴圈指令執行完成後, 再度檢查迴圈執行條件, 判斷是否再次執行迴圈內容.



## 離開 while 迴圈
while 迴圈執行的次數通常是未知的, 舉例來說, 我們有時會使用 while 迴圈處理讀取到的每一筆記錄, 
當資料已完全讀完後就離開迴圈.
```javascript
//設定一個布林變數eof, 初值設定為false
//讀取一筆資料, 若讀不到就設定eof變數為true

while(!eof){
	//進行讀入資料的處理
	//再讀取一筆資料, 若讀不到就設定eof變數為true
}
```


## 使用 break 指令離開 while 迴圈
在某些應用中, while 迴圈會被設定為無窮迴圈, 在某些條件成立後才使用 `break;` 指令離開迴圈,
以下是一個例子.
```javascript
while(true){
	int i=(int)(Math.random()*100);
	System.out.println(i);
	if(i==50) break;
}
```
在以上的例子中, `while(true)` 有一個永遠都成立的條件, 因此迴圈每次的檢查都會成立. 
在此當 i 的值等於50時, 就使用 `break;` 指令離開迴圈. 



## 使用 do...while 迴圈
和 while 迴圈指令有些不同, do...while 迴圈指令將判斷執行迴圈的條件寫在後需, 
這表示迴圈內容將至少被執行一次, 以下是一個例子.
```javascript
do{
	int i=(int)(Math.random()*100);
	System.out.println(i);
	if(i==50) break;
}while(true);
```
在以上的例子中, `while(true);` 指令被放在迴圈之後, 條件成立時再進入迴圈執行.