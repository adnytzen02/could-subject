## 格式

* 常用格式 一
```js
If   [  條件判斷式 ]  ;  then
	命令語句
fi     <==將 if 反過來寫，結束 if 之意！
```

---
* 常用格式 二

```js
if 條件; then
    命令語句
else
    命令語句
fi
```
```js
if 條件
then
   命令語句
else
   命令語句
fi
```

* read命令後面，如果沒有指定變數名，讀取的資料將被自動賦值給特定的變數REPLY
```js
語法
read(選項)(參數)
選項
-p：指定讀取值時的提示字元；
-t：指定讀取值時等待的時間（秒）。
參數
變數：指定讀取值的變數名
```
* 另一寫法,read 沒變數  $REPLY
```js
#!/bin/bash
clear
read -p "請在5秒內猜1到9 一個數字?" -t 5
echo "您輸入的是:"$REPLY
if [ "$REPLY" = "5" ] ; then
echo "答對了!"
fi
echo "程式結束!"
```

## ping 命令

* 語法
```js
ping -參數 主機位址
```
* 選項
```js
-c<完成次數>：設置完成要求回應的次數
-w 1 等待回應時間為一秒
```


```js
ping：查詢網路上某台主機是否開著
ping -參數 主機位址
c 次數：送幾次封包給這台主機，然後等待回應
d：設定SO_DEBUG選項
f：大量且快速的送網路封包給一台主機，看它的回應
i 秒數：設定幾秒鐘送一次封包給一台主機，預設值1秒
q：不顯示傳送封包的資訊，只顯示最後結果
l 次數：在次數內，以最快速的方式送封包給一台主機
```

* 等待回應時間為一秒 (-w 1)
```js
ping命令
網路測試
ping命令用來測試主機之間網路的連通性。
執行ping指令會使用ICMP傳輸協定，發出要求回應的資訊，
若遠端主機的網路功能沒有問題，就會回應該資訊，因而得知該主機運作正常。
```
* 語法
ping(選項)(參數)
* 選項
```js
-d：使用Socket的SO_DEBUG功能；
-c<完成次數>：設置完成要求回應的次數；
-f：極限檢測；
-i<間隔秒數>：指定收發資訊的間隔時間；
-I<網路介面>：使用指定的網路介面送出資料包；
-l<前置載入>：設置在送出要求資訊之前，先行發出的資料包；
-n：只輸出數值；
-p<範本樣式>：設置填滿資料包的範本樣式；
-q：不顯示指令執行過程，開頭和結尾的相關資訊除外；
-r：忽略普通的Routing Table，直接將資料包送到遠端主機上；
-R：記錄路由過程；
-s<數據包大小>：設置數據包的大小；
-t<存活數值>：設置存活數值TTL的大小；
-v：詳細顯示指令的執行過程。
```
* 參數
    * 目的主機：指定發送ICMP報文的目的主機。
