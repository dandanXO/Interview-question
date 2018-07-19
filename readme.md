
# 系統概念與開發工具
## 請列出 Unix-like 系統上 5 個常用的指令並描述使用時機與用法
1. ls -a 列出目錄下的所有文件，包括以. 開頭的隱含文件。
    ls -l 列出文件的詳細訊息息。
2. cp -r xxx yyy 完整複製 xxx至yyy 
3. cd 更改當前所在位置
4. mkdir  新建資料夾
5. rm 刪除檔案或目錄

## 請描述 Unix-like 系統的使用經驗
一開始接觸Unix-like 系統時才知道原來有不同的作業系統，當時都是依循著鳥哥網站教學所學的，接觸時間也不算久，我心目中unix-like系統的靈魂價值應該是服務與多用戶;從開始初學的基礎指令到架起服務只要有一本良好的手撤或說明書應該都能達成。而shell的操作自如則是最終的目標。

## 請列出平常慣用的 IDE 或編輯器
vscode 
eclipse

## 請列出使用過或玩過的版本控制系統
只使用過git	

## 請說明 process 與 thread 的差異
process: Process 意旨已經執行並且載入 到記憶體中的 Program ，process中的每一行程式碼隨時都有可能被CPU執行，每一個 Process 是互相獨立的，且Process 本身不是基本執行單位，而是 Thread (執行緒)的容器。
thresd: 在同一個 Process 中會有很多個 Thread ，每一個 Thread 負責某一項功能，同一個 Process 底下的 Thread 共享資源，如 記憶體、變數等，不同的Process 則否。
# 程式設計概念
## 請描述物件導向中的封裝跟繼承，在什麼情境使用過？
我用java來解釋
1. 封裝: 就是把邏輯或知識給取個名字也就是方法名稱，定義傳入與傳出 然後把將同性質的邏輯(方法)，集合在一起，建立一個class (物件藍圖) 。
2. 繼承: 其目的就是讓"程式碼再利用"，可以適當的切割類別，並在衍生類別中重複使用、擴充和修改基底類別中定義的行為，又不破壞原先基底類別設計。
3. 使用情境: 在我的大學專題中有一個情況是這樣，在APP中分成需求者與供應者2種角色，因此先封裝一個CALSS為"角色"有基本的姓名與電話號碼，在創建A(供應者)class和B(需求者)class去繼承剛剛的"角色"class這樣基本資料的方法就不用一直重法打了。
4. 請描述 interface 的使用情境
	當你一個想要繼承的方法跳脫出固有abstract class的性質時就可以使用interface來達成
	例如:們需要有 開/關 方法 與警報方法
	就可以寫成這樣
```java
abstract class Door {  

 abstract void open();  

 abstract void close()；  

}  

interface Alarm {  

 void alarm();  

}  

class AlarmDoor extends Door implements Alarm {  

 void open() { … }  

 void close() { … }  

    void alarm() { … }  

}  
```

 
## 聽過哪些 Design Pattern，在什麼情境使用過？
比較常寫js 有聽聽過 "中介者模式(Mediator Pattern)" express框架似乎就是此模式開發(可能有誤)，各個元件不用知道彼此的情形，只要專心處理自己的事，元件之間所需要的互動就交給 Mediator 來負責就好。例如有一個網頁應用程式，它允許使用者點擊專輯，然後播放音樂。
```javascript
$('#album').on('click', function(e) {
	e.preventDefault();
	var albumId = $(this).id();
	mediator.publish("playAlbum", albumId);
});
var playAlbum = function(id) {
	…
	mediator.publish("albumStartedPlaying", {songList: [..], currentSong: "Without You"});
};
var logAlbumPlayed = function(id) {
	//Log the album in the backend
};
var updateUserInterface = function(album) {
	//Update UI to reflect what's being played
};
//Mediator subscriptions
mediator.subscribe("playAlbum", playAlbum);
mediator.subscribe("playAlbum", logAlbumPlayed);
mediator.subscribe("albumStartedPlaying", updateUserInterface);
```
	
## call by value 與 call by reference 的差別是什麼？

