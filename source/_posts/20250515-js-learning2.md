---
title: JavaScript 修練 (2) | 陳述式與表達式
date: 2025-05-15 23:30:47
categories: 
  - JavaScript
tags:
  - JavaScript
  - 前端
description: 介紹陳述式與表達式的差異
---

## JavaScript 的文法概念

程式語言就像對電腦說的語言，和其他語言一樣也會有自己的文法概念，這些文法形成的語句，會影響電腦對程式碼執行的方式

本篇文章將介紹陳述式與表達式的差異，而下篇文章也會接續提到關於運算子執行的先後順序，這些都與 JavaScript 的文法相關，而開發中這種文法概念所產生的問題，往往不容易被察覺，所以如果能先了解一些觀念在除錯上也會比較容易發現問題所在，甚至避開可能發生的問題

## 陳述式與表達式

陳述式與表達式在學習過程中常常被忽略，但其實很常在各種技術文件中出現的專有名詞

陳述式與表達式在中文翻譯都有其他不同的名稱，但看英文原文就會知道說的是同一個東西，所以開始往下介紹之前，先來定義一下接下來文章的中文用詞：

- **Statement** ：中文翻譯有敘述句、陳述式，接下來文章都統一叫「陳述式」

- **Expression** ：中文翻譯有運算式、表示式、表達式，接下來文章都統一叫「表達式」

定義好用詞後，接下來先比較這兩者各自的特點，再來說明常看到的陳述式和表達式有哪些吧 ~

### 陳述式

陳述式特點如下：

- 會執行一些程式碼，但是 **不會回傳結果**
- 可能是幾個單詞或一個片段，但不會是單一個字母
- 其中可能混合表達式

### 表達式

表達式特點如下：

- 最大特點是 **會回傳結果**
- 單一個字也可以是表達式

---

### 哪些是常見的陳述式？

- 宣告 ( var、let、const、function )
- 流程控制 ( block、if...else )
- 迴圈 ( for、for...in )
- 其他 ( import、export )

#### 範例說明

再來看看幾個範例，實際觀察陳述式在 Chrome 的開發者工具 Console 中會顯示的內容

`var a;` 這個程式片段宣告了一個變數 a，是一個簡單的陳述式，而在 Console 中`<・` 符號後面內容代表 Console 回傳的結果，這邊看到這段程式碼結果會是 undefined，代表這段程式碼沒有取得值、不會回傳值

