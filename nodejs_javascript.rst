
********************
JavaScript 與 NodeJS
********************

其實使用Javascript在網頁端與伺服器端的差距並不大，但是為了使NodeJS可以發揮他最強大的能力，有一些知識還是必要的，所以還是針對這些主題介紹一下。其中event loop、scope以及callback其實是比較需要了解的基本知識，cps、currying、flow control是更進階的技巧與應用。


Event Loop
==========

可能很多人在寫Javascript時，並不知道他是怎麼被執行的。這個時候可以參考一下jQuery作者John Resig一篇好文章，介紹事件及timer怎麼在瀏覽器中執行：How JavaScript Timers Work。通常在網頁中，所有的Javascript執行完畢後（這部份全部都在global scope跑，除非執行函數），接下來就是如John Resig解釋的這樣，所有的事件處理函數，以及timer執行的函數，會排在一個queue結構中，利用一個無窮迴圈，不斷從queue中取出函數來執行。這個就是event loop。

（除了John Resig的那篇文章，Nicholas C. Zakas的 "Professional Javascript for Web Developer 2nd edition" 有一個試閱本：http://yuiblog.com/assets/pdf/zakas-projs-2ed-ch18.pdf，598頁剛好也有簡短的說明）

所以在Javascript中，雖然有非同步，但是他並不是使用執行緒。所有的事件或是非同步執行的函數，都是在同一個執行緒中，利用event loop的方式在執行。至於一些比較慢的動作例如I/O、網頁render, reflow等，實際動作會在其他執行緒跑，等到有結果時才利用事件來觸發處理函數來處理。這樣的模型有幾個好處：
沒有執行緒的額外成本，所以反應速度很快
不會有任何程式同時用到同一個變數，不必考慮lock，也不會產生dead lock
所以程式撰寫很簡單
但是也有一些潛在問題：
任一個函數執行時間較長，都會讓其他函數更慢執行（因為一個跑完才會跑另一個）
在多核心硬體普遍的現在，無法用單一的應用程式instance發揮所有的硬體能力
用NodeJS撰寫伺服器程式，碰到的也是一樣的狀況。要讓系統發揮event loop的效能，就要盡量利用事件的方式來組織程式架構。另外，對於一些有可能較為耗時的操作，可以考慮使用 process.nextTick 函數來讓他以非同步的方式執行，避免在同一個函數中執行太久，擋住所有函數的執行。

如果想要測試event loop怎樣在「瀏覽器」中運行，可以在函數中呼叫alert()，這樣會讓所有Javascript的執行停下來，尤其會干擾所有使用timer的函數執行。有一個簡單的例子，這是一個會依照設定的時間間隔嚴格執行動作的動畫，如果時間過了就會跳過要執行的動作。點按圖片以後，人物會快速旋轉，但是在旋轉執行完畢前按下「delay」按鈕，讓alert訊息等久一點，接下來的動畫就完全不會出現了。

Scope 與 Closure
================

要快速理解 JavaScript 的 Scope（變數作用範圍）原理，只要記住他是Lexical Scope就差不多了。簡單地說，變數作用範圍是依照程式定義時（或者叫做程式文本？）的上下文決定，而不是執行時的上下文決定。

為了維護程式執行時所依賴的變數，即使執行時程式運行在原本的scope之外，他的變數作用範圍仍然維持不變。這時程式依賴的自由變數（定義時不是local的，而是在上一層scope定義的變數）一樣可以使用，就好像被關閉起來，所以叫做Closure。用程式看比較好懂：

.. code-block:: js

	function outter(arg1) {
		//arg1及free_variable1對inner函數來說，都是自由變數
		var free_variable1 = 3;
		return function inner(arg2) {
			var local_variable1 =2;//arg2及local_variable1對inner函數來說，都是本地變數
			return arg1 + arg2 + free_variable + local_variable1;
		};
	}

var a = outter(1);//變數a 就是outter函數執行後返回的inner函數
var b = a(4);//執行inner函數，執行時上下文已經在outter函數之外，但是仍然能正常執行，而且可以使用定義在outter函數裡面的arg1及free_variable1變數
console.log(b);//結果10

在Javascript中，scope最主要的單位是函數（另外有global及eval），所以有可能製造出closure的狀況，通常在形式上都是有巢狀的函數定義，而且內側的函數使用到定義在外側函數裡面的變數。

Closure有可能會造成記憶體洩漏，主要是因為被參考的變數無法被垃圾收集機制處理，造成佔用的資源無法釋放，所以使用上必須考慮清楚，不要造成意外的記憶體洩漏。（在上面的例子中，如果a一直未執行，使用到的記憶體就不會被釋放）

跟透過函數的參數把變數傳給函數比較起來，Javascript Engine會比較難對Closure進行最佳化。如果有效能上的考量，這一點也需要注意。
