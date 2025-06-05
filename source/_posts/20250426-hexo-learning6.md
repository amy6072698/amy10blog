---
title: 從零開始學 Hexo (6) | 認識 Hexo 目錄與調整全站網站設定
date: 2025-04-26 19:32:58
categories:
  - Hexo
tags: 
  - Hexo
  - 前端
description: 介紹 Hexo 部落格資料夾裡有哪些資料，以及如何調整網站的相關資訊內容
---

## 認識 Hexo 目錄結構

在開始講解如何部署你的部落格網站之前，我們先簡單認識一下 Hexo 資料夾內的目錄結構吧！什麼？你說為什麼？看下去就知道啦 ~

還記得一開始下 Hexo 指令的時候嗎？對的，就是你下了一個像 `hexo init 你的網站英文名稱` 這樣的指令，然後 Hexo 就咻的把一個 Hexo 部落格資料夾丟進你的專案資料夾裡了

前面一直都沒有細談 Hexo 給的這個部落格資料夾裡面到底有什麼，接下來就簡單說明裡面的內容，以我的部落格資料夾為例，裡面有這麼多資料夾及檔案，接下來就簡單講解幾個資料夾及檔案的作用吧 ~

![部落格資料夾](https://ithelp.ithome.com.tw/upload/images/20250519/20172694MGmxffqIXw.png)

### node_modules

裡面會存放很多很多 ~~( 多到無法想像 )~~ 專案 ( 你的部落格網站 ) 所需的所有套件資料，所以它通常不會被加入 git 的版本控制，就不會被 push 傳到遠端的 GitHub 儲存庫

假設這個專案需要和別人協作開發，對方把資料 `git clone` 下來 (從遠端 GitHub 儲存庫抓下來)，而抓下來的資料當然不會有 node_modules ，不過只要執行 `npm intsall` 指令，就會自動產生 node_modules 這個資料夾了

~~所以就不需要把藍鯨 ( node_modules ) 冰到小冰箱裡了，可以多冰幾顆布丁~~

如果你對 git 還不了解，可先忽略不懂的部分，只要知道 node_modules 是用來放你的部落格網站所有所需套件的資料夾就好

### scaffolds

這個資料夾裡有下 Hexo 指令生成草稿、頁面及文章的預設模板檔案，分別是 `draft.md`、`page.md`、`post.md`

![ scaffolds 資料夾裡的檔案](https://ithelp.ithome.com.tw/upload/images/20250519/20172694SDjvVvjwsi.png)

還記得前篇提到的，文章開頭可以寫入 tags 嗎？

假設我希望每次下 `hexo new '文章名稱'` 指令產生的文章檔，都要在文章開頭加 description 項目，就要改 `post.md` 這個檔案，像這樣：

![ post.md 檔新增 description](https://ithelp.ithome.com.tw/upload/images/20250519/20172694YOv5aamCpL.png)

這樣下次執行 `hexo new '文章名稱'` 指令，文章開頭就會多出 description 囉 ~

順便補充生成草稿的 Hexo 指令：`hexo new draft` ( 雖然我比較少用 )

### source

再來我們目前最熟悉的 source 資料夾 ~ 前面講到你的部落格文章、頁面檔案都會放在這個資料夾

### themes

這個資料夾會用來放安裝下來的 Hexo 樣板主題資料，看到資料夾名稱有 `s` 對嗎？沒錯，是複數這表示它可以放不只一種主題，至於 Hexo 如何更換主題之後會再講解 ~~( 保留點神祕感 )~~

### _config.yml (全站)

奇怪這個檔名？好眼熟！眼熟就表示你前篇有認真看👏

沒錯，前篇有提到 themes 的 landscape 資料夾內也有一個 `_config.yml` 檔，但是和這裡的 `_config.yml` 檔當然是不同的，這就是為什麼要先認識 Hexo 目錄的原因

這裡的 `_config.yml` 檔網站全站的設定檔，不是主題的設定檔，也就是當你需要調整一些全站設定時，就會來這裡修改這個全站的 config 檔

為了避免誤會先定義好兩者的名稱，接下來 themes 的 `_config.yml` 檔，我會叫「主題的 config 檔」，這個全站的 `_config.yml` 檔，就叫「全站的 config 檔」

### .gitignore

顧名思義，這個檔案是用來列出要被 git 忽略的檔案，裡面列出的檔案不會被 git 加入版本控制 ~~讓檔案變成小透明的地方~~，聰明的你應該有發現 node_modules 也在裡面

### package.json

這個檔案用來記錄專案使用的套件版本資訊、可以下哪些指令等專案的基本資訊，前面有提到可以透過 `npm install` 重新安裝專案所需的所有套件，至於要下載哪些、和哪個版本的套件就是這個檔案存在的意義了

## 調整網站全站設定

前面講一堆，終於到動手做的時候啦 ~

如果你觀察現在的首頁，會發現有一點就是很想給他改掉啦！沒錯，就是那大大 Hexo 單字，那是什麼？跟我部落格完全不搭 ~~( Hexo 別生氣，沒有針對你的意思 )~~

好，說改就改！想修改它就要修改「全站的 config 檔」( 是全站不是主題喔 )，打開檔案後找到 `# Site` 就可以設定專屬於你的網站資訊囉 ~

![全站的 config 檔 Site 設定](https://ithelp.ithome.com.tw/upload/images/20250519/20172694kU4mbGaCqz.png)

內容可以自己慢慢想，我自己光部落格網站的名稱就想了很久，如果想了解更多全站設定的內容可以參考 [Hexo 官網文件的配置部分](https://hexo.io/zh-tw/docs/configuration)

設定好儲存開啟伺服器之後，首頁的 Hexo 就改為 Amy 的小天地啦🎉

![修改後首頁畫面](https://ithelp.ithome.com.tw/upload/images/20250519/201726944w8bfhr7ya.png)

那你一定會疑惑其他項目改了哪裡？請對網頁按下滑鼠右鍵選「檢視網站原始碼」，看看程式碼前面幾行是不是出現剛剛設定的內容了？

![檢視網站原始碼畫面](https://ithelp.ithome.com.tw/upload/images/20250519/20172694wPo7ljTSyX.png)

這樣就能客製化你的網站資訊了，記得一定要填 title 和 description，這樣可以幫助你的網站更容易被搜尋到喔 ~

## 結語

這篇文章介紹了 Hexo 部落格資料夾裡面，到底有哪些神秘資料，這邊主要講解一些比較簡單的介紹，因為不知道大家 git 程度，不知道怎麼寫新手也能理解，有點小困擾但是還是寫完了，最後還講了如何客製化自己的部落格全站網站設定

大家可以試著開始想自己的部落格名稱囉 ~ 也可以想到再來重溫這篇文章，那我們就下篇文章見囉 ~
