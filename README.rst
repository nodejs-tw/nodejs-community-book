NodeJS Taiwan 開源電子書計畫
=============================

這份電子書是由 NodeJS Taiwan 開發社群共同製作

我們的 GitHub 網址是：
https://github.com/nodejs-tw/nodejs-from-scratch

您可以利用 Google Doc Viewer 預覽本電子書最新版：
http://goo.gl/Y7nSh

使用 ContPub 服務打包：
http://contpub.org/

如何加入 NodeJS Taiwan 開源書寫計畫？
--------------------------------------

1. 請先申請一組 GitHub 帳號
2. 請瀏覽本專案於 GitHub 的網頁
   https://github.com/nodejs-tw/nodejs-from-scratch
3. 您的系統必須裝有 Git 軟體
4. 本專案的 Repo 位址是
   git@github.com:nodejs-tw/nodejs-from-scratch.git

如何使用 reStructuredText 格式排版文字內容？
---------------------------------------------

本書採用 Sphinx 擴充的 reStructuredText 格式撰寫。

http://sphinx.pocoo.org/rest.html

如果您有興趣加入內容寫作小組，只需要參考以下的語法說明。

本書的架構以「章」為單位切割檔案，
副檔名一律採用 .rst 結尾。
例如 nodejs_intro.rst 、 nodejs_hello.rst 分別是兩個不同 Chapter，
在 index.rst 主文件中，
會依次序連結到這些檔案（但定義時不含副檔名）。

每一章的 .rst 檔案會有以下的文件結構： ::

	這是大標題（章）
	===============
	
	這是小標題（節）
	----------------
	
	這是更小標題（子節）
	^^^^^^^^^^^^^^^^^^^^

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

