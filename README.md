# sublime-imfix
在 Linux 版的 Sublime Text 3 中，使用 gcin 輸入中文

在 Linux 下使用 Sublime Text 3，要支援中文輸入，需使用 fcitx 輸入法，但是我不習慣它的拆字界面，覺得使用 gcin 比較順手。
很幸運的是，在網路上，有網友的討論提出解決方式。參考連結如下。

http://www.sublimetext.com/forum/viewtopic.php?f=3&t=7006&start=10#p41343
http://www.sublimetext.com/forum/viewtopic.php?f=3&t=7006&start=20#p61143 \
(以上為 Sublime Text forum) \
http://whitequark.org/blog/2014/04/14/xcompose-support-in-sublime-text/ 

我自己使用的是 Gentoo Linux，也對 C 語言不熟，此處的程式，是從網路上找到的，經測試可以使用。

編譯: \
$ gcc -shared -o libsublime-imfix.so sublime-imfix.c  ``` `pkg-config --libs --cflags gtk+-2.0` ``` -fPIC

設定環境變數: \
$ export GTK_IM_MODULE=xim

執行: \
$ LD_PRELOAD=./libsublime-imfix.so subl3

如上，Sublime Text 3 中文切換，必需將 GTK_IM_MODULE 設成 xim
但是會讓所有的程式，gcin 的輸入視窗都黏在視窗左上角，不會跟著程式的游標 。
只好要用 Sublime Text 時，才設成 xim。終究能夠直接輸入中文，比起以往必需用 copy and paste 來輸入中文，要好得多了。

另外，有下面一些小小的不便。
在輸入中文時，若想用 Backspace 來修正時，無法刪除輸入的字根，反而會刪除編輯的內容。必須按 Escape 鍵，取消所有的輸入，重新輸一次。
無法用 ctrl+, 或 ctrl+. 來輸入中文的豆號和句號。

修改 sublime-text-3.desktop 中的執行指令 \
Exec=bash -c 'GTK_IM_MODULE=xim LD_PRELOAD=/usr/local/lib/libsublime-imfix.so subl3' %F

關於中文輸入法的環境變數的設定，可以參考 \
http://moto.debian.tw/viewtopic.php?t=9525