![ var a 陳述式在 Console 中的結果](https://ithelp.ithome.com.tw/upload/images/20250519/201726945X4wBALuaY.png)

前面提到陳述式可能混合表達式，接下來就來看看混合的範例

綠框延續上一個單純是陳述式的範例 `var a;`，黃框處透過運算子 `+` 計算 `2 + 2;`，會回傳計算結果 `4` 所以是表達式，橘框處則是混合綠框與黃框的陳述式，所以 Console 的回傳結果是 undefined

![陳述式混合表達式的結果](https://ithelp.ithome.com.tw/upload/images/20250519/20172694ZKuwl6LBq4.png)

#### undefined 產生的誤會

前面有提到「表達式最大特點是會回傳結果」，這樣陳述式在 Console 回傳的結果是 undefined 就容易因此產生誤會，因為會出現兩種情況：

- **不會回傳值** ：因為不會回傳值，所以 Console 回傳的結果是 undefined
- **會回傳值但沒有提供回傳值** ：此時就算會回傳值，Console 回傳的結果也是 undefined

只看以上說明可能有些抽象，讓我們看看以下範例吧

![說明回傳結果 undefined 的兩種狀況](https://ithelp.ithome.com.tw/upload/images/20250519/20172694DMNSLJ9Yn8.png)

圖中綠框處 fn1 和 fn2 都是用函是陳述式宣告的函式，所以陳述式在 Console 回傳的結果是 undefined，而呼叫函式會回傳值所以是表達式，而 fn1 函式在綠框片段中有提供回傳值，所以在黃框處呼叫 fn1 函式後，Console 回傳的結果是 `'我是 fn1 函式'`

容易產生誤會的片段在橘框，明明呼叫函式是表達式，怎麼 Console 回傳的結果是 undefined？

往前看綠框片段中的 fn2 並沒有提供回傳值，所以在橘框處呼叫函式時有回傳值，但是因為沒有提供回傳值，所以 Console 才會回傳 undefined

---

### 哪些是常見的表達式？

- 純值 ( 一個數字 1 也可以稱為「表達式」)
- 變數
- 運算子
- 執行函式
- 正規表達式
- 函式表達式
- if 小括號內的條件 (condition) 是表達式

#### 範例說明

接下來看幾個程式碼範例，然後利用 Chrome 的開發者工具 Console 查看結果

在 Console 輸入 1，會回傳 1，`<・` 符號後面的 1 代表 Console 回傳的結果

![純值在 Console 會回傳結果](https://ithelp.ithome.com.tw/upload/images/20250519/20172694vMcUipV9Ih.png)

再來看看運算子 `===` 在 Console 中的結果，`1 === 1` 會回傳 `true` 的結果

![運算子計算結果也是表達式](https://ithelp.ithome.com.tw/upload/images/20250519/20172694A76HRFz2av.png)

以上兩個範例都會回傳結果，因此純值和運算子計算的結果都屬於表達式

接下來看看陳述式與表達式混合的範例，以下程式碼中，紅框區塊函式陳述式是陳述式，下面藍框區塊呼叫函式之後回傳了 `'我是函式'` 的結果，所以呼叫、執行函式為表達式

![陳述式與表達式混合](https://ithelp.ithome.com.tw/upload/images/20250519/20172694pc54DnLUnI.png)

- **簡單比喻一下陳述式與表達式**：陳述式就像只是在講一件要對方做的事，對方只要去做就好不用回應，表達式則像是在問對方問題，希望對方能夠給你回應

### 表達式運用情境

了解陳述式與表達是如何判斷對於閱讀技術文件會有很大的幫助，以前面提到的 if 小括號內的條件 (condition) 是表達式為例

假設需要知道 if...else 如何使用，在 [MDN 文件](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)會看見關於 if...else 說明引用如下：

```javascript
if (condition)
  statement1

// With an else clause
if (condition)
  statement1
else
  statement2
```

>condition：An expression that is considered to be either truthy or falsy

這邊可以說明有提到小括號內的 condition 是一個表達式，而它的結果會是真值或假值，那就可以放心的把任何表達式加入 condition 內，像這樣：

紅框內呼叫 fn 函式，回傳值為 true，所以會執行 if 大括號 `{}` 中的程式碼印出 `'恭喜通關！'`

![ condition 是表達式](https://ithelp.ithome.com.tw/upload/images/20250519/20172694Oka1pbliOB.png)

這時候就會想實驗看看，把陳述式放入 condition，會發生什麼事 ~~(跟你說要放表達式竟然不聽話)~~

結果就是會跳出 SyntaxError 的錯誤訊息，把陳述式放入 condition 會造成運作上的錯誤，還是乖乖聽話吧 ~

![把陳述式放入 condition 的錯誤訊息](https://ithelp.ithome.com.tw/upload/images/20250519/20172694eOlxHlhL7P.png)

除了 if 的 condition 之外，還有一些框架使用上會需要了解表達式的概念，像是 React 的 JSX 就有提到大括號 `{}` 中可以放入 JavaScript 的表達式來運作

---

## 函式陳述式與函式表達式

前篇有提到這兩者一樣是宣告函式，但是不同語句的差異，遇到提升時卻有不同的運作方式，這篇剛好介紹到了陳述式與表達式 ~~真巧呀~~，那就再分別對這兩種宣告函式的語句做一些介紹吧 ~

### 函式陳述式

首先 function 和 var 一樣是關鍵字，可以用來宣告一個函式，而以下範例的宣告方式就屬於陳述式語句

```javascript
function fn() {
  return true;
}
```

陳述式不會回傳值，所以 Console 只會回傳 undefined 的結果

![函式陳述式不會回傳值](https://ithelp.ithome.com.tw/upload/images/20250519/20172694WGJJ56uGXs.png)

而相同寫法只要在前後加上小括號，就會從陳述式轉變為表達式，這邊可以看到前後加上小括號後，Console 會回傳這個函式本身的結構，此時的函式可稱為「函式表達式」

![陳述式轉變為表達式的回傳結果](https://ithelp.ithome.com.tw/upload/images/20250519/20172694RX8ZErFckf.png)

### 函式表達式

前面提到把函式本身作為表達式使用，回傳的值會是函式的本身，那麼如果我們將這個值 ( 函式本身 ) 賦予到一個變數上，那它就會成為大家所說的「函式表達式」

將函式表達式回傳的函式賦予給等號 `=` 左邊的變數

```javascript
var fn = function fn() {
  return true;
}
```

延伸討論剛剛提到的 if 小括號內的 condition 必須是表達式，那如果把函式陳述式語句直接放入小括號中 ( 如下 )，程式碼是否還可以運作呢？

```javascript
if (function a(p) {}){
  console.log('ㄟ嘿！我可以動！');
}
```

這邊雖然小括號中的語句看起來是函式陳述式，但是實際上是作為表達式使用，就像前面陳述式前後加小括號轉為表達式一樣，所以程式碼式能正常運作的，而表達式回傳的函式本身會報判斷為真值，所以 `console.log` 也可以執行喔 ~ ~~看它可以動多開心~~

![函式陳述式放入 if 小括號內可以正常運作](https://ithelp.ithome.com.tw/upload/images/20250519/20172694pJFvUcID8X.png)

### 具名函式與匿名函式

既然都講到以上兩種函式的宣告語句差異了，那就來接著往下講講函式命名問題吧 ~

顧名思義，具名函式是有名字的函式，而匿名函式則沒有名字，函式有沒有名字在函式陳述式和函式表達式兩種語句上也有差異

- **函式陳述式** ：宣告的函式一定要有名字
- **函式表達式** ：宣告的函式有沒有名字都可以

接下來看範例比較一下兩者

```javascript
// 函式陳述式
// function 後方有名字 fn1，這稱為具名函式
function fn1() {
  return true;
}

// 函式表達式
// function 後方沒有名字，因此稱為匿名函式
var fn2 = function() {
  return true;
}
```

函式表達式其實也可以在 function 後面加上函式的具名名稱

```javascript
// function 後方的 callMe 是函式的名稱
var fn2 = function callMe() {
  return true;
}
```

但是以上範例的 callMe 這個名稱無法在外部被取得，只能透過變數 fn2 回傳值的方式，或是在 fn2 函式內才能取得

圖中可以看見紅框處執行 fn2 函式後式可以取得 callMe 這個名稱的，黃框處直接輸入變數名稱 fn2，也可以取得 callMe 這個名稱，但是綠框處試圖在外部取得 callMe，卻跳出 ReferenceError 錯誤，無法取得 callMe 這個名稱

![callMe 名稱無法被外部取得](https://ithelp.ithome.com.tw/upload/images/20250519/20172694EJbzF2WXbJ.png)

雖然具名的函式表達式名稱，可以在函式內被呼叫，但實戰上不太會有呼叫此函式的需求，所以不太會這樣做

## 結語

以上是一些關於陳述式與表達式的差異介紹，如果想在更深入了解陳述式及表達式的分類也可以參考以下相關的 MDN 文件：

- [陳述式與宣告 - Statements and declarations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements)
- [運算式與運算子 - Expressions and operators](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators)

下篇會再接續本篇，往後介紹運算子執行先後順序的相關內容，那我們就下篇文章件囉 ~
