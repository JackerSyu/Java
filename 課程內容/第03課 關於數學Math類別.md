# Math類別中有很多靜態方法, 不必產生小白, 直接呼叫就好.


## Math類別方法的使用
在JDK文件中, 我們可以查到Math類別中有一個abs方法, 它會回傳輸入值的絕對值, 如下:
```
static double abs(double a)
              Returns the absolute value of a double value.
```
比較特別的是, 它是一個靜態方法, 它在記載體中只有一份, 而且不會依賴這個類別產生的物件而存在. 
所以我們要呼叫它時, 只要直接以類別名稱開頭, 在一個小數點後, 接著方法名稱即可, 如下:
```javascript
double a=Math.abs(100);  //a的值是100.0
double b=Math.abs(-100); //b的值也是100.0
```

靜態方法的設計是有道理的, 想想同樣是計算-100的絕對值, 在小白或小黑物件上呼叫都會回傳100, 
不會因為物件的不同而有不同結果. Java因此將其設計為static, 只要存一份, 有效運用記憶體空間.


## Math類別中的靜態成員
在Math類別中定義了兩個靜態成員, 如下:
```
static double E
              The double value that is closer than any other to e, the base of the natural logarithms.
```
```
static double PI
              The double value that is closer than any other to pi, the ratio of the circumference of a circle to its diameter.
```
它們是常數, 在Java中以全大寫字母表示, 包括自然對數的底E及圓周率PI. 我們稱它們為常數是因為它們的值是恆常不變的, 我們也不能在程式中改變它們的內容. 
例如PI, 它的值約是3.14159265, 我們可以在程式中直接使用, 不必自行輸入數值. 以下是印出半徑為10圓面積的程式:
```javascript
System.out.println(10*10*Math.PI);
```
因為PI在Math類別中也被宣告為static靜態的, 因此我們也可以直接使用它, 不必先產生物件.


## 視頻教學
```
(1)J03_01 Math.sqrt()靜態方法      http://www.youtube.com/watch?v=Ht8_f83IP88
(2)J03_02 Math.PI靜態成員          http://www.youtube.com/watch?v=9N7RIO5nqak
(3)J03_03 Math.pow()靜態方法       http://www.youtube.com/watch?v=R7uST8Udtp0
```
