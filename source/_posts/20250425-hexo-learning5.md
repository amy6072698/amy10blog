---
title: 從零開始學 Hexo (5) | Hexo 文章細節調整與如何新增頁面
date: 2025-04-25 17:25:32
categories:
  - Hexo
tags: 
  - Hexo
  - 前端
description: 介紹如何調整 Hexo 文章細節，如何用指令新增部落格頁面
---

## Hexo 文章細節調整

前面有介紹如何新增文章的 Hexo 指令及 Mackdown 語法，其中還有一些細節想和大家說明，Hexo 的文章除了可以 Mackdown 語法編輯文字外，還有一個部份在每個文章檔案的開頭：

![ Hexo 文章寫入相關資訊的部分](https://ithelp.ithome.com.tw/upload/images/20250519/20172694c1DAp1d443.png)

沒錯，就是這塊區域，它可以寫入這篇文章的 title、tags 等與文章相關的資訊，接下來就看看這些資訊如何寫入，以及在部落格頁面上會如何呈現囉 ~

### title

顧名思義就是你文章的主要標題，現在修改後儲存，再開啟 Hexo 伺服器

![修改 title 程式碼](https://ithelp.ithome.com.tw/upload/images/20250519/201726941dJ7wiesl8.png)

修改後右側的 Recent Posts 區塊，會呈現你修改後的 title 名稱

![首頁的 Recent Posts 區塊](https://ithelp.ithome.com.tw/upload/images/20250519/201726949yJ0iZRZOq.png)

進入這篇文章的頁面，你會看到修改後的 title 名稱就是這篇文章最上方的大標題

![文章最上方大標題](https://ithelp.ithome.com.tw/upload/images/20250519/20172694yfP97tJigv.png)

### tags

標籤，它是你文章的關聯標籤，假如你的文章內容跟前端技術、Hexo 有關，你就可以在 tags 加上前端和 Hexo 兩個標籤，寫法如下：

![ tags 寫法](https://ithelp.ithome.com.tw/upload/images/20250519/20172694AXTrusbfL0.png)

儲存後重整網頁，文章的最下方就會出現剛剛修改的 tags 內容

![文章最下方出現修改的 tags 內容](https://ithelp.ithome.com.tw/upload/images/20250519/20172694W7DP0SivQF.png)

然後你會發現右側出現兩個區塊：Tags 和 Tag Cloud，裡面有剛剛新增的標籤內容

![ Tags 和 Tag Cloud 區塊](https://ithelp.ithome.com.tw/upload/images/20250519/20172694YOIhd2CJ5J.png)

等等！怎麼有兩個跟 tags 有關的區塊？別急，我來解釋，Tag Cloud 這個區塊內的標籤字體會隨相關文章變多而變大

實際示範，如果我又新增了一篇文章，這次 tags 的內容我輸入： `Hexo` 和 `待辦`，這時候跟 Hexo 標籤相關的文章就有兩篇，比 前端 和 待辦 兩個標籤的文章還多，再看看 Tag Cloud ：

![ Tag Cloud 區塊的標籤會隨文章變多而變大](https://ithelp.ithome.com.tw/upload/images/20250519/20172694hh4QO9AHRD.png)

Tag Cloud 區塊的 Hexo 標籤字體變大了，而反觀 Tags 區塊只有條列新增一個 待辦 標籤：

![ Tags 區塊](https://ithelp.ithome.com.tw/upload/images/20250519/20172694d7UlmWMko4.png)

你以為只有這樣嗎？oh, no no no ！點擊這兩個區塊內任一標籤連結，可以到與該標籤相關的所有文章清單頁面，點擊 Hexo 標籤就會看到有兩篇相關文章：

![點擊 Hexo 標籤有兩篇相關文章](https://ithelp.ithome.com.tw/upload/images/20250519/201726946y61ArwM9O.png)

### 如何縮短 Hexo 首頁文章長度

這個是額外的小補充，也稍微跟文章有關係就放進來講，經過一系列調整你應該有發現首頁左側會顯示你寫的所有文章，很貼心...但是顯示太多了！

別擔心，你只需要在文章中想截斷的地方，加入 `<!--more-->` 這行程式碼

![在文章想截斷的地方加入程式碼](https://ithelp.ithome.com.tw/upload/images/20250519/20172694BpC6txGrld.png)

噹噹 ~ 神奇的 Read More 按鈕就會出現在首頁左側的區塊的文章卡片中，而且文章卡片內只會顯示 `<!--more-->` 之前的內文

![ Read More 按鈕出現在首頁文章區塊](https://ithelp.ithome.com.tw/upload/images/20250519/20172694i9jxhhvCBh.png)

這樣首頁就簡潔許多囉 ~

## 如何新增 Hexo 頁面

學到這邊你也許會想我知道怎麼新增文章，但是我想做的不只是寫文章，我想向大家介紹自己或介紹部落格，但是沒有關於頁面可以給我放這些內容怎麼辦？

別擔心 ~ Hexo 也想到了，你可以用簡單的 Hexo 指令新增頁面，接下來就來看看如何新增並調整 Hexo 網站的頁面吧 ~

一樣開啟終端機，確認是否在 Hexo 部落格資料夾的路徑上，再執行以下指令

```bash
hexo new page about
```

執行完之後，你就會看到 source 資料夾中多了一個 about 資料夾

![ about 資料夾位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694p1JzqaPDj5.png)

資料夾中有一個 index.md 的檔案，你可以在裡面輸入關於頁面的內容，完成後開啟伺服器你會發現首頁上方沒有地方進去 QAQ ，別急 ~ 這部分之後會說，先在網只後面輸入 `/about` ，就會看到你新增的 about 頁面囉 ~

![ about 頁面](https://ithelp.ithome.com.tw/upload/images/20250519/20172694l9YpIiiidx.png)

## 如何在網站上方導覽列新增頁面連結

確定可以看見你更新的 about 頁面內容後，接下來就來新增導覽列的項目啦 ~ 畢竟現在的項目數量已經滿足不了我們了

但在新增之前我們要先處理一件事，那就是把現在 Hexo 預設的樣板主題：landscape 安裝好，關於 Hexo 主題的挑選方式在後面會再做介紹

先進到 [landscape 的 GitHub 頁面](https://github.com/hexojs/hexo-theme-landscape)，往下滑會看到 install 的說明內容，目前 Hexo 5.0 和以後的版本可以用 npm 方式安裝，但這邊先用 git 的安裝方式示範安裝，執行以下 git 指令：

```bash
git clone --depth 1 https://github.com/hexojs/hexo-theme-landscape themes/landscape
```

執行後會看到 themes 資料夾多出一個 landscape 的資料夾，然後你會在裡面看見一個 `_config.yml` 的檔案，這個檔案裡會有關於樣板主題的各種設定

![ themes 中 landscape 的 config 檔](https://ithelp.ithome.com.tw/upload/images/20250519/20172694wlwiyswC10.png)

點開那個 config 檔找到 menu ，你會發現它下面的項目很眼熟，沒錯，它就是你要修改的目標，在 menu 下再新增一行 `About： /about`

![在 menu 下新增 about ](https://ithelp.ithome.com.tw/upload/images/20250519/20172694YPU9BM5Ndy.png)

修改後儲存再開啟 Hexo 伺服器，你就會看見上方導覽列多出了一個 About，點進去就可以看見你的 about 頁面囉 ~

![上方導覽列出現 About 項目](https://ithelp.ithome.com.tw/upload/images/20250519/20172694uKpZlJqqxR.png)

### 怎麼把導覽列項目名稱改成中文

相信聰明的你，在修改過程中已經發現了，`About： /about` 中前面的 About 就是導覽列項目的名稱，所以只要將 `About： /about` 改成 `關於： /about` ，導覽列 About 項目名稱就會被改成「關於」囉 ~

當然也可以把所有導覽列項目都改成中文，改法跟 About 一樣，修改完就會像這樣

![修改後中文導覽列項目名稱](https://ithelp.ithome.com.tw/upload/images/20250519/20172694vMBke8D5sO.png)

## 結語

今天的介紹就到這邊，大家可以試著新增頁面，嘗試修改文章細節，希望這篇文章能幫助到在學習 Hexo 的你，那我們下篇文章見 ~
