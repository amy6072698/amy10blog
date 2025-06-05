---
title: JavaScript 修練 (5) | 型別的顯性與隱性轉換
date: 2025-05-23 20:30:13
categories: 
  - JavaScript
tags:
  - JavaScript
  - 前端
description: 本篇將介紹型別的顯性轉換及隱性轉換，各種轉換型別的方式及規則
---

## 轉到你會暈的動態型別

前篇提到 JavaScript 的型別不是固定不變的，所以我們可以把字串型別的值賦予在一個變數上，然後重新賦予該變數一個數值型別的值，覆蓋原本的型別，程式在運作時，型別會自動轉換，這也代表我們可以**以不同的型別使用同一個變數**，而這就稱為「動態型別」

那麼有靜態型別嗎？有的，像 Java 這種編譯式語言，會先經過編譯後才會執行，在**編譯期間會執行型別檢查，確保型別不會在執行時變更**，增加程式運作的穩定性，這類就稱為「**靜態型別**」

而 JavaScript 屬於直譯式語言，原始碼是由直譯器生成代碼並執行，過程中不會檢查型別，且會在**執行過程中動態變更資料型別**，因此稱為「**動態型別**」

前篇也有提到 **JavaScript 的變數沒有型別，值才有**，因此變數隨著值的變更，也會同時變更型別，而除了直接重新賦予值之外，也可透過一些方式讓型別轉換

而轉換方式的類型又分為「**顯性轉換**」( Explicit Conversion ) 和「**隱性轉換**」( Implicit Conversion )，這兩者看名字可以知道顯性是使用較明確的方式進行型別轉換，而隱性則是使用其他較不明顯的方式進行轉換，有些隱性轉換手法雖然不明顯無法直接看出轉換原因但是卻很簡短，所以對 JS 較熟練的開發者，也可能因此使用較隱性的方式轉換型別

只是 JavaScript 規範中，並沒明確描述顯性及隱性的定義，所以何謂顯性、何謂隱性各開發者主觀的認定可能會略有不同，不過大致會以普遍的認知來區別兩者差異，接下來就以「顯性轉換」和「隱性轉換」，來分別介紹 JavaScript 有哪些轉換手法吧 ~

## 顯性轉換

### 原始型別包裹物件及原型方法

#### 原始型別包裹物件

前篇文章提到原始型別包裹物件本身，也可以做為型別轉換的方法使用，其中除了沒有原始型別包裹物件的 null、undefined 之外，Number、String、Boolean、BigInt、Symbol 皆可作為轉換型別使用

```javascript
let produceId = '111';  // produceId 為字串型別
let price = 100;  // price 為數值型別

// 將 produceId 轉為數值型別
console.log(Number(produceId));  // 111
console.log(typeof Number(produceId));  // number

// 將 price 轉為其他型別
console.log(String(price));  // '100'
console.log(typeof String(price));  // string

console.log(Boolean(price));  // true
console.log(typeof Boolean(price));  // boolean

console.log(BigInt(price));  // 100n
console.log(typeof BigInt(price));  // bigint

console.log(Symbol(price));  // Symbol(100)
console.log(typeof Symbol(price));  // symbol
```

#### 原型方法

前篇也有提到使用 console.dir 印出原始型別包裹物件後，可以在 prototype 這個物件中查看可以使用的方法，而這些原型方法中也有可以轉換型別的方法，如下圖在 Number 包裹物件中展開 prototype 可以找到 `toString()` 方法