用C++大概舉例
1. Call by value(直接把值丟到不同記憶題): 參數在被程式呼叫之後，主程式的參數的值不會受到副程式的影響，以及副程式和主程式所使用的參數的記憶體位置是不同的。

2. Call by reference(指向同一個記憶體位置):參數在被副程式呼叫之後，主程式的值會受到副程式的影響，以及副程式和主程式所使用的參數的記憶體位置是相同的。


## 請說明 MVC 架構、你知道的 MVC framework 以及使用感想
把系統分成三個部份: Model、View、Controller的軟體架構
1. Model: 資料庫、演算法、程式功能
2. View: UI、UX
3. Controller: 負責轉發請求，對請求進行處理
蒐集使用者於View中所輸入的資料，並決定由哪一支程式進行處理接收Model傳回的資料，解析後傳給View呈現
	
我認為MVC 並沒有一定的樣子(架構)，MVC的重點在於分化程式的職責，像是我用的node.js express 其實Router本身就會涵蓋了controller及model的部分，因此我認為，開發一個專案，專案上要怎麼分化整個程式的職責，其實都是由當時的情況來做考量。且若有一同開發後端的工程師夥伴，就需要跟他們進行溝通，並商榷要用什麼方式來進行開發。


## 請寫出一個 regular expression 可容許台灣身分證字號格式（英文字母開頭，第二位只能是1 或 2，全長10個字元）
	/[A-Za-z][1-2][0-9]{8,8}$/

##　請解釋 GC(garbage collection) 概念
就我的認知來回答，Java 跟 C 語言不一樣，它不需要自行解構，Java 語言會自動刪除不必要的物件，Java 語言並不會在程式碼中指定記憶體或移除，所以有些人會透過將相應的物件（譯註：應為物件參照）設為 null，或透過呼叫 System.gc() 來達到效果。


## 請 refactor 這段程式碼（ https://pastebin.com/XQ7iBq0T ）
讓它有功能分隔明確的程式結構。
假設未於此定義的 class，如 Order、Mailer 等的使用及實作邏輯是正確的，可任意增刪及 rename class、function。
如有多 class 放在同一檔案即可，並以註解說明修改原因，最後使用 https://pastebin.com/ 產生答案連結貼於此。

新增setHeader 與 request 兩個function 就由此簡化程式碼的重複性。
	https://pastebin.com/mkwAmT7k

# 網頁程式相關概念
## 請描述 GET 與 POST 的差異
簡單說就是傳送資料的header 放資料的地方不同
post 允許message-body 的存在get則否
	get 傳輸資料會在url中以 host.com/get?xxx=yyy傳送
## 請描述 HTTP 與 HTTPS 的差異
S的差別代表了網站使用編碼協定的安全性(secure)，簡單說前者是未經過加密的明文傳輸，後者則是有使用SSL協定取得憑證加密之後才傳輸。

## 請說明 cookie 的作用與使用情境
可將依些不敏感或是不太需要驗證的資訊放在使用端，可用於提升使用者體驗像是頁面上的資料填到一半，不小心把網頁關掉，這時再重新打開發現先前填的內容還在靠的就是 cookie。(不得超過 4096 Bytes)
實作原理，client 端的程式在一旦填寫的資料有變動時，就把該資訊寫入 cookie中。



## 請說明 session 的作用與使用情境
Session 負責紀錄在 web server 上的使用者訊息。Session 機制會在一個用戶完成身分認證後，存下所需的用戶資料，接著產生一組對應的 id，存入 cookie 後傳回用戶端。
通常是用來驗證身分或是Session 傳值，讓不同頁面之間可以互相傳遞資料。其原理通常是使用 Query String 或 POST body 等方法，把資料往 Server 傳之後，在 Server 端將 Client 上傳的資料存在 Session 之中。之後的連線或開啟其它頁面時，因為你拿的號碼牌是同一個，所以在不同的頁面之下，仍然可以讀到前一次所儲存在 Session 的狀態。

## 請說明 ajax 的作用與使用情境
ajax基本上一改過去web前端和後端採用的同步溝通方式，而是使用非同步來溝通。
例如想要在網頁上按下一個按鈕可以邊loading資料邊瀏覽網頁，不會卡住，藉此提升使用者體驗。


