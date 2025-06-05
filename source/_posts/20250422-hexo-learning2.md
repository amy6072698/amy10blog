---
title: 從零開始學 Hexo (2) | Hexo 安裝方法
date: 2025-04-22 11:16:29
categories:
  - Hexo
tags: 
  - Hexo
  - 前端
description: 了解 Hexo 安裝前需求與如何安裝 Hexo 
---

## 想了解 Hexo 從官網開始

想知道怎麼安裝 Hexo，第一站就是 [Hexo 的官網](https://hexo.io/zh-tw/) ，進入官網後點上方導覽列的「文件」:

![進入 Hexo 官網後點上方導覽列的文件](https://ithelp.ithome.com.tw/upload/images/20250429/20172694EThBdppvdH.png)

然後你就可以看到 Hexo 很貼心的把安裝方式放在文件的第一頁囉 ~

![ Hexo 的安裝方式在文件第一頁](https://ithelp.ithome.com.tw/upload/images/20250429/20172694pKvZW6QO9e.png)

往下滑你可以看到更多關於 Hexo 安裝需要的東西：

![ Hexo 安裝需求](https://ithelp.ithome.com.tw/upload/images/20250429/20172694sCbdH74cis.png)

首先安裝需求的部分會需要先安裝 Node.js 和 Git，先從 Node.js 的安裝開始

---

## 安裝 Node.js

如果你曾經看過以前的文章講解如何安裝 Node.js，那你就會看見以下這張圖，它有兩種下載按鈕，一個是 LTS 版本、一個是 Current 版本

![舊版 Node.js 官網下載安裝按鈕](https://ithelp.ithome.com.tw/upload/images/20250429/201726942qi9mlKzLY.png)

這兩種版本差異簡單講就是 LTS (Long-term support) 長期支援版是當前穩定的版本，Current 則是最新版本，一般如果不是為了最新功能不會去下載 Current 版，所以這邊就下載 LTS 版本就可以囉 ~

不過現在[官網](https://nodejs.org/zh-tw)已經改成只有 LTS 一個按鈕了，所以上面說明就當作是小補充吧，把那唯一的下載按鈕揍下去就對了

![新版 Node.js 官網下載安裝按鈕](https://ithelp.ithome.com.tw/upload/images/20250429/20172694Lkc9MCfbK2.png)

下載完成之後你的下載資料夾會出現 Node.js 的安裝檔，點兩下開啟檔案然後按 Next 按鈕、勾選同意，然後一路按 Next 按鈕最後再按下 Install 按鈕就可以完成安裝了

如果你按安裝過程中沒有指定位置，安裝完之後的 Node.js 一般會在本機的 Program Files 資料夾中：

![安裝完之後的 Node.js 一般會在本機的 Program Files 資料夾中](https://ithelp.ithome.com.tw/upload/images/20250429/20172694to0E2nkZ3Z.png)

---

## 安裝 Git

要安裝 Git 就先進入它的[官網](https://git-scm.com/)，進入後往下滑會看見一台小電腦在畫面上，它會判斷你是 Windows 還是 Mac 系統，按下下載按鈕：

![ Git 官網下載安裝按鈕](https://ithelp.ithome.com.tw/upload/images/20250429/20172694adon1sG4bp.png)

然後官網會跳轉下載頁面，並自動下載，若沒有自動觸發，可點擊下圖 Click here to download 連結手動下載：

![ Git 官網 Click here to download 連結手動下載](https://ithelp.ithome.com.tw/upload/images/20250429/20172694y749Bk58j7.png)

下載完成之後你的下載資料夾會出現 Git 的安裝檔，一樣點兩下開啟檔案，再來就是按肯定的按鈕 ~~(說 Yes 就對了~~ ，然後按下安裝，這樣就完成安裝囉 ~

---

## 安裝 Hexo 前先檢查

再來就要開啟終端機檢查有沒有成功安裝好 Node.js 和 Git 了，開啟終端機後輸入以下指令如果系統都有回應你剛剛安裝的版本號碼就表示你正確完成安裝囉 ~

### 檢查是否安裝 Node.js

```bash
node -v
```

### 檢查 npm 是否正常

npm 是 Node.js 預設的軟體套件管理系統，會隨著 Node.js 安裝時一起安裝，因為之後會透過 npm 進行 Hexo 的安裝，所以一定要確保 npm 有正常安裝

```bash
npm -v
```

### 檢查是否安裝 Git

```bash
git --version
```

---

## 安裝 Hexo

終於進入安裝 Hexo 的階段啦~~~ 確認以上軟體安裝完成後，接下來依照[官網的安裝指示](https://hexo.io/zh-tw/docs/#%E5%AE%89%E8%A3%9D-Hexo)，執行以下指令就可以透過 npm 來安裝 Hexo 囉 ~

```bash
npm install -g hexo-cli
```

### 檢查 Hexo 是否安裝成功

接下來別忘記檢查 Hexo 是否安裝成功，執行以下指令，如果有成功跑出版本號碼，那麼就恭喜你成功安裝好 Hexo 囉🎉

```bash
hexo -v
```

---

## 你可能會遇到 PowerShell 執行原則問題

如果你是使用 Windows 系統的 PowerShell 為執行指令的終端機，或你是開 VSCode 內的終端機(VSCode 預設使用的終端機是 PowerShell)，那在安裝時你可能會遇到 PowerShell 的執行原則問題 ~~(提前說以免有人再掉到坑裡，維護安全人人有責~~

### 情況說明

當你執行指令打算美美的完成 Hexo 安裝時，發現它回了一串錯誤給你，有可能長得像這樣：

```bash
hexo : 因為這個系統上已停用指令碼執行，所以無法載入 ...
```

講一堆就是不給你安裝的意思，那有可能是 PowerShell 的執行原則產生的問題， Windows 預設的 powershell 執行原則為 `Restricted`

 **PowerShell 有四種執行原則：**

  1. Restricted：所有 `PowerShell Script`(.ps1) 皆無法執行(Windows系統預設)
  2. AllSigned：所有 `PowerShell Script` 都要經過受信任的發行者簽屬過後才可執行
  3. RemoteSigned：針對從異地下載下來的 `PowerShell Script` 需要經過受信任的發行者簽屬過後才可執行，本機的 `PowerShell Script` 可直接執行
  4. Unrestricted：無限制，所有 `PowerShell Script` 皆可執行

### 解決方法

想解決前面出現的錯誤其實只要改變執行原則的設定即可，但在改變之前要先執行以下指令確認 PowerShell 現在是哪個執行原則：

```bash
get-executionpolicy
```

如果它回 `Restricted`，再往下執行以下指令，執行後會有視窗詢問，按下確定後就能將執行原則改為 `Remotesigned`

```bash
set-executionpolicy remotesigned
```

但如果不幸還是跳出錯誤，長得像這樣：

```bash
Set-ExecutionPolicy : 拒絕存取登錄機碼...
```

那就再往下執行以下指令，就能成功執行了：

```bash
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

希望大家還是不要踩到坑比較好，如果不幸遇到的話希望這個問題補充可以幫助到你，以上內容參考自[CC的技術隨筆 VSCode 執行 npm install 失敗文章](https://akoncc.github.io/2019/11/01/vscode-cant-run-script/)，想了解更詳細內容可以去看看

那就先祝大家都順利安裝 Hexo 成功囉 ~ 我們下篇文章見🪄
