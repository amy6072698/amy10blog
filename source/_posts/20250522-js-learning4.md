---
title: JavaScript 修練 (4) | 型別判斷與原始型別包裹物件
date: 2025-05-22 16:21:54
categories: 
  - JavaScript
tags:
  - JavaScript
  - 前端
description: 本篇將介紹強型別與弱型別的基本概念，及 JavaScript 型別判斷方式，還有原始型別包裹物件的相關內容
---

## 強型別與弱型別

開始介紹 JavaScript 中型別有哪些和判斷的方式之前，我想先介紹一些強型別與弱型別的基礎知識，程式語言中依語言型別系統 ( Type system ) 分成「**強型別語言**」與「**弱型別語言**」兩種

- **強型別**：程式所定義的變數型別等於變數在執行時的型別，在宣告變數時必須指定一種資料型別給它
- **弱型別**：不需要在宣告變數時指定資料型別，雖語法較簡潔，但要注意型別轉換所產生的非預期結果

### JavaScript 是弱型別語言

那麼 JavaScript 經過前幾篇文章的程式碼，可以很明顯發現宣告變數時只是直接賦予值，就開始使用這個變數了，並不需要指定資料型別給變數，所以我們可以知道 JavaScript 屬於「**弱型別**」語言

可是不需要指定型別，JavaScript 的型別是怎麼來的？JavaScript 的型別只在值本身，而非透過變數帶來資料型別的資訊，也就是說「**變數沒有型別，值才有**」

不用指定型別不是少一件事要做，也挺好的不是嗎？但是 JavaScript 沒有這麼單純，它的型別不是固定不變的，你可以透過一些方式讓變數的值轉換型別，這對於習慣撰寫強型別語言的開發者來說，簡直就是災難 ~~調皮的 JavaScript~~

這表示如果不熟悉 JavaScript 型別轉換背後的規則，將可能在執行程式碼時產生不如預期的結果，至於哪些情況會讓型別發生轉換，就是這篇文章將提到的主要內容

## JavaScript 的型別與判斷

在開始說明型別轉換之前，首先要先認識 JavaScript 有哪些型別，JavaScript 的型別主要區分為兩大類：「原始型別」( Primitives，也稱為基本型別 ) 與「物件型別」( Object )

### 原始型別

