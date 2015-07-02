===================
先 Work Around 再說
===================

前情提要： `我們老師構想了一套 IoT 系統 <20150424-tree.rst>`_

這個 IoT 系統可以分成兩大部份，Client 和 Server，我負責的是 Client。

在老師的要求下，Server 開始有兩種，一種是原本的 Global 版本，是我們架設的，放在 Internet 上，有個 Public IP 可以連（才不會寫在這裡咧）；另一種是 Local 的，會灌在筆電上，透過 WiFi 和 Client 溝通。

大家應該很快可以發現一個小問題，Local 版的 Server 不會預先知道自己拿到什麼樣的 IP，所以要提供一個機制讓 Client 能找到 Server 才行。

我們的解法是在 Client 端那裡跑一支 UDP Server，聽在某個 Port；Server 則是固定週期發一個 UDP Broadcast 封包，Client 收到的話，看來源 IP 就知道 Server 在哪裡了。

反正都要偵測，我就把 Global 和 Local 的偵測寫在同一支 Client 裡：Client 開起來以後，會先去連 Global 的，同時開一支 UDP Server 起來等，如果運作到一半收到來自 Server 的封包，就對 Global 的 Server 斷線，改連 Local 的 Server。先叫它 Client1 吧，是一支 Java 程式。

OK，動工。

完成，測試。

（應該是在這之前）我寫了一支迷你 Local Server，行為上模仿 Global 的 Server，這樣我才能在自己的電腦上測試，寫完 Code 總要測試嘛。

做了幾種不同的測試

1.  直接開 Client1，讓它連 Global Server（連原本功能都爛掉的話就不用說了）
2.  先打開 Local Server，讓它開始 Broadcast，再開 Client1
3.  Client1 先開，送資料送到一半再開 Local Server

都 ok，完工。

Export 成 jar 檔，放進集中區（Client 有很多支），把載點寄給學長，完成。

----

向學長要了另一支 Client 的原始碼，叫它 Client2 好了，這次是 Python Script。也加上能夠偵測 Local Server 的功能。測試，收工。

然後學長寄了信來，說 Client2「怪怪的」，但這個先暫時放旁邊；Client1「連不上 Local Server」，要我「先把 IP 設成 127.0.0.1，編譯後給他一份」。

覺得火大，What The Fuck？我他媽寫了那麼久，做了完整的測試，因為「不會動」就要用這種方式先「生一個會動的」出來。

做個補充，這支程式是一支視窗程式，但它的視窗大小是不能用滑鼠拉動的，它的長寬寫在程式碼裡面。

前一陣子老師說「這視窗太大」，於是學長請我把它改小，我改了半天才弄好，因為程式碼裡面有一大堆莫名奇妙的常數是根據「那個大小」調的，直接改視窗大小的話整個程式的行為都會跑掉，幹。

對，Client1 就是那棵 `永生樹 <20150424-tree.rst>`_ ，預設大小 900 x 600，要我各改小一半，改成 450 x 300。裡面所有數字都不是按照比例寫的，螢幕上每條線的長度和位置都是寫死的，把視窗直接改小的話整棵樹就會衝出視窗了。

改小以後呢？原本大棵的那個也沒說可以丟掉，所以之後每次修改，我就得先「檢查長寬是不是 900 x 600，編譯一次，輸出成 jar 檔，把長寬改成 450 x 300，編譯一次，輸出成 jar 檔，檔名要加上 "small"。」

現在又要我弄個 IP 寫死 127.0.0.1 的，以後每改一次 Code 我就要編譯四次。Code 我在寫我在編，站著說話不腰疼，看人家吃麵沒在怕燙的啦。

----

我認為 **Work Around 堆起來的東西是垃圾** ，來看看什麼時候會出問題。

