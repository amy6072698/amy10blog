---
title: 從零開始學 Hexo (8) | landscape 主題如何客製 Hexo 首頁
date: 2025-04-28 21:15:00
categories:
  - Hexo
tags: 
  - Hexo
  - 前端
description: 介紹如何在 landscape 主題，客製化 Hexo 的網站樣式
---

## 激發你的客製魂

經過前面的努力我們終於把 Hexo 網站部署到 GitHub Pages 了，但是這樣用主題模板套用的固定結構、樣式的網站，滿意嗎？

沒錯！我們不滿意！這篇文章就是來激發你的客製魂的，接下來就開始介紹如何用預設主題 landscape 來客製化你的 Hexo 網站吧 ~

## EJS 樣版語言

開始客製化之前需要先認識一下 EJS 這個樣版語言，這邊會簡單先講解它的作用，如果想深入了解語法可以到 [EJS 官網文件](https://ejs.bootcss.com/#docs)查看官方說明

仔細觀察你應該會發現你寫的每篇文章頁面，網頁的結構跟樣式都很相似，唯一不同的是文章內容

前面提過只要在 `source/_posts` 資料夾的 md 檔內寫入文章內容，文章內容就會更新到該文章的頁面上，不需要每篇文章都新增一個不同的 HTML 檔...

而 landscape 主題就是使用 EJS，做到把網站中重複部分拆分成不同 EJS 檔，再將每個部分的結構和不同資料內容，整合到一個 `layout.ejs` 的檔案中

簡單來說 EJS 樣版語言，可以做到把網頁結構跟資料組合成一個個看起來結構很像，但顯示資料卻不同的網頁 ( 像每篇文章頁面一樣 )

比較以下 Hexo 的文章頁面，網頁的結構、樣式都一樣，只有文章內容不同

![ Hexo 文章頁面 1](https://ithelp.ithome.com.tw/upload/images/20250519/20172694DXCgVkXtw9.png)

![ Hexo 文章頁面 2](https://ithelp.ithome.com.tw/upload/images/20250519/20172694eiZK7BnfZg.png)

## layout.ejs 檔案

前有提到網站的結構跟資料會整合到一個 `layout.ejs` 的檔案中，那接下來就看看這個檔案，試著調整看看會對網頁產生什麼改變吧 ~

首先點開 themes 底下的 landscape 資料夾，在點開裡面的 layout 資料夾，就會看見 `layout.ejs` 的檔案，點開它你會發現檔案的內容很像 HTML，但是又混合一些用 `<%- %>` 包住的程式碼

`<%- %>` 內可以寫入 JavaScript 控制網站結構，也可以匯入其他檔案的內容到 `layout.ejs` 檔中，匯入的結構或資料會放在 `<%- %>` 程式碼所在的位置

![ layout.ejs 檔案](https://ithelp.ithome.com.tw/upload/images/20250519/20172694OgBZpWQr1B.png)

先看 `<%- partial('_partial/head') %>` 這個片段，在這行程式碼的位置引入了網站的 head，被引入的是在 `_partial` 資料夾內的 `head.ejs` 中的內容

點開檔案可以看到確實有 `<head>` 標籤和 head 裡面會有的內容

![ head.ejs 檔案](https://ithelp.ithome.com.tw/upload/images/20250519/20172694Km4xhLRGIs.png)

---

### 不確定引入的是不是這個檔案怎麼辦？

雖然現在知道怎麼找被引入檔案的位置，但如果不確定到底引入的是不是這個檔案，要怎麼辦？

這時候可以試著修改那個檔案的內容，觀察網站結構是否改變，現在模擬一下情境：

假設我想加入文字到網站的 footer 位置，這時候我開啟 Hexo 伺服器，點開本地端的網站連結，打開 Chrome 的開發者工具，查看 Elements 的 HTML 結構，發現 footer 的區塊被包在 `<div id="wrap">` 的最後面

![ Elements 開發者工具 footer 位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694nx5IU5RqRU.png)

這時候我回到 `layout.ejs` 檔，尋找 footer 區塊的對應位置，發現它可能在第 14 行

![ layout.ejs 第 14 行](https://ithelp.ithome.com.tw/upload/images/20250519/20172694ZHtEhaq0fP.png)

第 14 行程式碼有看到 `partial('_partial/footer'` 這樣的內容，所以我覺得被引入的是 `_partial` 資料夾內的 `footer.ejs` 檔，但我不太確定，就先在這個檔案內嘗試加入一行字

![ footer.ejs 修改](https://ithelp.ithome.com.tw/upload/images/20250519/20172694Q2p0SzBz5J.png)

加入文字後儲存再重新整理網站，footer 確實有加入我剛剛輸入的文字內容，所以被引入的檔案就是 `footer.ejs` 

![重新整理網站 footer 結果](https://ithelp.ithome.com.tw/upload/images/20250519/20172694ZORy0QJsgM.png)

經過上面示範的模擬情境，應該就比較知道要如何找到你要客製化的部分在哪，以及不確定時要怎麼驗證了，來嘗試找找想客製的部分在哪個檔案中吧 ~

## 怎麼客製化滿版頁面

如果去看 Hexo 網站的每個頁面，你會發現右側都有一個側欄選單，如果想讓關於或是首頁變成沒有側欄選單的滿版頁面，要怎麼做呢？

還記得前面有提到，如何用文章 md 檔的開頭調整文章細節嗎？接下來就可以運用這個方法，讓你可以控制頁面是否要滿版顯示

假設我希望關於頁面可以滿版顯示，先打開 `source/about` 下的 `index.md` 檔，在開頭加入自訂的內容：`fullPage: true`

![關於頁面 md 檔的開頭設定](https://ithelp.ithome.com.tw/upload/images/20250519/20172694z6jKtvV9P7.png)

看到小駝峰的命名方式應該可以預感到，沒錯... 接下來就是 JavaScript 登場的時候的，接下來會寫入一些 JavaScript 的內容到 `layout.ejs` 中

但首先，要先找到我們想去除的側欄選單在檔案中的哪個位置，這時候就是依照前面的步驟，先在 Chrome 的開發者工具的 Elements 內，找到側欄選單的 HTML 結構位置

你會發現它在 `<div class="outer">` 內

![ Elements 側欄選單位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694PTPAevByKF.png)

然後就是找到 `layout.ejs` 檔案中對應的位置：第 10 ~ 12 行

![ layout.ejs 第 10 ~ 12 行](https://ithelp.ithome.com.tw/upload/images/20250519/20172694rBGpjpG9F4.png)

再來就是在第 10 行 `if (` 後面寫入 JavaScript 判斷，修改後程式碼如下，這樣當 fullPage 是 ture 就不會顯示側欄選單

```ejs!
<% if (!page.fullPage && theme.sidebar && theme.sidebar !== 'bottom'){ %>
```

加入後儲存再查看關於頁面右邊的側欄消失了

![關於頁面側欄消失](https://ithelp.ithome.com.tw/upload/images/20250519/201726947eXhg3Soh5.png)

---

### 滿版 CSS 樣式調整

接下來你會發現側欄是消失了，但是左邊區塊怎麼沒有滿版向右邊延伸？

那就要靠 CSS 的力量來調整了，但是如果直接改控制排版的 CSS 屬性，可能會連其他頁面版面都一起被調整，所以這時候就需要透過新增一個 class，來增加 CSS 權重用覆蓋方式，蓋掉原本 landscape 預設的樣式

先用開發者工具找到是誰在控制頁面排版，這邊可以看到控制頁面排版的 CSS 屬性設定是 `float: left;`，選擇器是用 `#main`

![控制頁面排版的 CSS 屬性](https://ithelp.ithome.com.tw/upload/images/20250519/20172694waRqhgWjVu.png)

接下來回到 `layout.ejs` 檔案，找到 container 然後加入 class 屬性，class 屬性值寫入 JS 判斷讓 fullPage 為 true 時，再加入 fullPage 這個值

```ejs!
<div id="container" <%- page.fullPage ? 'class="fullPage"' : '' %>>
```

回到網站查看會發現只有關於頁面，可以看見 container 多了 fullPage 這個 class，其他頁面則沒有

![關於頁面多了 fullPage 這個 class](https://ithelp.ithome.com.tw/upload/images/20250519/201726949jDMJAUVze.png)

再來就是調整 CSS 啦 ~ 因為還沒講到 CSS 檔案怎麼客製化調整，所以這邊先在 `layout.ejs` 的 `</body>` 結尾標籤前，用 `<style>` 標籤直接寫入 CSS 樣式

這邊選擇器 `.fullPage #main` 權重較大，可以覆蓋原本的 CSS 預設樣式，除了把 float 改為 none 之外，也順便把 width 改成 100% ~~滿版樣式滿起來~~

![寫入滿版樣式](https://ithelp.ithome.com.tw/upload/images/20250519/20172694pC5A3B2pvV.png)

回去查看關於頁面，就可以看見滿版頁面樣式囉 ~

![關於頁面呈現滿版](https://ithelp.ithome.com.tw/upload/images/20250519/20172694a5YcZghaAy.png)

## 客製你的 Hexo 網站首頁

知道如何客製滿版頁面之後，接下來可能就會想動動網站的門面「首頁」，對 ~ 接下來就來看看怎麼讓首頁不要顯示成部落格文章列表，改成自己客製化的網頁結構囉 ~

假如我想客製化首頁，但是又想保留現在首頁的結構樣式，把它移到落落格的頁面，要怎麼做呢？

首先，先修改目前首頁的路由網址，進到全站的 config 檔，找到 `index_generator` 片段，把 `path` 這項改成 `'/blog'`

![全站 config 首頁路由設定](https://ithelp.ithome.com.tw/upload/images/20250519/20172694qM3imLmALb.png)

再來就是設定導覽列的網址，和前面文章提過的修改方式差不多，一樣到主題的 config 檔的 menu 設定，這邊把網址路由 `/archives` 改成 `/blog`

![修改主題的 config 檔部落格路由](https://ithelp.ithome.com.tw/upload/images/20250519/20172694NE39Iecdrj.png)

然後執行 `hexo clean` 指令清除目前的編譯檔後，重新開啟 Hexo 伺服器，點擊上方導覽列的部落格項目，進入後就會看到原本的首頁出現了

![首頁移動到部落格頁面](https://ithelp.ithome.com.tw/upload/images/20250519/20172694gSa0W73xpA.png)

接下來就是放首頁 HTML 檔的時候啦 ~ 到 source 資料夾內新增一個 `index.html` 檔案，在檔案開頭加入 title 和 fullPage 的設定，然後加入首頁的 HTML 結構

![新增首頁的 HTML 檔](https://ithelp.ithome.com.tw/upload/images/20250519/201726940DfKVED972.png)

回到網站進入首頁，剛剛寫的文字就出現在首頁囉 ~

![首頁呈現結果](https://ithelp.ithome.com.tw/upload/images/20250519/20172694KbGlNYdlh1.png)

## CSS 樣式怎麼客製調整

修改好首頁之後，你可能會想要再多客製一些網站的樣式，那就需要修改主題的 CSS 樣式了

進到 `themes/landscape/source` 路徑下，會看見一個 `css` 資料夾，裡面有一個 `style.styl` 檔，打開會看到內容很像 Sass 的寫法，styl 檔其實是一個叫 [Stylus](https://stylus-lang.com/) 的 CSS 預處理器，作用跟 Sass 很類似

如果有學過 Sass，可以試著自己修改裡面的樣式，在客製化時如果擔心直接修改，之後需要更新版本會有影響，可以註解原本的預設設定的內容，方便日後對照修改前後的內容

另外也可以使用 CSS 的方式客製樣式，前篇常見的 Hexo 指令有提到執行 `hexo generate` 指令，會產生 public 資料夾，裡面是編譯後的網站內容

沒錯，接下來就是執行 `hexo generate` 指令，然後進去 public 找到 `css` 資料夾 ，你會看見有一個 `style.css` 檔案

![ public 裡的 style.css 檔案](https://ithelp.ithome.com.tw/upload/images/20250519/201726948grKGiJp26.png)

這個檔案裡是目前網站套用的 CSS 樣式，把它複製到剛剛 `themes/landscape/source` 路徑下的 `css` 資料夾內

![複製 style.css 檔案](https://ithelp.ithome.com.tw/upload/images/20250519/20172694m0QsAcNj1e.png)

然後打開 `style.styl` 檔，在最底下加入 `@import "style.css"` 這行程式碼，引入剛剛複製的 `style.css` 檔覆蓋原本的樣式

![引入複製的 style.css 檔](https://ithelp.ithome.com.tw/upload/images/20250519/20172694YtDDZwf1nN.png)

接下來就可以在剛剛複製的這個檔案中，客製化自己的網站樣式啦 ~

### 修改導覽列項目文字顏色

假設我想修改網站上方導覽列項目的文字顏色，要怎麼做呢？

首先，一樣利用開發者工具，查看控制導覽列項目文字顏色的 CSS 屬性在哪，這邊可以發現是 `.nav-icon, .main-nav-link` 這個選擇器內的 color 屬性在控制

![開發者工具畫面](https://ithelp.ithome.com.tw/upload/images/20250519/201726942vuNBWi5jl.png)

看上圖黃框處，可以知道這行程式碼在 `style.css` 檔內大約 381 行的位置，接下來就來修改 color 屬性，我要改成 pink ~~粉粉der~~

![修改導覽列 color 屬性](https://ithelp.ithome.com.tw/upload/images/20250519/20172694JflYnd5dLB.png)

再來先執行 `hexo clean` 清除舊的編譯內容，然後再開啟 Hexo 伺服器，就可以看見上方導覽列文字 pink 起來啦 ~

![上方導覽列文字顏色改為 pink ](https://ithelp.ithome.com.tw/upload/images/20250519/20172694VT5xzoXsGo.png)

接下來就可以利用以上方法，自由的在 `style.css` 檔中客製化自己的網站樣式囉 ~

## 結語

這篇文章介紹了如何在 landscape 主題中，客製化 Hexo 的網站樣式，這些客製方法是學習加上實作後得來的，也鼓勵大家實作遇到問題，可以多查看官方文件，或是尋找大神寫過的技術文章，來解決目前遇到的難題

不同 Hexo 主題在客製化上可能要修改的地方會不同，但如果可以跟上這篇的操作，就可以期許自己去研究如何客製化你更喜歡的 Hexo 主題，不用侷限在 landscape 主題

下篇文章會帶大家學了解如何挑選及更換主題，那我們就下篇文章見囉 ~
