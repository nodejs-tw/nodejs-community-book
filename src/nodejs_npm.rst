******************************
套件管理（Node Package Manager）
******************************

npm 全名為node package manage，此為node module 管理包，藉由安裝npm 之後可以輕鬆使用npm install xxx 的方式安裝任意模組，安裝模式類似於gem, apt-get 方式，如此管理module 就會更加輕鬆，同時也可以查看目前module 是否為最新版本，進行module 更新。

nodeJS v0.6.3之後版本開始內建npm ，已經安裝v0.6.3版本的使用者，可以不用再執行底下步驟，可以直接使用npm 安裝、移除相關module。當然有興趣自己手動安裝npm 可以查看底下文章說明。

安裝方式分別介紹linux, windows 安裝方式

Linux 安裝
==========

安裝npm 之前必須安裝 curl，同時確認node 已經安裝完成，環境變數也設定完成，node 版本需為 v0.4.x 以上，底下為安裝指令。 ::

	curl http://npmjs.org/install.sh | sh

接著輸入指令測試 ::

	npm --v

Windows 安裝
============

本篇介紹如何使用node.exe (windows native)安裝npm ，node.exe 版本為v 0.6.1 ，這個版本之後已經變成安裝包，安裝完成後會自動將環境變數(environment path)設定完成，意謂安裝完成node windows 版本之後，就不需要做任何設定，進入command line  之後，立即安裝npm，輸入指令如下。 ::

	git config --system http.sslcainfo /bin/curl-ca-bundle.crt
	git clone --recursive git://github.com/isaacs/npm.git
	cd npm
	node cli.js install npm -gf

PS. 目前版本只能支援手動設定環境變數，將node.exe 換到"c:\node\"路徑底下，才能順利安裝npm。

NPM 指令說明
===========