![Number 中的 toString 方法](https://ithelp.ithome.com.tw/upload/images/20250531/20172694wyDF1QieeD.png)

 `toString()` 方法可以將不同型別的值轉為字串型別

```javascript
// Number 裡面的 prototype 有 toString 這個方法
console.dir(Number);

let price = 100;  // price 為數值型別

console.log(price.toString());  // '100'
console.log(typeof price.toString());  // string
```

但是 null、undefined 這兩個型別，因為沒有原始型別包裹物件，無法使用 `toString()` 方法轉型為字串型別，所以 `String()` 相對於未知型別轉換是較穩定的，`toString()` 遇到特定型別可能會出現錯誤訊息 ( 如下 )

```javascript
// undefined 沒有 toString 方法可用，所以會跳出錯誤
console.log(undefined.toString());   // VM1630:1 Uncaught TypeError: Cannot read properties of undefined (reading 'toString')

// String() 方法可以將 undefined 轉為字串型別，不會跳錯
console.log(String(undefined));  // 'undefined'
```

---

📎**補充數值型別轉換**

除了使用 Number 包裹物件之外，還可以用 `parseInt()` 方法將不同型別的值轉為數值型別，只是兩者轉換上有一些差異，如果要將混有數字跟其他字元的字串轉為數值，`Number()` 會轉為 NaN ( Not a Number ) 的數值型別結果，但是 `parseInt()` 則可以將其中的數字轉換為數值型別，範例如下

```javascript
console.log(Number('100元'));  // NaN
console.log(Number.parseInt('100元'));  // 100
```

在全域 window 物件中也有 parseInt 方法，且跟 Number 下的 parseInt 方法一樣，所以省略 parseInt 前面的 Number 也可以運作

```javascript
console.log(window.parseInt === Number.parseInt);  // true，兩者相同
console.log(parseInt('100元'));  // 100
```

Number 下的 parseInt 方法

![Number 下的 parseInt 方法](https://ithelp.ithome.com.tw/upload/images/20250531/20172694a9TZ5OWMMV.png)

`parseInt()` 方法是將數值轉為整數，有小數點會直接被去除，所以如果數值有包含小數點，請改用 `parseFloat()` 進行轉換

```javascript
let str = '20.6元'
console.log(parseInt(str));  // 20
console.log(parseFloat(str));  // 20.6
```

---

### 正負運算子 `+`  `-`

這裡的 `+`、`-` 是一元運算子，不是計算左右兩個運算元的二元運算子，更像是數學上用於表示正負值的用法，而不是用於計算結果

在想轉換的值前方加上 `+` 或 `-`，可以將值轉換為數值型別，只是如果字串中含有非數字的字元，就會轉為 NaN，所以相對來說使用 `parseInt()` 是更穩定的轉數值方法

```javascript
console.log(typeof(+'1'));  // number
console.log(+true);  // 1
console.log(+'50元');  // NaN
console.log(-'50元');  // NaN
console.log(typeof(+'50元'));  // number，NaN 也是 number 型別
```

📎**注意**：以上轉換數值型別的方式，指的是一元運算子的 `+` 跟 `-`，以下範例第一行的 `+` 是二元運算子 ( 這裡的運作之後會提到 )

```javascript
// 二元運算子
console.log(1 + '1');  // '11'
console.log(typeof(1 + '1'));  // string

// 要正確轉為數值計算，需要在要轉換的字串前補上 +
console.log(1 + +'1');  // 2
```

---

### 邏輯運算子 NOT `!`

要將不同型別轉換為布林值，可以使用前面提到的包裹物件 `Boolean()` 來進行轉換，它可以將「真值」轉為 true，「假值」轉為 false ( 什麼是真值、假值後面會提到 )

但也可以使用更簡單的方式進行轉換，那就是使用邏輯運算子 Not `!`，`!` 運算子會將值轉為相反的布林值，也就是原本是真值會轉換成 false，原本是假值會轉換成 true

```javascript
console.log(!true);  // false
console.log(!false);  // true
console.log(!0);  // true
```

那麼聰明的你一定想到了，如果在前面再加上一個 `!`，`!!` ~~雙重驚嘆~~ 是不是就可以讓不同型別的值轉換成原本的布林值了呢？沒錯，所以有時候在實戰上會使用兩個 Not `!!`，來將值轉換成布林值，示範如下

```javascript
console.log(!!'1');  // true
console.log(Boolean('1'));  // true
```

---

## 隱性轉換

### 二元運算子的 `+`

在顯性轉換時有提到，`+` 作為一元運算子 ( 正負運算子 ) 使用時，會將運算元轉換為數值型別，而這裡要講的是二元運算子的 `+`，有兩種用途：

一種是作為「算術運算子」，用來計算數值 ( 算術運算子不只有 `+`，後面還會介紹其他 算術運算子)；另一種是作為「字串運算子」，用來連接字串，可以用以下三個規則判斷 `+` 是屬於哪種用途：

- 規則一：前後運算元如果其中之一為「字串」型別，`+` 視為字串運算子
- 規則二：前後運算元如果其中之一為「物件」型別，`+` 視為字串運算子
- 規則三：上述情況以外，`+` 視為算術運算子

簡單總結就是「**當前後運算元，其一為字串或物件型別時，`+` 為字串運算子**」

---

#### 1. 字串運算子的 `+`

當符合規則一、二，`+` 被視為字串運算子時，會先將前後運算元轉型為字串，再將兩個字串連接起來，示範如下

```javascript
// 符合規則一：運算元其一為字串型別
console.log(1 + '1');  // '11'

// 符合規則二：運算元其一為物件型別
// [] 轉字串為空字串 ''
console.log(1 + []);  // '1'
console.log(1 + {});  // '1[object Object]'
console.log(1 + function(){});  // '1function(){}'
```

📎**補充物件型別轉字串**：物件型別中陣列、物件、函式套用 `toString()` 轉為字串型別的結果如下方範例

```javascript
// [1, 2] 套用 toString() 轉字串結果為 '1,2'
console.log(1 + [1, 2]);  // '11,2'

// 任何物件套用 toString() 轉字串結果都是 '[object Object]'
console.log(1 + {a: 1});  // '1[object Object]'

// function(){return 1;} 套用 toString() 轉字串結果為函式本身 '1function(){return 1;}'
console.log(1 + function(){return 1;});  // '1function(){return 1;}'
```

---

#### 2. 算術運算子的 `+`

當不符合規則一、二，也就是前後運算元為非字串的原始型別時，`+` 為算術運算子，這時會套用 `Number()` 將前後運算元轉為數值型別，再進行計算相加 ( 如下範例 )

```javascript
// 前後為數值計算相加結果為 3
console.log(1 + 2);  // 3

// 布林值 true 轉為數值是 1，false 則為 0
console.log(1 + true);  // 2
console.log(false + 2);  // 2

// undefined 轉為數值是 NaN，NaN 跟任何數值計算都是 NaN
console.log(1 + undefined);  // NaN

// null 轉為數值是 0
console.log(1 + null);  // 1

console.log(null + null);  // 0
console.log(null + undefined);  // NaN
```

#### BigInt 和 Symbol 型別

然後你應該會發現上面算術運算子範例，少了原始型別的 BigInt 和 Symbol，沒錯，因為它們比較特殊，會出現例外狀況所以要另外說

- **BigInt 型別**

  當 `+` 為字串運算子時，BigInt 一樣會轉成字串再連接
  
  ```javascript
  // 符合規則一：運算元其一為字串型別
  // 1n 轉為字串是 '1'
  console.log(1n + '1');  // '11'

  // 符合規則二：運算元其一為物件型別
  console.log(1n + []);  // '1'
  console.log(1n + {});  // '1[object Object]'
  console.log(1n + function(){});  // '1function(){}'
  ```

  但是當遇到算術運算子時 ( `+` 以外的算術運算子也是 )，BigInt 不會隱性轉換為數值型別，而是會跳出 TypeError 錯誤，提示 BigInt 無法和其他型別混合使用，需要另外用顯性轉換方式轉型
  
  ![BigInt 無法和其他型別做計算](https://ithelp.ithome.com.tw/upload/images/20250531/201726941CLAE98h50.png)

- **Symbol 型別**
  
  Symbol 型別則是無論 `+` 是不是算術運算子，都不能用這種方式隱性轉型，值得一提的是，`+` 是字串運算子和 `+` 是算術運算子，跳出的 TypeError 錯誤提示會不太一樣
  
  當 `+` 為字串運算子時，會出現無法轉為字串型別的錯誤提示；`+` 為算術運算子時，則會出現無法轉為數值型別的錯誤提示，而這剛好可以驗證 + 的用途
  
  如下圖黃框處錯誤提示是無法轉為 number，可以驗證 `+` 為算術運算子，紅框處錯誤提示是無法轉為 string，可以驗證 `+` 是字串運算子
  
  ![Symbol 型別驗證 + 的用途](https://ithelp.ithome.com.tw/upload/images/20250531/201726941wY49nk6GP.png)

  📎補充：Symbol 型別可以轉型成字串、布林，但是不能轉成數值型別
  
  ![Symbol 型別不能轉為數值型別](https://ithelp.ithome.com.tw/upload/images/20250531/201726943I4XYC51yn.png)

---

### 算術運算子 `-`、`*`、`/`

講完比較特殊的 `+` 之後，前面也有說到算術運算子其實不只有 `+`，還有 `-`、`*`、`/`，用起來就和數學四則運算一樣，可以做加減乘除計算

算術運算子會將前後運算元套用 `Number()` 轉型為數值型別，再做計算

```javascript
console.log(100 - 50);  // 50

// 空字串轉數值為 0
console.log(100 - '');  // 100
console.log(100 - '50');  // 50

// 布林值 true 轉為數值是 1，false 則為 0
console.log(100 - true);  // 99
console.log(false - 50);  // -50

// undefined 轉為數值是 NaN，NaN 跟任何數值計算都是 NaN
console.log(100 - undefined);  // NaN

// null 轉為數值是 0
console.log(50 - null);  // 50

console.log(null - null);  // 0
console.log(null - undefined);  // NaN

// *、/ 也一樣會轉型為數值型別，再做計算
console.log('100' * null);  // 0
console.log(50 / true);  // 50
```

**`+` 必須不是字串運算子**，才會套用 `Number()` 將運算元轉為數值型別後計算

```javascript
console.log(1 + '1');  // '11'
console.log(typeof(1 + '1'));  // string

console.log(1 - '1');  // 0
console.log(typeof(1 - '1'));  // number
```

#### 物件型別轉為數值型別

物件型別轉型為數值型別的過程，會先用 `toString()` 轉型為字串，再用 `Number()` 轉型為數值，如果字串中有非數字字元就會是 NaN，而 NaN 跟任何數值計算都是 NaN

```javascript
// 陣列 [100, 1] 轉為字串是 '100,1'，轉成數值是 NaN
console.log([100, 1].toString());  // '100,1'
console.log(Number([100, 1].toString()));  // NaN
console.log([100, 1] * 100);  // NaN

// 陣列 [100] 轉為字串是 '100'，轉成數值是 100
console.log([100].toString());  // '100'
console.log(Number([100].toString()));  // 100
console.log([100] * 100);  // 10000

// 任何物件轉為字串都是 '[object Object]'，轉成數值是 NaN
console.log({} * 100);  // NaN

// 以下函式為字串是 'function fn(){return 1}'，轉成數值是 NaN
console.log(function fn(){return 1} * 100);  // NaN
```

#### 例外狀況

這邊例外狀況前面有稍微提到，就是 BigInt 和 Symbol 這兩個型別，BigInt 型別不能和其他型別混合計算，若 BigInt 型別要與數值型別計算，要先把 BigInt 轉成數值型別再計算，才不會跳錯，而 Symbol 型別則是無法用這種方式隱性轉型再計算

```javascript
// BigInt 型別不能和其他型別計算，僅能與 BigInt 型別計算
console.log(1n * 100);  // Uncaught TypeError: Cannot mix BigInt and other types, use explicit conversions
console.log(1n * 100n);  // 100n

// 若要與數值型別計算，BigInt 要先顯性轉型成數值再計算
console.log((Number(1n)) * 100);  // 100

// Symbol 型別無法用這種方式隱性轉型再計算
console.log(100 * Symbol(1));  // Uncaught TypeError: Cannot convert a Symbol value to a number
```

## 結語

本篇文章介紹了 JavaScript 在型別轉換分成顯性及隱性轉換，也分別針對兩種轉換介紹了各種轉換型別的方式及規則，希望下次在遇到型別轉換時，大家都能更了解背後的規則

那我們就下篇文章見囉 ~
