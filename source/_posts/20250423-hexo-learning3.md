---
title: 從零開始學 Hexo (3) | 下 Hexo 指令建立部落格環境吧 ~
date: 2025-04-23 14:26:12
categories:
  - Hexo
tags: 
  - Hexo
  - 前端
description: 如何帥氣的下指令建立 Hexo 環境😎，在本機查看你建立的 Hexo 部落格吧 ~ 
---

## 建立 Hexo 環境的前置

經過前篇 ~~激烈的戰鬥~~ 努力的奮鬥，相信大家都安裝好 Hexo 了，那接下來要做的就是建立你的 Hexo 部落格環境啦 ~

### 建立專案資料夾

首先，在桌面(或其他你想建立專案資料夾的地方)建立一個專案資料夾，我這邊就先在桌面建立一個 amyHexo 的資料夾 ~~(沒錯，我桌面背景是紅色的~~ ，資料夾的名字可以自己取不用和我一樣

![在桌面建立 amyHexo 的資料夾](https://ithelp.ithome.com.tw/upload/images/20250429/201726949J7FjsCAB7.png)

### 用cd指令移動到指定的路徑

再來開啟終端機執行 `cd` 指令移動到專案資料夾如下，你的資料夾要看你建立在哪個路徑再將你的路徑填入以下 `你的專案資料夾路徑` 位置裡 (注意：cd 後面有一個空白字元再接路徑)

```bash
cd 你的專案資料夾路徑
```

以我建立的 amyHexo 的資料夾為例，就要執行 `cd c:\Users\User\Desktop\amyHexo` 這個指令，每個人的 User 名字可能不一樣那就看你自己叫什麼囉 ~

### 快速填入指定資料夾路徑的方法

如果你懶得輸入這麼長的路徑，有一個方法可以試試看，先在終端機輸入 `cd` 和一個空白字元，再把你想前往的專案資料夾用滑鼠按住左鍵拖曳到終端機視窗內

![把想前往的資料夾拖曳到終端機](https://ithelp.ithome.com.tw/upload/images/20250429/201726944tnpIC3tmI.png)

然後放開滑鼠左鍵， `cd` 空白後面就會自動填入你拖曳進來的資料夾路徑囉 ~

![放開就會自動填入該資料夾位置](https://ithelp.ithome.com.tw/upload/images/20250429/20172694ewCUEzUq4x.png)

---

## 下 Hexo 指令建立環境

再來就進入重頭戲用 Hexo 指令來建立你的部落格環境囉 ~

前面講到 `cd` 移動到你的專案資料夾中，確定有移動到正確路徑下之後，執行以下指令，其中 `你的網站英文名稱` 可以自己取名：

```bash
hexo init 你的網站英文名稱
```

以我的部落格網站英文名稱 amy10blog 為例，下完 `hexo init amy10blog` 指令後，終端機成功跑完回應就成功囉 ~

![終端機執行 hexo init ](https://ithelp.ithome.com.tw/upload/images/20250429/20172694Z78eK5oMQd.png)

執行完以上指令後， Hexo 就會在專案資料夾中建立一個新資料夾，這個新資料夾會用剛剛指令輸入的 `你的網站英文名稱` 命名，以我的為例新資料夾就會叫 `amy10blog`：

![新資料夾名稱](https://ithelp.ithome.com.tw/upload/images/20250429/20172694KdrmLtwayg.png)

而新資料夾裡面是所有 Hexo 部落格環境會需要用到的東西，給瞄你一眼：

![資料夾內 Hexo 部落格環境會需要用到的東西](https://ithelp.ithome.com.tw/upload/images/20250429/20172694rIxaAoeMRt.png)

---

## 如何瀏覽 Hexo 為你建立的部落格網站呢？

說了這麼多，要怎麼看我現在的部落格網站長什麼樣子呢？一樣要用 Hexo 的指令，接著往下看

使用 Hexo 的指令在本地查看你的部落格網站之前，要記得先移動到 Hexo 剛剛在專案資料夾中幫你建的新資料夾路徑下，以我的為例，就是要移到 `amy10blog` 資料夾：

![先移動到 Hexo 剛剛在專案資料夾中幫你建的新資料夾路徑下](https://ithelp.ithome.com.tw/upload/images/20250429/201726944BzbPrOwIl.png)

接著，再執行以下指令，開啟 Hexo 伺服器

```bash
hexo server
```

如果嫌棄 `hexo server` 太長，下 `hexo s` 這個指令一樣可以開啟 Hexo 伺服器，如果要執行其他指令，想關閉伺服器，可以依照終端機的提示按下 ctrl + c 鍵即可關閉

![hexo server 開啟 Hexo 伺服器指令](https://ithelp.ithome.com.tw/upload/images/20250429/20172694y0YKDcJD69.png)

執行完之後它會回給你一段本地端的網址，點開網址就可以看見目前部落格的樣子囉 ~ 通常初始的部落格網站大家都會長這樣：

![ Hexo 部落格網站初始樣子](https://ithelp.ithome.com.tw/upload/images/20250429/20172694RC45P8QUN0.png)

後續會再教大家客製化的方法，不過會先把 Hexo 的基本指令講解完再討論這塊，也是有許多研究後的結果可以分享，那我們就下篇文章見囉 ~
