# 走著走著, 就走到了三叉路口... 


## switch...case 指令的使用
如果程式在幾個不同值的條件下有各自不同的動作, 那麼使用 switch...case 指令有可能比用 if 指令簡潔, 以下是一個例子.
#### 問題: 如果會員等級為 'a' 時, 購物金額可打7折; 'b' 可打8折; 'c' 可打9折; 其他等級均打95折.
此問題用 switch...case 指令完成如下(假設已有一字元變數rank,代表會員等級; 另有total存放購物金額):
```javascript
//假設已有一個字元變數 rank, 也有一個 double 變數 total
switch(rank){
    case 'a':
        total*=0.7;
        break;
    case 'b':
        total*=0.8;
        break;
    case 'c':
        total*=0.9;
        break;
    default:
        total*=0.95;
}
System.out.println(total);
```
在上述的例子中變數 rank 的型態是字元, 因此判斷的值用一對單引號框住, 表示其為字元值. 
另外, 在每個條件值內敘述的最後一行 `break;` 表示接下來的程式流程將離開 switch 指令的範圍之外, 
在此其將接著執行 `System.out.println(total);` 指令. 如果不寫 `break;` 指令, 程式將從成立的條件開始, 執行其後
所有敘述, 直到遇到 `break;` 指令或是執行完 switch 指令的最後一行才結束.

 
## 多個條件執行相同程式時
如果程式中有多個條件將執行相同程式, 可以將條件寫在一起, 避免同一個程度片段出現多次, 降低日後維護程式的成本.
#### 問題: 如果會員等級為 'a' 及 'b' 時, 購物金額可打7折; 'c', 'd' 及 'e' 可打8折; 'f' 可打9折; 其他等級均打95折.
範例程式如下:
```javascript
//假設已有一個字元變數 rank, 也有一個 double 變數 total
switch(rank){
	case 'a':
    case 'b':
		total*=0.7;
        break;
    case 'c':
    case 'd':
    case 'e':
    	total*=0.8;
    	break;
	case 'f':
    	total*=0.9;
    	break;
    default:
     	total*=0.95;
}
System.out.println(total);
```