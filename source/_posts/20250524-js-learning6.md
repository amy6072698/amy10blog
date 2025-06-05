---
title: JavaScript 修練 (6) | 比較時的型別轉換與真值假值
date: 2025-05-24 19:24:42
categories: 
  - JavaScript
tags:
  - JavaScript
  - 前端
description: 本篇將介紹嚴格相等與寬鬆相等、真值與假值，及寬鬆相等比較時型別的轉換規則，真值與假值的實戰應用
---

## 前置知識

前篇文章講了很多情況的型別轉換，而在比較時的型別轉換又是不同的規則，開始講解規則之前先介紹一些基礎知識：嚴格相等與寬鬆相等、真值與假值

- **嚴格相等與寬鬆相等**

  兩種相等的運算子符號差在等號數量，實戰中會建議使用三個等號 `===`，避免不如預期的結果，從以下兩者介紹中寬鬆相等 `==` 不用連型別都一樣，那麼前後運算元型別不同要如何比較呢？寬鬆相等會比較轉型後的結果，比較時的型別轉換規則就從這裡展開

  - **嚴格相等 `===`**：值與型別，完全相等才能回傳 true，對應的不相等符號是 `!==`
  - **寬鬆相等 `==`**：值相等就回傳 true，型別不需要相等，對應的不相等符號是 `!=`

