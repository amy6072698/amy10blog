---
title: 從零開始學 Hexo (1) | Hexo 安裝方法
date: 2024-05-26 02:11:52
categories:
  - Hexo
tags: 
  - Hexo
  - 前端
description: 了解 Hexo 是什麼，安裝前須知和如何安裝 Hexo 
---

## 什麼是 Hexo？

Hexo 是一個快速、簡單且強大的網誌框架
Hexo 使用 Markdown（或其他標記語言）解析您的文章，並在幾秒鐘內，透過漂亮的主題產生靜態部落格網站

## 安裝前先檢查

安裝 Hexo 之前先檢查是否已安裝 Node.js 及 Git，若不確定是否已安裝可在終端機下以下指令：

### 檢查是否安裝 Node.js

``` bash
node -v
```

### 檢查 npm 是否正常

``` bash
npm -v
```

npm 是 Node.js 預設的、用 JavaScript 編寫的軟體套件管理系統，之後會透過 npm 進行 Hexo 的安裝

### 檢查是否安裝 Git

``` bash
git --version
```

若成功跑出版本號碼代表安裝成功，若還未安裝可至以下網址進行安裝：

* [Node.js](https://nodejs.org/en) (Node.js 版本需不低於 8.10，建議使用 Node.js 10.0 及以上版本)
* [Git](https://git-scm.com/)

## 安裝 Hexo

確認以上軟體安裝完成後就可以透過 npm 來安裝 Hexo 囉~

### 執行以下指令透過 npm 安裝 Hexo

``` bash
npm install -g hexo-cli
```

### 檢查 Hexo 是否安裝成功(跑出版本號碼代表安裝成功)

``` bash
hexo -v
```

若是透過 PowerShell 安裝，一直無法安裝成功可以參考[這篇文章](https://akoncc.github.io/2019/11/01/vscode-cant-run-script/)


遇到其他問題可參考 [Hexo 官網](https://hexo.io/zh-tw/)