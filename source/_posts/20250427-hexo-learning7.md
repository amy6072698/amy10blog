---
title: 從零開始學 Hexo (7) | 部署你的落格網站與常見 Hexo 指令
date: 2025-04-27 21:13:55
categories:
  - Hexo
tags: 
  - Hexo
  - 前端
description: 介紹如何將自己的 Hexo 部落格網站部署到 GitHub Pages
---

## 前置

### 確認是否已安裝 git

在開始往下介紹如何用部署你的 Hexo 部落格之前，我們要先確認是否有正確安裝 git，如果你是跟著前幾篇文章實作的朋友，基本上是不用擔心沒有安裝的，因為安裝 Hexo 前，官網的文件就有說明要先安裝 git

如果你還是想確認可以執行以下指令，有回傳版本號表示你已經安裝好 git 了

```bash
git --version
```

還未完成安裝的話可以到參考[這系列文章的第二篇](https://amy6072698.github.io/amy10blog/2025/04/22/20250422-hexo-learning2/)，先完成安裝

---

### 註冊你的 GitHub

確定安裝好 git 之後，先前往 [GitHub 官網](https://github.com/) 註冊你的 GitHub 帳號

進入官網點擊右上角的 Sign up 按鈕
![ GitHub 官網註冊按鈕](https://ithelp.ithome.com.tw/upload/images/20250519/20172694xdZhyBnX72.png)

接下來就是註冊帳號會有的流程，讓你填寫一些基本資料、回答一些問題 ( 主要是 GitHub 要調查你申請帳號的用途 )，然後請你選擇方案，如果不需要付費才有的功能選擇免費就好

---

### 讓 VSCode 綁定你的 GitHub 帳號

如果你跟我一樣使用 VSCode，要記得綁定你的 GitHub 帳號往下介紹前先做個小補充：[讓 VSCode 介面中文化套件](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hant)

可以在 VSCode 左邊找到以下圖示，然後在側欄搜尋框搜尋 chinese，找到中文化套件點擊它之後右邊會出現這個套件的相關介紹，點擊「安裝」按鈕，然後關掉 VSCode 在重開就可以看見中文化的 VSCode 介面囉 ~

![ VSCode 延伸模組圖示](https://ithelp.ithome.com.tw/upload/images/20250519/201726946kGiHmSY4C.png)

安裝完套件之後相信大家就能看見中文化的介面了，接下來往下介紹如何讓 VSCode 綁定 GitHub 帳號

打開 VSCode 點擊左下的人像 icon，再選擇「啟用雲端變更...」( 英文介面應該叫：Turn on Cloud Changes... )

![點擊左下人像 icon，選啟用雲端變更](https://ithelp.ithome.com.tw/upload/images/20250519/20172694Be3GJcerGO.png)

然後最上方搜尋框會跳出兩個項目，選擇「利用 GitHub 登入」

![上方搜尋框選擇利用 GitHub 登入](https://ithelp.ithome.com.tw/upload/images/20250519/20172694aif6smUhN5.png)

再來就會跳出一個 GitHub 的視窗，要你確認綁定的帳號，確定好後點擊「Continue」

![確認綁定帳號點擊 Continue](https://ithelp.ithome.com.tw/upload/images/20250519/20172694sgoa8Daeq5.png)

然後就會出現請你授權給 VSCode 的視窗，點擊「Authorize Visual-Studio-Code」

![授權給 VSCode 的視窗](https://ithelp.ithome.com.tw/upload/images/20250519/20172694yIptVAl5vi.png)

最後會出現確認視窗，點擊「開啟 Visual Studio Code」

![開啟 Visual Studio Code 的確認視窗](https://ithelp.ithome.com.tw/upload/images/20250519/20172694CHx2ik1Qc2.png)

打開 VSCode 點擊左下的人像 icon，就可以看見圖中白色長方處會出現你的 GitHub 帳號，如果中間遇到錯誤可以關閉 VSCode 再重啟

![點擊左下人像 icon，可以看見你的 GitHub 帳號](https://ithelp.ithome.com.tw/upload/images/20250519/20172694y2mlNpeqAZ.png)

如果以上步驟都順利完成就恭喜你完成綁定囉🎉

## 新增 GitHub 空間

完成前置的一番奮鬥，接下來就可以用你的 GitHub 帳號新增 GitHub 空間，也就是 GitHub 儲存庫 ( GitHub repository，以下簡稱 GitHub repo )，把你的 Hexo 部落格推上去囉 ~

登入你的 GitHub 帳號後會出現你的 Dashboard，點擊右上方你的頭像會跳出以下選單，選擇「Your repositories」

![ Your repositories 選項位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694odgHCcrUM1.png)

進入 Your repositories，這裡會有所有你創建的 GitHub repo，點擊右上方的「New」按鈕

![ New 按鈕位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694ezQkyiE83a.png)

然後就可以在 Repository name 填入你的 GitHub repo 名稱

![ Repository name 位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694D1kDzrkuK7.png)

完成後就點擊下方的「Create repository」按鈕，就可以進入你剛剛建立的 GitHub repo 頁面了，左上 GitHub Logo 旁邊的白色長方處會顯示你的 GitHub 帳號，在往右就是你剛剛命名的 GitHub repo 名稱

![ GitHub repo 頁面](https://ithelp.ithome.com.tw/upload/images/20250519/20172694G2e3kizOOb.png)

學會如何新增 GitHub repo 之後，我們就繼續往下前進

## 部署你的部落格到 GitHub Page

首先，先到 Hexo 的官方文件，上面有寫到關於「在 GitHub Pages 上部署 Hexo」的內容，讓我們看到[「一鍵部署」( One-command deployment )](https://hexo.io/zh-tw/docs/github-pages#One-command-deployment)這一節的內容

接下來就一步步完成部署吧 ~ 首先進入 [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)，往下滑查看 README 的說明，可以看到 Installation 提供了以下安裝指令

```bash
npm install hexo-deployer-git --save
```

複製安裝指令貼到終端機 ( 記得確認是否在 Hexo 部落格資料夾的路徑上 )，然後執行

![執行安裝 hexo-deployer-git 的指令](https://ithelp.ithome.com.tw/upload/images/20250519/20172694Ks8PnDTsDP.png)

安裝好之後，要在「全站的 config 檔」中加入以下內容

```yml
deploy:
  type: git
  repo: https://github.com/<username>/<project>
  # example, https://github.com/hexojs/hexojs.github.io
  branch: gh-pages
```

點開全站的 config 檔後，找到 `deploy` 的區塊替換成以上內容，這時候眼尖的你一定會發現 repo 這一項似乎有些內容要修改

沒錯，網址中的 `<username>` 要改成你的 GitHub 帳號，`<project>` 則要改成你的 GitHub repo 名稱，假設我的帳號是「amy12345」、repo 名稱是「amy_hexo」，那 repo 這項就要改成：`https://github.com/amy12345/amy_hexo`

其中 branch 這項，代表之後部署 Hexo 部落格到 GitHub Pages 時，會部署到哪個分支名稱，這邊可以直接用預設名稱 gh-pages

![新增 deploy 內容到全站 config 檔](https://ithelp.ithome.com.tw/upload/images/20250519/20172694g6tmS3msZC.png)

接下來是不是要下指令部署啦？

先等等！全站的 config 檔還有東西要改，我們找到 `url` 然後會看見檔案中的註解有提示，如果你是用 GitHub Pages 要把 `url` 這項改成：`https://username.github.io/project`，經過前一個步驟，聰明的你一定已經知道要怎麼改了吧 ~

用我前面的範例套用，我的 `url` 這項就要改成：`https://amy12345.github.io/amy_hexo`

![修改 url 網址](https://ithelp.ithome.com.tw/upload/images/20250519/201726945eqhPSD2zX.png)

好的，接下來就是期待已久的下指令啦 ~ 執行以下指令部署你的 Hexo 網站到 GitHub Pages ( 如果之後要更新網站內容一樣要用以下指令部署 )

```bash
hexo clean && hexo deploy
```

![執行 hexo clean && hexo deploy 指令](https://ithelp.ithome.com.tw/upload/images/20250519/201726945MZuwAZHdr.png)

- **補充**：`hexo clean` 跟 `hexo deploy` 是兩個不同指令，`hexo clean` 會清除原先有的 public 資料夾，確保後續部署的是最新的網站內容，而 `hexo deploy` 執行後會產生 public 資料夾，裡面是編譯後的網站內容，且還會把編譯內容部署到 GitHub Pages

![hexo deploy 指令](https://ithelp.ithome.com.tw/upload/images/20250519/20172694hUBnwMb0tH.png)

執行完成後回到你的 GitHub repo 頁面，重新整理就會看見出現了剛剛部署的 gh-pages 分支

![ GitHub repo 頁面更新](https://ithelp.ithome.com.tw/upload/images/20250519/20172694eywtSg9EJh.png)

然後點擊上方的「Settings」

![點擊 Settings ](https://ithelp.ithome.com.tw/upload/images/20250519/201726949LOHOiU9MD.png)

選擇左側欄的「Pages」，就會在黃框處看見你部署到 GitHub Pages 的部落格網址，如果沒出現網址就稍等一下再重整網頁

![ GitHub Pages 網址位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694fv24Mpv2xe.png)

點進網址後，就可以看見你的部落格囉 ~

![部署部落格完成的樣子](https://ithelp.ithome.com.tw/upload/images/20250519/20172694vAPPC9dejM.png)

- **小提醒**：點進網址後如果還沒出現預期的網站樣式，就等一下再重整網頁或用無痕模式開看看，等很久還是沒反應，就需要檢查前面提到的全站 config 檔設定，是否有錯誤或缺漏，有的話修改儲存後再重新下指令部署

## 常見 Hexo 指令

看到這篇文章恭喜你👏已經將 Hexo 指令學得差不多了，接下來就列出一些比較常見的 Hexo 指令做個小統整吧 ~

- `hexo init 你的網站英文名稱`：初始化 Hexo 部落格環境的指令，init 後面接自訂的網站英文名稱，執行後會在專案資料夾中，新增 Hexo 部落格網站的資料夾，該資料夾名稱與自訂的網站英文名稱相同
- `hexo server` 或 `hexo s`：開啟 Hexo 伺服器，執行後可以在本地端查看 Hexo 網站的樣子
- `hexo new '你的文章名稱'`：新增 Hexo 部落格文章，new 後面接自訂的文章名稱，記得名稱要用單引號包住，執行後會在 `source` 內的 `_posts` 資料夾中新增一個文章的 md 檔
- `hexo new page 頁面英文名稱`：新增 Hexo 網站的頁面，page 後面接頁面英文名稱，執行後會在 `source` 內新增該頁面名稱的資料夾，裡面有 `index.md` 檔，頁面相關設定可見本系列文章第五篇
- `hexo clean`：執行後會清除 public 資料夾
- `hexo deploy`：執行後會產生 public 資料夾，並把裡面編譯後的網站內容部署到 GitHub Pages
- `hexo generate` 或 `hexo g`：執行後會產生 public 資料夾，裡面是編譯後的網站內容，和 `hexo deploy` 不同，不會把網站內容部署到 GitHub Pages

## 結語

看完這篇文章相信大家都能夠了解，如何將自己的 Hexo 部落格網站部署到 GitHub Pages 了，其實說到 GitHub 通常會講到 git 指令，但是這個系列主要還是介紹 Hexo，怕模糊焦點所以就先不談 git 的相關知識 ~~(留給未來的我寫~~

作為補償我幫大家整理了 Hexo 的常見指令，請笑納🫡，不過如果想多了解 git 的內容可以參考以下的一些學習資源：

- [Git & GitHub 教學手冊](https://w3c.hexschool.com/git/cfdbd310)
- [為你自己學 Git](https://gitbook.tw/)

那我們就下篇文章見囉 ~
