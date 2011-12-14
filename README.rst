.. raw:: latex

   \setcounter{secnumdepth}{-1}

**************
如何取得本書？
**************

《NodeJS 中文開發指南》
是「開放原始碼電子書」，
內容由 NodeJS Taiwan 社群多位作者共同撰寫。

本書採用線上持續出版方式發行，
您可以在以下網址獲取本書的最新版本：

http://contpub.org/read/NodeJSFromScratch

參與電子書計畫
==============

請加入 NodeJS Taiwan 的 Facebook 專頁，
並留言與社群成員取得聯繫。

GitHub 專案網址是：
https://github.com/nodejs-tw/nodejs-from-scratch

當您成為共筆作者，
可以使用 Git 版本控制系統參與協作。

授權方式
========

所有電子書內容提交 GitHub nodejs-tw 彙整後，
即同意其內容為 NodeJS Taiwan 開發社群共有，
所有共同作者願意無條件免費公開、分享，
並接受持續修改、再製與發佈。

無論您以任何方法取得本書內容，
請依以下 **創用CC授權條款** 複製、散布或修改著作。

**姓名標示─非商業性─相同方式分享**

本授權條款允許使用者重製、散布、傳輸以及修改著作，但不得為商業目的之使用。若使用者修改該著作時，僅得依本授權條款或與本授權條款類似者來散布該衍生作品。使用時必須按照著作人指定的方式表彰其姓名。

取得本書原始碼
==============

您可以使用 git 指令，取得完整電子書原始碼。 ::

	git clone git://github.com/nodejs-tw/nodejs-from-scratch.git

您也可以下載 ZIP 壓縮檔。

* https://github.com/nodejs-tw/nodejs-from-scratch/zipball/master

編輯慣例
========

專有名詞英文大小寫，盡可能與官方用法相同：

* NodeJS
* JavaScript

中文段落中，標點符號使用全形。

* （）「」
* ，、；。

段落中英文與中文文字之間，使用一個空白字元隔開（遇標點符號則不必）。

* 中文遇到 English 以空白隔開
* 中文標點符號遇到（English）不必以空白隔開

撰寫電子書原始碼
================

本書採用 reStructuredText 文字格式撰寫。

http://sphinx.pocoo.org/rest.html

您只需要認識幾個基本標記語法，
就可以開始參與協作。

本書的架構以「章」為單位切割檔案，
副檔名一律採用 .rst 結尾。
例如 nodejs_intro.rst 、 nodejs_hello.rst 分別是兩個不同 Chapter，
在 index.rst 主文件中，
會依次序連結到這些檔案（但定義時不含副檔名）。

每一章的 .rst 檔案會有以下的文件結構： ::

	***************
	這是大標題（章）
	***************
	
	這是小標題（節）
	===============
	
	這是更小標題（子節）
	-------------------

內文的部份，為了方便編輯，可以在在合適的文字長度之後換行，
連續換行兩次則會建立新的段落。 ::

	這是第一段落，
	第二行還是同一個段落；
	第三行也是。
	
	隔一個空行，
	就會產生一個新的段落，
	到這裡還是第二個段落。

如果要顯示一行或多行指令，例如 Shell 命令，則使用兩個冒號，
隔一行之後再以 Tab 起始。 ::

	執行一個 NodeJS 程式檔。 ::
	
		node example.js

請注意兩個冒號前面若有其它文字，必須插入「空白」隔開。

項目符號，使用 * 星字符號起始，編號採用數字加半型小數點。 ::

	這是項目符號：

	* 第一項
	* 第二項
	* 第三項

	這是編號：

	1. 第一項
	2. 第二項
	3. 第三項

使用項目符號及編號，請與上下段落保持一個空行。

如果要顯示程式碼，有兩種寫法。

第一種，直接寫在文件裡面（適合片段、部分節錄）： ::

	.. code-block:: javascript

		function say_hello(who) {
			return 'Hello, ' + who + '!';
		}

第二種，寫在外部程式碼檔案（適合大型、可執行程式）： ::

	.. literalinclude:: src/example.py
	   :language: javascript

為了方便測試程式碼，
如果是可被執行的完整程式，
請放在 src 資料夾下，
再使用第二種方法嵌入文件中。

.. raw:: latex

   \setcounter{secnumdepth}{1}

