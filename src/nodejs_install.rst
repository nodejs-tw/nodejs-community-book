********
安裝與設定
********

本篇將講解如何在各個不同OS建立NodeJS 環境，目前NodeJS 0.4.8版本環境架設方式需依賴Linux指令才可編譯完成，當然在不同作業系統中也已經有NodeJS package，可以直接使用指令快速架設。以下列表依據各不同作業系統解說如何架設NodeJS。

Linux
======

Linux 很適合作為 NodeJS 的伺服器作業系統及開發環境。安裝前，請先確認以下套件已正確安裝。

curl (wget) 用來下載檔案的工具
git 先進的版本控制工具
g++ GNU C++ 軟體編譯工具
make GNU 軟體專案建置工具
指令如下，如設有權限問題，請在指令前面加上sudo 
git clone --depth 1 https://github.com/joyent/node.git
cd node

如果有要切換到不同版本，輸入如下指令

nodeJS 版本參考頁面：https://github.com/joyent/node/tags
git checkout v0.x.x

開始編譯nodeJS，如果在make install 出現錯誤訊息，請使用sudo 權限
./configure
make -j2 # -j sets the number of jobs to run
make install

設定環境變數，將NODE_PATH加入到bash 檔案，後面的~/.profile 需要視自己實際狀況改變檔名
echo 'export NODE_PATH=/opt/node:/opt/node/lib/node_modules' >> ~/.profile
echo 'export PATH=$PATH:/opt/node/bin' >> ~/.profile

重新讀取bash
. ~/.profile

接著測試nodeJS 是否正常執行
node --version

出現版本訊息，表示安裝成功。

其他各家Linux有套件包可使用，請參考官方安裝說明


Mac OS X
=========

nodeJS 在nodeJS 在v0.6.x版本之後 ，Mac 環境可以直接使用pkg 安裝包，點擊兩下之後，即完成安裝。

下載node.pkg (由官方網站)

Windows（cygwin）
================

目前NodeJS 0.4.8版本安裝方式需要透過Linux指令才能完成，執行方式如下描述：

A. 執行Binary NodeJS
    1. 外部善心人士已將Cygwin與NodeJS打包，成免安裝版本，至此網址下載
    2. 下載後解壓縮至硬碟內，至command line即可執行。

B. 使用 cygwin 編譯 NodeJS

1. 下載 cygwin。
2. 執行Setup.exe，選擇以下幾個package.
Devel
gcc-g++ C++ compiler
gcc-mingw-g++
gcc4-g++ G++ subpackage
git
make
openssl-devel
pkg-config
zlib-devel
Python - install (全套件)
Web
wget
Devel
gcc-g++ C++ compiler
gcc-mingw-g++
gcc4-g++ G++ subpackage
git
make
openssl-devel
pkg-config
zlib-devel
Python - install (全套件)
Web
wget
TIP：git 和 wget 可只選一個安裝即可

修改此檔案 c:\cygwin\bin\rebaseall，搜尋：

TmpDir="${TMP:-${TEMP:-/tmp}}"

修改如下：

#TmpDir="${TMP:-${TEMP:-/tmp}}"
TmpDir="/tmp"

至command line執行指令如下：

c:\cygwin\bin\ash.exe rebaseall -v

最後一行結果為

/usr/bin/cygz.dll: new base = 69b90000, new size = 30000
rebaseall


使用 wget (v0.x.x表示版號，以官方網站為主)


$ wget http://nodejs.org/dist/node-v0.x.x.tar.gz
$ tar xvf node-v0.x.x.tar.gz

使用 git (v0.x.x表示版號，以官方網站為主)

$ git clone git://github.com/joyent/node.git
$ cd node
$ git fetch --all
$ git tag
$ git checkout v0.x.x

編譯

$ cd node
$ ./configure
$ make
$ make install


C. 使用 MinGW+MSYS 編譯 NodeJS

1. 下載MinGW

MinGW的官網在：
http://www.mingw.org/

在Windows環境中使用的話，建議下載他的自動安裝程式：
http://sourceforge.net/projects/mingw/files/Automated%20MinGW%20Installer/mingw-get-inst/

從目錄中挑一個適當的版本來安裝就可以了（通常是挑最新的）