- **真值與假值**

  在 JavaScript 中，任何值用 Boolean 轉換型別的結果，不是 true 就是 false，所以可以把 JavaScript 中的值分成兩種「值」：[真值](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)、[假值](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy)

  - **假值 ( falsy )**：轉換為布林後會變成 `false` 的值
  - **真值 ( truthy )**：其他會變成 `true` 的值

  真值很多，所以只要**記假值就好，除假值之外其他都是真值**，以下是 MDN 整理的假值表格

  ![假值表格](https://ithelp.ithome.com.tw/upload/images/20250531/20172694UAZNAFSveU.png)

講完一些基礎知識之後，接下來就分別來介紹嚴格相等和寬鬆相等比較，以及真值假值的相關內容吧 ~

## 嚴格相等 `===`

嚴格相等比寬鬆相等更單純，值和型別都相等才能回傳 `true`，但是還是有一些容易搞混的嚴格相等範例

```javascript
// 以下結果為 false
console.log(NaN === NaN);  // 因為 NaN 不等於 NaN
console.log(undefined === null);  // 這是兩個不同的型別
console.log({} === {});  // 左邊的物件實體和右邊的物件實體不是同一個實體
console.log([] === []);  // 左邊的陣列實體和右邊的陣列實體不是同一個實體
console.log(new Number(0) === new Number(0));  // 前篇說過這樣建立的 number 會變成物件型別，所以左右是兩個不同的實體

// 以下結果為 true
console.log(+0 === -0);
```

📎**補充 NaN 特性**：NaN ( Not a Number) 雖然不是數字，但是它的型別是 Number 型別，NaN 不等於任何值，包括它自己 ( 三個等號跟二個等號都不相等 )，NaN 跟任何數值計算都是 NaN ~~一直覺得 NaN 很像病毒，它會傳染耶~~

## 寬鬆相等 `==`

寬鬆相等的規則就比較複雜，前面有提到寬鬆相等只要值相等就可以回傳 `true`，前後運算元的型別不同時，就會比較轉型後的結果，而其中每種型別轉換比較的規則都不大一樣

### Number、String、Boolean 型別

這三者之間在進行寬鬆相等的比對時，通通都會轉為 Number 型別再比較，如：

```javascript
console.log(Number('a'));  // NaN

// NaN 等於任何值也不等於自己
console.log('a' == true);  // false
console.log('a' == false);  // false

console.log('a' == 1);  // false

// 其他混合比較
console.log('1' == true);  // true
console.log(1 == '1');  // true
console.log('0' == false);  // true
```

### Null、Undefined 型別

這兩者進行寬鬆相等的比對時幾乎不會轉型，null 和 undefined 除了跟自己相比，或兩者彼此相比結果是 true 之外，其他結果都為 false

```javascript
console.log(null == 0);  // false
console.log(null == '');  // false
console.log(null == false);  // false

console.log(undefined == 0);  // false
console.log(undefined == '');  // false
console.log(undefined == false);  // false

console.log(null == undefined);  // true
console.log(null == null);  // true
console.log(undefined == undefined);  // true
```

### BigInt 型別

任何值與 BigInt 型別進行寬鬆相等的比對時，都會轉型為「數學值」( mathematical value )，這裡說的數學值並不是指 Number 型別的值，實際比較時也可以理解為「和 BigInt 型別比較的值會轉型為 BigInt」，而與 Number 型別的值相比數學值具有以下特性：

- 沒有 NaN
- 沒有小數點
- 沒有最大值

除以上三點，數學值的其它概念與 Number 型別的值接近

上面有提到最大值的概念，Number 型別其實有最大安全值，在 Number 包裹物件中的 MAX_SAFE_INTEGER 這個屬性就可以查看該值，當大於這個值計算精準度就會下降

![MAX_SAFE_INTEGER 的值](https://ithelp.ithome.com.tw/upload/images/20250531/20172694X0vjjatcVL.png)

```javascript
// Number 的最大安全值 MAX_SAFE_INTEGER
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991

// 單純用 Number 與 String 型別比較，會因為超出最大安全值而不精準
console.log(9007199254740991 == '9007199254740991'); // true
console.log(9007199254740993 == '9007199254740992'); // true

// 改用 BigInt 與 String 型別比較，不受最大安全值影響
console.log(9007199254740993n == '9007199254740992'); // false
console.log(9007199254740993n == '9007199254740993'); // true
```

遇到帶有小數點的 Number 型別值時，因為 BingInt 沒有小數點，所以結果會是 false，遇到 NaN 則因為 NaN 不等於任何值，所以結果為 false

```javascript
// Number 型別轉為 BingInt 型別比較
console.log(100 == 100n);  // true

// BingInt 沒有小數點
console.log(100.5 == 100n); // false

// NaN 不等於任何值
console.log(NaN == 100n); // false
```

### Symbol 型別

Symbol 型別建立的值是唯一的，運作有點類似物件的「傳參考」特性，所以一樣的值，無論嚴格或寬鬆相等比對結果都是 false

```javascript
// 類似物件與物件比對的運作
let s1 = Symbol(2);
let s2 = Symbol(2);
console.log(s1 == s2);  // false
console.log(s1 === s2);  // false

console.log(Symbol(2) == Symbol(2));  // false
console.log(Symbol(2) === Symbol(2));  // false
```

注意以下範例會得到 true 的結果，運作和物件與物件比對很相近，這邊實際上只有建立一個 Symbol，s1 和 s2 是共用同一個記憶體位置

```javascript=
// s1 和 s2 共用一個記憶體位置
let s1 = Symbol(2);
let s2 = s1;
console.log(s1 == s2);  // true
console.log(s1 === s2);  // true
```

---

### 物件型別與原始型別比較

前面提到 Symbol 型別比較的運作，很類似物件與物件比對的運作，會使用參考位置的方式比較，但物件型別與原始型別比較卻有不同規則，當物件型別與原始型別進行寬鬆相等比較時，JavaScript 會嘗試將物件型別轉換為與原始型別相同的型別，再進行比較

#### Number、String、BigInt 型別

物件型別與這三種原始型別比較時，物件型別會嘗試轉換為與原始型別相同的型別，可以想成是用包裹物件 Number、String、BigInt 進行型別轉換後，再進行比較，這邊會以陣列為主要範例

- **物件型別 vs Number 型別**：陣列 `[100]` 轉為 Number 型別是 `100`，所以結果為 true

  ```javascript
  console.log([100] == 100);  // true
  ```
  
- **物件型別 vs String 型別**：陣列 `['x', 'y']` 轉為 String 型別是 `'x,y'`，所以結果為 true，補充任何物件轉為 String 型別都是 `'[object Object]'`，所以 `{} == '[object Object]'` 結果為 true

  ```javascript
  console.log(['x', 'y'] == 'x,y');  // true

  // 任何物件轉為字串都是 '[object Object]'
  console.log({} == '[object Object]');  // true
  ```

- **物件型別 vs BigInt 型別**：陣列 `['100']` 和 `[100]` 轉為 BigInt 型別都是 `100n` ( 可以用 BigInt 包裹物件轉換型別查看結果 )，所以結果為 true

  ```javascript
  console.log(['100'] == 100n);  // true
  console.log([100] == 100n);  // true

  // BigInt 不受最大安全值影響
  console.log(['9007199254740992'] == 9007199254740993n); // false
  console.log(['9007199254740993'] == 9007199254740993n); // true
  ```

#### Null、Undefined

Null 或 Undefined 型別本身沒有對應的包裹物件，物件型別也就不會轉換成 Null 或 Undefined 型別，所以物件型別與 Null 或 Undefined 型別比較的結果為 false

```javascript
console.log([] == null);  // false
console.log({} == null);  // false

console.log([] == undefined);  // false
console.log({} == undefined);  // false
```

#### 例外情況

- **Boolean 型別**：物件型別與布林做比較，布林會轉為 Number 型別，物件型別也會轉為 Number 型別，再做比較

```javascript
// [] 轉為 Number 型別是 0，true 轉為 Number 型別是 1，false 則為 0
console.log([] == false);  // true
console.log([1] == true);  // true
console.log([2] == true);  // false

// {} 轉為 Number 型別是 NaN，NaN 不等於任何值
console.log({} == true);  // false
```

📎物件型別與 Symbol 型別進行比較時，不是結果為 `false`，就是拋出無法轉型的錯誤，因此不建議直接讓物件或陣列與 Symbol 進行比較，因為幾乎不會得到 `true`，反而容易出現錯誤

## 真值與假值的應用

真值與假值在實戰中，常會用於 if 判斷值是否存在、是否不為 0、是否不為 null 或 undefined，嚴格來說是判斷該值是否為「真值」，看看以下的範例應用

變數 `a` 有被賦予值 `'我是 a'`，所以 if 判斷 `'我是 a'` 為真值，所以會運行完整的陳述式，若變數 `a` 的值是 null 或 undefined，則不會執行 `console.log('可運行');` 這行程式碼

```javascript
let a = '我是 a';
if(a){
  console.log('可運行');  // '可運行'
}
```
  
空的陣列 `[]` 是真值，若希望陣列內沒東西要被視為假值，可以在陣列後加上 `.length`，當長度為 0 就為假值，也就不會運行完整的陳述式了

```javascript
// [] 是 true，console.log 會運行
if([]){
  console.log('可運行');  // '可運行'
}

// [].length 是 false，所以 console.log 不會運行
if([].length){
  console.log('可運行');
}
```

當然真值與假值在實戰中並不只限於 if，也有其他應用，像是搭配三元運算子或邏輯運算子 `&&`、`||` 來使用，接下來看幾個結合運算子的真值、假值應用範例

- **三元運算子**

  在 if 判斷式結構相對單純的情況下，可以改用三元運算子方式撰寫條件判斷的程式碼，能讓程式碼看起來更簡潔，增加閱讀性

  ```javascript
  // if 判斷式
  let message;
  let isLoggedIn = true;
  if(isLoggedin) {
    message = '歡迎回來！';
  } else {
    message = '請先登入';
  }
  console.log(message);
  ```

  ```javascript
  // 三元運算子
  let isLoggedIn = true;
  let message = isLoggedIn ? '歡迎回來！' : '請先登入';
  console.log(message);
  ```

- **邏輯運算子 AND `&&`**

  若要陣列有資料才執行程式，就可以用 `list.length` 取得陣列長度，再搭配邏輯運算子 `&&`，如果陣列中沒有資料，長度就會是被視為假值的 0，這時候就不會觸發 `&&` 後的 `console.log` 執行

  ```javascript
  const list1 = [];
  list1.length && console.log('有資料！');

  const list2 = [1, 2];
  list2.length && console.log('有資料！');  // '有資料！'
  ```

- **邏輯運算子 OR `||`**

  若函式沒有帶參數，則參數值為 undefined，這可能會影響函式內程式碼的運作，而透過搭配邏輯運算子 `||`，可以將被視為假值的 undefined 賦予一個預設值，避免錯誤

  ```javascript
  function fn(num){
    var newNumber = num || 100;  // 預設值 100
    console.log(newNumber);
  }
  fn();  // 100
  ```

### 補充「AND `&&`」和「OR `||`」

經過上方的範例可以發現運算子「AND `&&`」和「OR `||`」，雖然字面意思是「且」跟「或」，感覺好像應該要回傳 `true` 或 `false` 這樣的布林值

但在 JavaScript 中它們回傳的值**不一定是布林值**，而是**兩個運算元中的其中一個**

這兩個邏輯運算子都會**從左至右**檢查運算元的值，並將每個運算元**先轉為對應的布林值（truthy / falsy）進行邏輯判斷**，再決定要回傳哪個原始值：

- **`&&`（AND 運算子）**
    如果第一個運算元為 falsy，代表結果已經是 `false`，所以會**直接回傳第一個值**，不再判斷後面；否則會繼續判斷第二個值，並**回傳第二個值**

- **`||`（OR 運算子）**
    如果第一個運算元為 truthy，代表結果已經是 `true`，所以會**直接回傳第一個值**，不再判斷後面；否則會繼續判斷第二個值，並**回傳第二個值**

而這樣的機制稱為**短路求值（Short-circuit evaluation）**，正因為有這樣的機制，我們才能更簡潔地設定預設值、執行條件判斷的程式碼或避免錯誤

## 不是！你不是假值嗎？

前面有提到真值很多，所以只要**記假值就好，除假值之外其他都是真值**，但就是會遇到那種讓人誤會滿滿的值，開始看以下範例前，建議再好好看一下[假值的表格](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy)

```javascript
console.log(Boolean([]));  // true
console.log(Boolean({}));  // true
console.log(Boolean('0'));  // true
console.log(Boolean(' '));  // true
console.log(Boolean(new Number(0)));  // true
console.log(Boolean(new Boolean(false)));  // true
```

沒錯，以上結果都是 true，它們都是真值 ~~( 真到讓你懷疑人生 )~~，空陣列跟空物件仔細看表格就會發現它們不是假值，而字串除了空字串是假值之外，字串內有任何值 ( 包含空白字元 ) 就是真值，再來最後兩個用 new 運算子搭配包裹物件建立的原始型別值，會變成物件，所以很遺憾它們也是真值

## 結語

本篇文章介紹了嚴格相等、寬鬆相等，以及寬鬆相等比較時型別的轉換規則，最後也補充了真值與假值在實戰上的應用方式，型別轉換在 JavaScript 這門語言算是很重要的概念，理解轉換的規則在開發也能避開錯誤，希望大家看完三篇與型別相關的文章可以功力大增

那我們下篇文章見囉 ~
