---
title: 從零開始學 Hexo (9) | Hexo 主題選擇及更換網站主題
date: 2025-04-29 23:15:43
categories:
  - Hexo
tags: 
  - Hexo
  - 前端
description: 介紹挑選 Hexo 網站主題的注意事項，及如何安裝並更換主題
---

## 關於 Hexo 主題挑選

Hexo 的主題不只有 landscape 這一種，還有許許多多的主題模板可以套用，進入 [Hexo 官網的主題頁面](https://hexo.io/themes/)，你就能看見很多主題

![Hexo 官網的主題頁面](https://ithelp.ithome.com.tw/upload/images/20250519/20172694OpdIEeJvSu.png)

點擊任一個主題標題名稱 ( 如上圖紅框處 )，可以進入該主題的 GitHub 頁面，裡面會有主題的安裝方式、使用說明等資訊

如果想看套用該主題的範例網站，就點擊「Visit preview site」( 如上圖綠框處 )

有很多主題可以選當然好，但是選擇障礙就出來了，挑選主題有沒有什麼需要注意的事項呢？

當然有，接下來就來針對挑選主題要注意的點來說明吧 ~

### 有實力有經驗也不懶怎麼選都行

如果你有一定開發實力，且有開發過主題的經驗，然後也不懶熱衷於挑戰 (？，那麼你想挑什麼主題都可以，反正有問題可以自己改👍

但如果你跟我一樣比較懶，可以根據以下提到的兩點挑選主題，可以少一些研究主題的時間，更專注在部落格經營及技術文章撰寫上

- **挑選有持續維護的主題**
- **挑選熱門的主題**

### 挑選有持續維護的主題

前面有說可以透過 Hexo 官網的主題頁面，進入到該主題的 GitHub 頁面，在這邊可以看見主題的一些相關資訊

以 [NexT](https://github.com/next-theme/hexo-theme-next) 這個主題為例，下圖紅框處可以看見更新專案的時間，這邊可以看到上個月甚至昨天都有更新

![NexT 主題的 GitHub 頁面](https://ithelp.ithome.com.tw/upload/images/20250519/201726945u7gUAbe4k.png)

這個更新的時間，可以作為這個主題是否有持續維護的判斷標準，如果更新時間是好幾年前，那表示這個主題已經很久沒有更新維護了

這樣對於使用較新版本 Hexo 的使用者來說，可能不是一個好選項，因為沒有持續維護的主題，可能會與現在使用的 Hexo 版本不相容，主題無法被新版本的 Hexo 編譯，就只能放棄這個主題了

除非有足夠實力自己修正問題，不然建議選擇有持續維護的主題套用，避免以上的狀況發生

### 挑選熱門的主題

另一個挑選主題的重點是挑選熱門的主題，那要如何判斷我選的主題熱不熱門呢？

一個主題熱不熱門，除了搜尋主題名稱，查看網路上相關技術文章的數量之外，也可以透過該主題的 GitHub 頁面找到一些蛛絲馬跡

頁面右上的這個星星數量就可以作為判斷，星星數量越多越熱門

![ GitHub 頁面星星數量](https://ithelp.ithome.com.tw/upload/images/20250519/20172694K4zi2b5tgU.png)

另外 Issues 的數量也可以當作判斷標準，熱門的主題因為比較多人使用，就容易有較多人在使用上遇到問題，然後到 GitHub 頁面尋求協助，所以主題的 Issues 數量越多越熱門

像是 [NexT 主題 GitHub 的 Issues 分頁](https://github.com/next-theme/hexo-theme-next/issues)，下圖黃框處已解決 ( Closed ) 的 Issue 就算蠻多的了

![ GitHub 頁面 Issues 數量](https://ithelp.ithome.com.tw/upload/images/20250519/20172694ZrDmWd6SCz.png)

會建議挑選熱門的主題，是因為社群針對熱門主題的討論度較高，這樣未來若遇到實作上的問題，可以參考學習的資源也較多

## 更換 Hexo 網站主題

接下來會以 NexT 來示範，如何更換 Hexo 網站的主題

我們知道原本 Hexo 網站的主題，預設是套用 landscape，假設現在我們想把網站主題換成 NexT 主題，要怎麼做呢？

- **注意**：如果前面有針對 landscape 主題客製化，為避免調整影響到 NexT 主題的套用，建議重新建立一個新的 Hexo 部落格環境或移除客製化設定，再依照以下步驟更換主題

首先，先進入到 [NexT 主題的 GitHub 頁面](https://github.com/next-theme/hexo-theme-next)，滑到頁面下方會看到 README 裡有安裝方法

Installation 列出兩種安裝方式，一種是透過 npm 但 Hexo 版本要 5.0 或以上，另一種是用 git clone 的方式

![NexT 主題 Installation](https://ithelp.ithome.com.tw/upload/images/20250519/201726946uYRhGVzAP.png)

這邊示範採用 git clone 的方式安裝主題，開啟終端機注意是否在 Hexo 部落格資料夾的路徑上，是的話執行以下指令

```bash
git clone https://github.com/next-theme/hexo-theme-next themes/next
```

執行後打開 themes 資料夾，可以看到多了一個 next 的主題資料夾

![next 資料夾位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694AudyMQ9GdX.png)

接下來打開全站的 config 檔，找到 theme 把 landscape 改成 next

![修改全站設定的 theme](https://ithelp.ithome.com.tw/upload/images/20250519/20172694tqFKQibUB2.png)

修改後儲存再打開 Hexo 伺服器，點開網址就可以看見網站被改成 NexT 主題的樣式囉 ~

![NexT 主題網站樣式](https://ithelp.ithome.com.tw/upload/images/20250519/20172694XmMRzK08rP.png)

如果要更換成其他主題，也是差不多的方式，參考該主題的安裝方式先進行主題安裝，再調整全站 config 的 theme 設定

## 結語

這篇文章介紹了如何挑選你的 Hexo 網站主題，以及如何安裝並更換主題，看完這篇文章大家可以試著挑選喜歡且合適的主題囉 ~

希望大家都可以有美美的 Hexo 網站，每個主題客製化上面設定可能會不一樣，但前篇文章提到的客製化方法，應該多少還是可以作為實作時的參考

接下來文章因為我個人創建自己的部落格，研究比較多的是 NexT 主題，所以會以如何客製化 NexT 主題為主要方向

那我們就下篇文章見囉 ~