2. 安裝MinGW

先執行下載來的安裝檔：


大部分選擇預設就可以。不過在Select Components的地方：


要編譯Node，至需要基本的msys系統以及C++編譯器，所以額外選擇：



點選Install開始安裝：


接下來安裝程式會從網路上抓取要安裝的package，請耐心等待：


安裝完畢後，即可從程式選單執行msys：


執行後，就可以進入bash環境：


接下視需求決定要不要先執行一下postinstall程序（不一定需要，除非要使用之前安裝過的其他MinGW環境）：


這樣，MinGW及MSYS環境就大致處理好了。


3. 下載並安裝python

python的網站在：
http://www.python.org/

在windows環境安裝，只要點選左側選單中的「Windows Installer」就可以下載msi安裝檔。安裝完後，記得打開cmd console，用「path」指令確定一下，python的安裝目錄是否在其中。msys中使用的其實是這個外部的python直譯器。


4. 設定openssl目錄

node與openssl-1.0.0似乎不搭，所以需要手動下載openssl-0.9.8。請到下列網址下載package：
http://sourceforge.net/projects/mingw/files/MSYS/openssl/openssl-0.9.8k-1/

需要下載的是這兩個：
libopenssl-0.9.8k-1-msys-1.0.11-dev.tar.lzma
libopenssl-0.9.8k-1-msys-1.0.11-dll-098.tar.lzma
在MSYS中，windows的C碟會掛載在/C目錄，而D碟會掛載在/D目錄，依此類推。假設上述兩個檔案下載後放在D:\Downloads目錄中，在MSYS中可以利用tar來安裝：


安裝過後，程式庫會安裝在/lib，標頭檔會安裝在/include/openssl...但是這樣node的編譯系統還無法辨識。

研究了一下wscript，會發現在node目錄上一層建立一個openssl目錄，然後把程式庫複製到這個目錄，把標頭檔複製到其下的include/openssl目錄，就可以順利執行./configure了。像這樣：


這個openssl目錄及檔案結構：




5. 下載node

可以直接透過nodejs.org上發布的網址下載，或是額外安裝msys-git後直接git clone（方法跟cygwin一樣）。只是解開後要編譯的node目錄，與openssl目錄的相對位置要如上所述。


6. 編譯

如果設定正確，那在node目錄中執行./configure之後看起來應該像這樣，接下來就可以執行make了：


編譯過程的畫面看起來像這樣：


編譯完成後，編譯過程中產生的檔案會放在build/default目錄中：


node.exe會複製一份到node目錄中：


想要驗證一下node.exe是否可以執行，可以試跑一下make test，不過現階段大部分測試在windows環境中都會fail：


不過這樣的結果已經比前幾版好了。


7. 在windows console中執行

從nodejs.org上下載的v0.5.x可執行檔，額外靜態編譯了所有需要的程式庫到執行檔中，可以不依賴任何dll就能執行。但是自己在MinGW下編譯出來的node.exe，還是需要額外的dll檔才能在MSYS環境外執行。以node-v0.5.2為例，需要的dll檔有幾個（不同版本需要的dll可能會有不同，需要的檔案大概都是在/bin或是/mingw/bin目錄中）：
msys-1.0.dll
msys-crypto-0.9.8.dll
msys-ssl-0.9.8.dll
在MSYS中複製過來後，從windows的cmd console進來看看（假設MinGW裝在C:\MinGW，使用者的家目錄會在C:\MinGW\msys\1.0\home\使用者帳號）：


接下來，只要執行

node javascript檔案

就可以跑了。不過如果要當作伺服器，開啟port來監聽的話，需要有系統管理員權限。所以要先用「系統管理員權限」來執行「命令提示字元」，然後才能在console中用node.exe執行伺服器程式。

Windows（native）
================

nodeJS 在v0.6.0版本之後開始正式支援windows native，直接使用node.exe 就可以執行程式，支援性完全與linux 相同，更棒的部份就是不需經過編譯，經過下載之後，簡單設定完成，立即開發node 程式。

下載node.msi (由官方網站)

點擊兩下開始安裝

如此完成windows native node.exe 安裝，接著可以進入command line 執行測試。

在command line 輸入"node"，會出現如下的畫面，表示安裝完成