以下七種型別屬於原始型別，這邊就不細說每個型別的特徵，只專注在介紹型別判斷的內容，若想深入了解每個型別可以參考 [MDN 的文件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Data_structures#%E8%B3%87%E6%96%99%E5%9E%8B%E5%88%A5)

- String ( 字串 )
- Number ( 數值 )
- Boolean ( 布林 )
- Undefined
- Null
- BigInt
- Symbol

### 物件型別

Object：不屬於原始型別的，都屬於物件型別

🔮**只要不屬於原始型別，就會被歸類為「物件型別」**，所以沒有什麼陣列型別或函式型別，不是原始型別就是物件型別

### 判斷型別的方式

想知道一個值屬於原始型別還是物件型別，只需要記得一個重點「**物件型別可以自由新增屬性，但是原始型別不行**」，接下來看看幾個範例

#### 物件型別可以自由新增屬性

物件、陣列、函式屬於物件型別，試著新增屬性

- **物件**：物件本身就有新增屬性的功能，印出 person 物件可以看見新增的 name 屬性，也能夠存取到物件內的 name 屬性值為 `'小夏'`

  ```javascript
  const person = {};
  person.name = "小夏";
  console.log(person);  // {name: '小夏'}
  console.log(person.name);  // 小夏
  ```

- **陣列**：雖然根據印出結果可以看見陣列內確實有新增的 name 屬性，可以運作，但實戰中請不要這樣做，陣列有它自己的運作方法，這樣奇怪的結構可能會造成一些操作問題

  ```javascript
  const arr = [];
  arr.name = "可愛的陣列列";
  arr.push(1);
  console.log(arr);  // [1, name: '可愛的陣列列']
  console.log(arr.name);  // 可愛的陣列列
  ```

  ![陣列也可以新增屬性](https://ithelp.ithome.com.tw/upload/images/20250531/20172694ppvyED8V6z.png)

- **函式**：因為函式本身已經有 name 屬性了，為了不覆蓋它，改為新增 myName 屬性，可以用 `console.log` 取得屬性值，但是看不見 fn 函式裡面的內容，所以要改用 `console.dir`，強制它使用物件結構展示，就可以看到 fn 函式變成一個可展開的物件，展開後可以看見裡面有剛新增的 myName 屬性

  ```javascript
  const fn = function() {};
  fn.myName = "小春";
  console.log(fn.myName);  // 小春
  console.log(fn);  // ƒ () {}
  console.dir(fn);  // 下拉展開可以看到 myName 屬性
  ```

  ![下拉展開可以看到 myName 屬性](https://ithelp.ithome.com.tw/upload/images/20250531/20172694Tl5oWJPosS.png)

#### 原始型別無法新增屬性

相反的，原始型別無法新增屬性，以下方原始型別中的 number 數值型別來說，新增屬性不會跳錯，但是無法取得 myName 的值，而且無論用 `console.log`、`console.dir` 都只會印出數值 1

```javascript!
let num = 1;
num.myName = "我是數字 1";
console.log(num.myName);  // undefined
console.log(num);  // 1
console.dir(num);  // 1
```

![number 型別無法取得 myName 的屬性值](https://ithelp.ithome.com.tw/upload/images/20250531/20172694wxjGqTdF7n.png)

🔮如果試圖在 null、undefined 內新增屬性，會跳出 TypeError 的錯誤

![在 null、undefined 內新增屬性跳出 TypeError](https://ithelp.ithome.com.tw/upload/images/20250531/20172694Q6eGSYvXhw.png)

#### typeof 的例外

相信講到判斷型別，一定會有人第一時間想到前篇提到的一元運算子 `typeof`，沒錯！它會回傳運算元的型別，但是有一些例外狀況

```javascript
// 原始型別
console.log(typeof "沒騙你！我是字串");  // string
console.log(typeof 1);  // number
console.log(typeof true);  // boolean
console.log(typeof undefined);  // undefined
console.log(typeof null);  // object
console.log(typeof 5n);  // bigint
console.log(typeof Symbol(1));  // symbol

// 物件型別
console.log(typeof {});  // object
console.log(typeof []);  // object
console.log(typeof function(){});  // function
console.log(typeof /1234/);  // object，正規表達式也是物件型別
```

觀察上方 `typeof` 程式碼，你就會發現 `null` 和 `function` 怪怪的，怎麼不是顯示我們預期的 null 跟 object

- **null**

  `typeof null` 為什麼是 `object`？ 其實它是一個過去就存在的 bug，曾經也有被討論要修改，但考慮到這會影響太多舊有的程式，所以就不修改了

  產生這個 bug 的原因，簡單來說就是在 JavaScript 初期的實作中，JavaScript 的值是由一個表示「型別」的標籤，與實際內容的「值」所組合成的

  但是由於物件 ( Object ) 這個型別的標籤是「0」，而且 null 代表的是空值 ( NULL pointer，慣例上會以 0x00 來表示 )，於是代表 null 的標籤與物件的標籤搞混了，就產生了這樣的錯誤結果

  如果想了解更多 typeof null 的內容可以參考這篇文章：[Null and typeof](https://javascriptrefined.io/null-and-typeof-9330e475d272)

- **function**

  再來說說函式，嚴格來說「函式是一個函式物件」，`typeof function(){ }` 回傳的是 `function`，但實際上仍然是屬於「物件型別」，前面也驗證過物件型別能新增屬性，而函式也可以，只是與一般物件不同的是，函式多了可以被呼叫 ( be invoked ) 的功能

  而 [ECMAScript](https://262.ecma-international.org/5.1/#sec-4.3.24) 對於 function 的定義也可以作為參考

  ![ECMAScript 對於 function 的定義](https://ithelp.ithome.com.tw/upload/images/20250531/20172694FGXJ7wurX0.png)

## 原始型別包裹物件

之後的文章會介紹一些型別轉換的內容，而其中會需要一些「原始型別包裹物件」( Primitive Wrapper Objects ) 的相關知識，所以加入在本篇文章介紹，原始型別中除了 undefined、null 之外，每個型別都有各自可以使用的方法 ( undefined、null 型別沒有包裹物件 )

如下範例，字串型別可以使用 `toUpperCase` 方法，將字串字母都轉為大寫，數值型別卻無法使用，可是字串是純值，不是物件、也不是函式，`toUpperCase` 方法又是從哪裡來的呢？

```javascript
let str = 'i am amy';
console.log(str.toUpperCase());  // I AM AMY
```

```javascript
// 數值型別沒有 toUpperCase 這個方法，試圖使用會跳出錯誤
let num = 1;
console.log(num.toUpperCase());  // Uncaught TypeError: num.toUpperCase is not a function
```

**原始型別的方法來自於「原始型別包裹物件」**，建立一個純值時，就會套用與該值型別對應的包裹物件，因此純值就能使用包裹物件中的方法了

以剛剛的 `toUpperCase` 方法為例，就可以在 String 包裹物件中找到這個方法，使用 `console.dir` 印出 String 這個包裹物件，展開一個叫 `prototype` 的物件

![展開 String 的 prototype 物件](https://ithelp.ithome.com.tw/upload/images/20250531/20172694xFFX56y3KJ.png)

往下尋找就可以找到 String 包裹物件中的 `toUpperCase` 方法

![String 中的 toUpperCase 方法](https://ithelp.ithome.com.tw/upload/images/20250531/20172694yIxdwRzLyO.png)

同理，數值和布林型別也有各自的包裹物件：Number、Boolean，同樣也可以試著用 `console.dir(Number);` 查看數值型別的包裹物件中有哪些方法，這邊就交給大家嘗試做做看囉 ~

### 原始型別包裹物件可用來轉換型別

而包裹物件其實也是一個可以被直接呼叫的函式，實戰中也會使用它來做型別的轉換，如以下範例，String 作為函式可以將傳入的值轉換成字串型別的值，所以轉型後的值能使用 String 中的 length 方法來查看字串的長度

```javascript
const str = String(123);
console.log(str.length);  // 3
```

### 不要把原始型別包裹物件作為函式建構子使用

以 String 來說，雖然可以使用 new 運算子來建構「字串」，但是這會造成所謂的「字串」變成物件，而這個物件會同時包含包裹物件的所有方法

直接看看用 new 運算子結合 String 包裹物件建立字串，會發生什麼事：印出結果都會明示或暗示你，你建立的字串變成物件了，所以要避免用這種方式來建立原始型別的值

```javascript
let str = new String('I am Amy');  // str 會是一個物件
let str2 = new String('I am Amy');  // str2 會是另一個物件

console.log(typeof str);  // object
console.log(str == str2);  // false

str.myName = '我是字串';
console.log(str);  // String {'I am Amy', myName: '我是字串'}
console.log(str2);  // String {'I am Amy'}
```

📎**補充**：BigInt、Symbol 僅能作為函式，無法作為函式建構子使用，若試圖這樣做，會跳出 TypeError 的錯誤如下圖

![BigInt、Symbol 無法作為函式建構子使用](https://ithelp.ithome.com.tw/upload/images/20250531/20172694CUGxj5ffuL.png)

## 結語

本篇文章簡單介紹了強型別與弱型別的基本概念，以及 JavaScript 中型別有哪些、型別判斷的方式和 typeof 的例外，最後介紹一些與原始型別包裹物件有關的內容，原始型別包裹物件在後面的文章也會出現，本篇文章算是建立一些基本知識，為接下來會往下介紹型別轉換時做鋪墊

那我們就下篇文章見囉 ~