## 請說明什麼是 cache？請描述使用 cache 的優缺點
就我離解範圍是在header中使用Expires跟max-age等關鍵字，決定用戶端是否使用快取與使否過期。
優點:節省流量，也節省時間，或是更宏觀地來說，減少資源的損耗。
缺點: 似乎沒有當server更新時也強迫client端更新的機制，若設定不當可能會造成資訊錯誤。
# 資料處理
## 請描述 stack 及 queue

1. tack 是一種有序的串列，其插入與刪除都是在同一端進行，就是所謂LIFO資料結構，可用於DFS深度優搜尋。
2. queue 也是一種串列，只是插入與刪除是在兩個相對的端點進行，也就是FIFO的資料結構，可用於BFS廣度優先搜尋。

## 請說明資料庫正規化的目的與達成方式

- 一般來說，將資料分別存放在多個關聯表時，期平均的效率會比放在少數幾個關連表中來的差(不一定是絕對)，當正規劃越多代表關聯表切的越細，也就是使用者在查詢時joion會用得越多，join是一個很花時間的運算動作，當然正規化的好處就是，可以減少存進多餘的資料，以及更新異常的現象。
- 正規畫是實際需求需要做幾次通常做到第3次正規畫就足夠了，正規畫主要依據是"功能相依性"(functional dependency)來找出重複資料與候選鍵和主鍵進而達成正規畫。



## 請描述關連式資料庫中 Primary Key、Unique Key、Index Key 的差別

Primary Key，它一定是非null且unique，並且一個table只能有一個Primary Key。
Index Key 可多欄位設定為Index，可重複，可null
	Unique Key 與index差不多差別是不可重複。

請問下列 SQL 語法中，你認為哪些欄位需要建立 index？
SELECT * FROM `order` WHERE `email` = ‘aaa@example.com’ ORDER BY `type`, `createDate`
email type createDate 3個項目需要建立索引(如果都不是大量重複的直)。

## 若有兩個人同時操作一筆資料庫內訂票紀錄，一個人取消訂票、一個人更改時間，兩個人同時送出，請問這個情境可能會發生什麼問題？程式上應該如何處理？

這段敘述牽扯到資料庫異動ACID中的isolation，可能會發生Dirty Read ，在取消票券動作還沒完全commit時而另一人的動作剛好開始執行，讓第一人再讀一次時看到不同的資料，
引此Isolation 分成四個等級如下

![Imgur](https://i.imgur.com/2vgl1bs.png)

mysql預設等級通常是 repeatable read 較安全但moongodb(no-sql)預設是read uncommitted不太適合這種需要高精準度資料存取。
# 安全性
## 請說明 SQL injection 攻擊如何進行，程式上應該如何防禦？
Sql Injection 就是指 SQL 語法上的漏洞，藉由特殊字元，改變語法上的邏輯(簡單說就是駭客們的克漏字遊戲)，防範方式不外乎檢查或跳脫字元escape 或是  Prepared Statement等方式讓傳入的值暴政是數值參數不會被認為是查詢語句的一部分。

## 請說明 XSS 攻擊如何進行，程式上應該如何防禦？
就我經驗xss攻擊通常是在網頁中插入惡意的js代碼，使用黑名單過濾僅僅只能防一些君子，要達到真正安全只能犧牲使用者體驗使用白名單放視作過濾，就是該表格中只能出現何種字元等。

## 請說明 CSRF 攻擊如何進行，程式上應該如何防禦？
	
CSRF要能成立的必要條件是，使用者已登入網站，而最簡單的場景就是，使用者登入後，單憑瀏覽器與伺服端之間的會話溝通，就確認使用者的身分無誤而進行各種操作(可能是在其他網域)，因而使得有意攻擊者，只要能命令瀏覽器做出想要的請求。
防範方式不外乎檢查header中的Referer看看是否適合法網域，另外CSRF token是一個常用方式server 比對表單中的csrftoken與自己 session 裡面存的是不是一樣的，是的話就代表這的確是由使用者本人發出的 request。另外像是chrome也有提供防禦機制使，SameSite關鍵字家在cookie後面就好，就代表說「我這個 cookie 只允許 same site 使用，不應該在任何的 cross site request 被加上去」。