---
title: 從零開始學 Hexo (10) | NexT 主題篇 - 客製化主題樣式
date: 2025-04-30 22:16:27
categories:
  - Hexo
tags: 
  - Hexo
  - 前端
description: 介紹 NexT 主題的 config 檔的客製化設定，及如何尋找程式碼的技巧
---

## NexT 主題官方文件

在客製化過程中，我蠻常參考 [NexT 主題官網](https://theme-next.js.org/)的，然後會有一些想調整的地方，其實 NexT 主題的 config 檔都有地方可以設定

所以在往更深的程式碼調整客製介紹之前，我想先針對 NexT 主題的 config 檔中，可以調整的內容做一些簡單介紹

## NexT 主題的 config 檔

接下來會介紹一些在 NexT 主題的 config 檔中，可以用來調整網站樣式的設定，為了避免重複說到檔案名字，先說明一下，以下提到的設定都是在 NexT 主題的 config 檔中修改的內容

### 開啟選單項目

NexT 主題的選單是需要自己設定開啟的，這邊的選單就很像是網站上方的導覽列，要調整選單要顯示什麼內容，就需要調整以下的 Menu Settings 區塊了

![Menu Settings 區塊](https://ithelp.ithome.com.tw/upload/images/20250519/2017269468IVyPHD69.png)

#### menu

首先，上方的 menu 可以控制選單要開啟哪些項目，以及調整項目對應的路由跟 icon

要開啟哪個項目，就刪除該項目開頭的井字號 `#` 解除註解，反之就加上井字號 `#` 註解掉，假設我想開啟前五個項目，就把前五項解除註解就可以了

```yaml
menu:
  home: / || fa fa-home
  about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  #schedule: /schedule/ || fa fa-calendar
  #sitemap: /sitemap.xml || fa fa-sitemap
  #commonweal: /404/ || fa fa-heartbeat
```

設定好儲存，再開啟伺服器，就可以看到網站多出了剛剛開啟的選單項目囉 ~

![選單項目出現](https://ithelp.ithome.com.tw/upload/images/20250519/20172694Kuwzsu9cHz.png)

再來假設我想把選單首頁的 icon 改成愛心，要如何調整設定呢？

這邊的 icon 是使用 [Font Awesome](https://fontawesome.com/search) 這個網站的 icon，所以我們就進到這個網站搜尋 heart，找到我想要的愛心 icon 點擊它

然後就會跳出這個 icon 的套用資訊，把圖中紅框處的代碼複製下來

![愛心 icon 套用資訊](https://ithelp.ithome.com.tw/upload/images/20250519/20172694TGYFy4I9NZ.png)

貼到首頁那項 `||` 後方，取代原本的 icon 代碼

```yaml
home: / || fa-solid fa-heart
```

小補充：`fa-solid fa-heart` 前面的 `fa-solid` 可以簡寫成 `fa`，所以也可以改成以下這樣

```yaml
home: / || fa fa-heart
```

重整網站就可以看到首頁的 icon 改成愛心囉 ~

![首頁項目 icon 改為愛心](https://ithelp.ithome.com.tw/upload/images/20250519/20172694kMm3KEffk7.png)

- **注意** ：記得執行 Hexo 指令新增頁面，才能連結到該頁面喔 ~ 如：要連結到標籤頁面，要先執行 `hexo new page tags` 新增頁面，點擊選單的標籤才能看到標籤頁面 ( archives 不用新增頁面，預設已經有連結的頁面了 )

- **補充** ：在 NexT 主題的標籤跟分類頁面開頭，分別加入 `type: tags` 和 `type: categories` 可以開啟該頁面預設的內容 ( 如下圖 )

![標籤頁面開頭 type 設定](https://ithelp.ithome.com.tw/upload/images/20250519/20172694fYqpJ5aZsP.png)

![分類頁面開頭 type 設定](https://ithelp.ithome.com.tw/upload/images/20250519/20172694GHW3ZsiNdY.png)

#### menu_settings

再來介紹 menu_settings 下的設定，icons 可以調整選單項目 icon 的開關，badges 可以調整選單項目數量標記的開關

接下來調整 icons 改成 false，badges 改成 true，實際看看選單項目會有什麼變化

```yaml
menu_settings:
  icons: false
  badges: true
```

設定好再重整網站，會發現選單項目的 icon 都不見了，但是標籤、分類、歸檔這三項多出了數量標記，代表這三項總共有多少數量

![設定後的選單項目](https://ithelp.ithome.com.tw/upload/images/20250519/20172694UlCdyrnQec.png)

這邊歸檔的數量是指網站的文章總共有幾篇，標籤跟分類對應的是文章 md 檔開頭的 tags 跟 categories ( 忘記請參考下方補充 )，所以標籤跟分類後面的數量，分別代表的是網站中所有文章不重複的 tags 有幾個、categories 有幾個

#### 補充：文章開頭設定 categories 跟 description

- **categories**

文章 md 檔開頭的 tags 跟 categories 可以這樣設定，因為 landscape 主題沒用到，所以之前沒有示範過 categories 的設定，這邊補上

![文章 categories 的設定](https://ithelp.ithome.com.tw/upload/images/20250519/201726945UfPoggvXt.png)

有文章有設定 categories 之後，再回去看網站就會看見分類項目的數量變成 1 了

![分類項目數量改變](https://ithelp.ithome.com.tw/upload/images/20250519/20172694MP9RjFUcY7.png)

- **description**

前面有說到如何讓首頁的文章只顯示部分內文，只要在文章中想截斷的地方加入 `<!--more-->`，首頁就會只顯示部份內文，然後多出一個 read more 按鈕，讓瀏覽者點擊查看全文

在 NexT 主題還有提供另一個產生 read more 按鈕的方法，跟 `<!--more-->` 不同的地方是，這個方法可以讓你自訂要顯示的內容是什麼，那就是在文章開頭設定 description

首先在一篇文章的 md 檔開頭加入 description，然後寫入想在首頁文章卡片顯示的文字內容

![文章開頭 description 設定](https://ithelp.ithome.com.tw/upload/images/20250519/20172694Ofese6QUqy.png)

完成後重整網站，查看首頁就會看見文章卡片顯示的是，剛剛 description 設定的內容

![首頁文章卡片顯示 description 的內容](https://ithelp.ithome.com.tw/upload/images/20250519/20172694GrpHDOgt7B.png)

---

### 調整不同模板樣式

NexT 主題本身有提供 4 種不同模板樣式，示範網站如下：

- [Muse](https://theme-next.js.org/muse/)
- [Mist](https://theme-next.js.org/mist/)
- [Pisces](https://theme-next.js.org/pisces/)
- [Gemini](https://theme-next.js.org/)

這邊示範網站提供的是暗色的主題樣式，在還沒調整設定之前預設會是亮色的主題樣式，兩者主要只是以黑或白為主色的差別而已
在調整色系前，先來看看如何調整不同模板樣式吧 ~ 順便給大家看看 4 種不同亮色的主題長什麼樣

調整模板樣式的方式很簡單，找到 scheme 改成你想要的模板樣式名稱就可以囉 ~

假設我要改成 Gemini 這個樣式，只要把原本的樣式註解掉，再解除想要樣式的註解，就會套用這個樣式的主題了

![修改主題的 scheme 設定](https://ithelp.ithome.com.tw/upload/images/20250519/20172694UFsWBnxv81.png)

亮色的 4 種不同模板樣式網站畫面：

- Muse

![亮色的 Muse 樣式](https://ithelp.ithome.com.tw/upload/images/20250519/20172694OLK7ey0pX8.png)

- Mist

![亮色的 Mist 樣式](https://ithelp.ithome.com.tw/upload/images/20250519/20172694t7S9xQ6rGO.png)

- Pisces

![亮色的 Pisces 樣式](https://ithelp.ithome.com.tw/upload/images/20250519/20172694YAwzbE9hs3.png)

- Gemini

![亮色的 Gemini 樣式](https://ithelp.ithome.com.tw/upload/images/20250519/20172694huIia5q6If.png)

---

### 調整明暗主題色系

除此之外，NexT 主題還可以選擇明暗色系的主題樣式，這對於喜歡暗色系網站的我來說就是福音，白色對我來說太明亮了 ~~太耀眼了，看太久會被消滅~~

調整方式也很簡單，只要在 NexT 主題的 config 檔中，把 darkmode 改成 true，就可以開啟 ~~暗黑模式~~ 暗色系的主題樣式囉 ~

![darkmode 改成 true](https://ithelp.ithome.com.tw/upload/images/20250519/20172694n030vsX3rY.png)

然後重整網站，搭啦 ~ 網站就變成暗色系的主題樣式了🪄

![網站變成暗色系樣式](https://ithelp.ithome.com.tw/upload/images/20250519/20172694v1mtpwVmvE.png)

---

### favicon、logo、作者頭像設定

如果你自己有設計網站的 logo，或是自己的頭像，NexT 主題也可以幫你把這些圖片客製到你的網站上

先說 logo 的部分，找到以下片段，這邊可以調整網站的 favicon 和 logo，這兩個部分的相關設定

![設定 favicon、logo 的片段](https://ithelp.ithome.com.tw/upload/images/20250519/20172694yvKnQ2kotk.png)

#### favicon

favicon 就是網站頁籤紅框處的這個圖片，通常會放 logo，這部分就要用 favicon

![網站 favicon 的位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694YLjgbL8GDM.png)

上面提到的網站頁籤圖片就要靠 `favicon` 下的設定來調整，你會看見 small 跟 medium ... 各個項目，每個設定都有一串圖片路徑，它們來自一個 images 的資料夾

```yaml
favicon:
  small: /images/favicon-16x16-next.png
  medium: /images/favicon-32x32-next.png
  apple_touch_icon: /images/apple-touch-icon-next.png
  safari_pinned_tab: /images/logo.svg
  #android_manifest: /manifest.json
```

images 資料夾在 `themes/next/source` 路徑下，打開來你就會看到主題預設給你的 logo 跟頭像圖片

![images 資料夾內容](https://ithelp.ithome.com.tw/upload/images/20250519/20172694ljwFueAmrR.png)

接下來就是依照預設圖片的尺寸，去設計 favicon 的圖檔，然後把 `favicon` 下的圖片路徑改成新的圖片路徑即可，假如 small 要改成套用 images 資料夾中 `favicon-small.png` 這個檔案的話，路徑就要改成以下這樣

```yaml
small: /images/favicon-small.png
```

我自己是把 `favicon` 下的沒註解掉的項目，都改成自己的 logo 了，但你可以看自己的需求做調整就好

#### logo

接下來調整網站的 logo 圖片，找到以下片段，備註有說 Mist 樣式不支援客製化 logo 的設定，所以選擇 Mist 樣式的朋友，如果有這項需求可以考慮換成其他樣式

![設定 logo 的片段](https://ithelp.ithome.com.tw/upload/images/20250519/20172694YVbMJ8O9uH.png)

跟上面的 favicon 一樣，可以把設計的 logo 圖檔放到 images 資料夾中，然後再調整圖片路徑，假設我要改成 images 中 `logo.png` 這個圖檔，那路徑就要改成以下這樣

```yaml
custom_logo: /images/logo.png
```

設定好之後回到網站重整，就可以看見網站上多出了 logo 的圖片

![網站多出了 logo 的圖片](https://ithelp.ithome.com.tw/upload/images/20250519/20172694TZPjFJM94x.png)

不同樣式 logo 位置可能會不同，這邊就不一一示範，留給大家去嘗試囉 ~

#### 作者頭像

如果你有自己想放的頭像，NexT 主題也有提供一個地方讓你放頭像的圖片路徑

找到以下的 `avatar` 片段，然後跟前面設定方式一樣，在 images 資料夾放入你想放的頭像圖檔，然後修改 url 的圖片路徑設定

![avatar 片段內容](https://ithelp.ithome.com.tw/upload/images/20250519/20172694CXGxKRDDMB.png)

假設要放的圖檔名稱是 `myphoto.png`，url 這項的路徑就要改成以下這樣

```yaml
url: /images/myphoto.png
```

設定後回到首頁就可以看見側欄出現了剛剛設定的頭像

![側欄出現頭像](https://ithelp.ithome.com.tw/upload/images/20250519/20172694cNaLWylnz4.png)

再來這個片段還有 2 個設定：`rounded` 跟 `rotated`

把 `rounded` 設定為 `true` 可以將頭像裁切成圓形，呈現畫面如下

![側欄頭像變圓形](https://ithelp.ithome.com.tw/upload/images/20250519/20172694MZi4Dk4VTx.png)

而 `rotated` 設定為 `true` 可以讓頭像新增一個 hover 的動畫效果，當瀏覽者把滑鼠移到頭像上時，頭像會像唱片一樣旋轉，這個效果就留給大家嘗試看看喜不喜歡囉 ~

---

### 社群連結按鈕

既然說到了作者頭像如何設定，那就接著講如何設定你的社群連結按鈕吧 ~

找到以下片段，`social` 下預設註解就有一些常用的社群連結及 icon 圖案設定，也可以另外新增其他的社群媒體連結及 icon 圖案

![social 片段](https://ithelp.ithome.com.tw/upload/images/20250519/20172694mdfGeMipYT.png)

這邊的 icon 修改方式跟 menu 選單項目設定的方式一樣，找到想要的 icon 代碼加入即可

假設我想新增 Discord 的社群按鈕，我找到 Font Awesome 中 icon 代碼是 `fa-brands fa-discord`，那就可以新增 Discord 設定到 `social` 下，這邊 icon 代碼 `fa-brands` 可以簡寫成 `fab`

```yaml
social:
  Discord: https://discord.com/你的Discord || fab fa-discord
```

設定後重整網站，就可以看見首頁側欄最下面出現剛剛設定的 Discord 社群按鈕囉 ~

![側欄最下面出現 Discord 社群按鈕](https://ithelp.ithome.com.tw/upload/images/20250519/20172694DLC6t0n0Wk.png)

再往下可以看見還有 `social_icons`，這個片段可以調整社群按鈕的 icon 設定

```yaml
social_icons:
  enable: true
  icons_only: false
  transition: false
```

每項設定介紹如下：

- `enable`：可以設定社群按鈕是否要顯示 icon
- `icons_only`：可以設定社群按鈕是否要只顯示 icon、不顯示文字
- `transition`：可以設定是否顯示 icon 的 transition 效果

transition 效果我自己其實看不太出差異，但官方文件說有這個效果，說不定有人感覺有差，那這個片段就留給大家嘗試自己喜歡的設定囉 ~

---

### copy right

再來我相信一定會有人想改 copy right 預設的內容吧？我自己是很想改成其他可愛的 icon，這樣每次看到都會療癒一下，接下來就來介紹以下 copy right 預設內容如何調整吧 ~

![網站預設 copy right](https://ithelp.ithome.com.tw/upload/images/20250519/20172694vvj81hPcYu.png)

先找到以下片段

![footer 片段內容](https://ithelp.ithome.com.tw/upload/images/20250519/201726945gQ4XMewmX.png)

`footer` 下會有 `icon`、`copyright`、`powered` 三個設定，這三個設定可以用來調整網站 footer 區塊的 copy right 內容

- `icon`：有 `name`、`animated`、`color` 這三項，可以設定下圖黃框處的 icon
  - `name`：用來設定 Font Awesome 的 icon 圖案代碼
  - `animated`：用來設定是否開啟讓 icon 跳動的動畫
  - `color`：用來設定 icon 的顏色
- `copyright`：可以寫入在下圖紅框處要顯示的文字，未設定會預設為全站 config 檔設定的 author 名稱，設定為 `false` 可不顯示整段 copy right 文字 ( 不包含強力驅動文字 )
- `powered`：可以設定是否要顯示下圖綠框處的強力驅動文字

![footer 片段對應網站的位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694Jt7iHU61eR.png)

copy right 的文字通常會寫類似：「轉載文章時請附上作者名及原文連結」的內容，然後我自己是會關閉強力驅動的文字，改一個喜歡的 icon 圖案、換顏色再加動畫 ~~會跳動的 icon 比較可愛~~

示範一下設定內容

```yaml
icon:
  name: fa fa-user-astronaut
  animated: true
  color: "#0080FF"

copyright: 轉載文章時請附上作者名及原文連結

powered: false
```

設定後重整網站，footer 就會變更成新設定的內容囉 ~

![copy right 區塊網站內容](https://ithelp.ithome.com.tw/upload/images/20250519/20172694HI5xQpqRuy.png)

這邊大家可以實際操作設定自己的 copy right 內容，看看自己比較喜歡哪種設定

### 如何調整文章開頭的顯示文字

再來我想應該會有人，想調整下圖紅框處文章開頭的這串文字吧？如果用預設再加上有分類項目的話，感覺確實資訊很多很雜

![網站文字開頭資訊](https://ithelp.ithome.com.tw/upload/images/20250519/20172694uw0BBuYw5v.png)

首先先找到以下片段

![post_meta 片段內容](https://ithelp.ithome.com.tw/upload/images/20250519/20172694H2ksQASP4X.png)

`post_meta` 這個片段可以用來調整文章開頭的區塊要顯示哪些內容

- `item_text`：用來設定是否要顯示項目前方的「發表於」、「更新於」、「分類於」文字 ( 如下圖黃框處 )

![item_text 在網站的顯示位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694sCV3F2nFno.png)

- `created_at`：用來設定是否要顯示文章的發表日期 ( 如下圖綠框處 )

![created_at 在網站的顯示位置](https://ithelp.ithome.com.tw/upload/images/20250519/201726946O6GMIcSBE.png)

- `update_at`：用來設定文章更新時間 ( 如下圖藍框處 ) 的顯示方式
  - `enable`：用來設定是否要顯示文章的更新日期
  - `another_day`：用來設定當發表日期和更新日期相同時，是否要顯示文章的更新時間，`true` 會不顯示更新時間、`false` 則會顯示更新時間

![update_at 在網站的顯示位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694OjN6CKSZoX.png)

- `categories`：用來設定是否要顯示文章的分類項目 ( 如下圖橘框處 )

![categories 在網站的顯示位置](https://ithelp.ithome.com.tw/upload/images/20250519/20172694ZX0qDYajEc.png)

這邊就讓大家試試看要顯示哪些內容在文章標題下方囉 ~

---

### 客製化檔案路徑

如果你有自己寫的程式碼想要加入網站中的某些區塊，NexT 主題有提供一個區塊 `custom_file_path`，讓使用者可以設定客製的檔案路徑

`custom_file_path` 區域上方的註解有說明，可以新增客製化檔案到 `source/_data` 路徑下，也可以用以下預設內容來新增不同網站部分的客製化檔案

![custom_file_path 片段位置](https://ithelp.ithome.com.tw/upload/images/20250519/2017269428UT0JD0PO.png)

這部分如果有需要可以多多運用，裡面還可以自己設定網站的樣式變數、也可以新增自己的 `styles.styl` 檔讓網站套用你寫的樣式檔，另外還可以針對網站結構也做客製，這邊看到可以新增不同部分的 njk 檔

---

### 更多檔案中的設定

其實 NexT 主題 config 檔中的設定還蠻多的，這裡介紹的只是一部份我想分享的設定，也推薦大家客製化遇到問題可以先探索一下這個檔案，如果有遇到想了解的設定也可以參考官方文件，多多探索可以幫助你更快掌握如何客製化

## 客製化修改程式碼

雖然有一些網站部分內容的客製化，可以透過上面提到的 NexT 主題 config 檔來設定達成，但是可能會有些東西你很想客製化，卻無法透過以上方法來調整設定

這時候就需要直接修改主題檔案的程式碼了，而在 NexT 主題修改的方式其實很類似之前客製化 landscape 主題的做法，只是檔案名稱和位置可能會不同，所以需要另外研究跟適應

但如果要直接修改原本檔案的程式碼，一樣會建議修改時用註解標記新增了哪些程式碼區段，或是把原本的設定值註解保留，以防後續需要更新主題版本時，無法對照修改了哪些程式碼

雖然通常不是想用新功能或是網站有出什麼問題，是不會主動去更新主題版本的，所以上面的建議就是一個以防萬一的準備

接下來就針對需要修改 NexT 主題本身檔案的程式碼時，如何找到該程式碼的檔案位置來做介紹

---

### njk 檔是什麼？

還記得之前 landscape 主題客製化，有介紹到一個統整所有頁面結構的檔案叫 `layout.ejs`，在 NexT 主題也有這樣的檔案，一樣在 layout 資料夾，但是它的檔名是 `_layout.njk`

如果你點開在 `themes/next/layout` 路徑下的 `_layout.njk` 檔，你會發現這個 njk 檔的內容和之前介紹的 EJS 樣版語言很類似

沒錯，它也是一種樣板語言，叫 Nunjucks ( 以下簡稱 njk )，它跟 EJS 一樣可以加入 JavaScript 到 HTML 片段中，也可以引入其他檔案的內容

只是語法上有些不同，EJS 是用 `<%- %>` 符號包住程式碼，njk 則是用 `{%  %}` 包住程式碼，如果想更深入了解這個語言的寫法可以參考 [Nunjucks 的官網文件](https://nunjucks.bootcss.com/templating.html)

---

### 如何找到要客製的 HTML 程式碼片段

這邊會再簡單介紹在 NexT 主題，如何尋找被引入 `_layout.njk` 的檔案所在位置

以網站 HTML 的 head 區塊為例，假設我想找到第 4 行被引入的檔案在哪，下圖程式碼可以看見 `_partials/head/head.njk` 這樣的內容

![_layout.njk 的 head 區塊](https://ithelp.ithome.com.tw/upload/images/20250519/20172694D88MQ93zB6.png)

所以可以知道第 4 行被引入的檔案，在 `_partials` 內的 `head` 資料夾，檔名是 `head.njk`，打開這個檔案就可以看見引入的內容是什麼了

![head.njk 檔內容](https://ithelp.ithome.com.tw/upload/images/20250519/20172694P4dzf8Pwmt.png)

接下來為了驗證，我們回到網站打開發者工具，查看 Elements 中網站的 `<head>` 起始標籤後第一行，是否和 `head.njk` 裡的第一行：`<meta charset="UTF-8">` 一樣

![開發者工具 head 程式碼內容](https://ithelp.ithome.com.tw/upload/images/20250519/20172694OXTJAKvXau.png)

看完上面的介紹，是不是覺得和 landscape 主題客製化的做法很像？之後如果需要客製化某個網站部分，也可以依照上面方式查找驗證，然後嘗試修改再觀察網站畫面的變化

---

### 如何找到要客製的 CSS 程式碼片段

在 NexT 主題中也有類似 landscape 主題的 `style.styl` 檔，它就是在 `themes/next/source/css` 路徑下的 `main.styl` 檔 ( 如下 )

![main.styl 檔的內容](https://ithelp.ithome.com.tw/upload/images/20250519/20172694kJ7nRaJLaZ.png)

這個檔案可以看到被引入的 styl 檔在哪裡，以 `@import '_variables/base';` 來說，引入的檔案是 `_variables` 資料夾內的 `base.styl` 檔

前面有介紹 NexT 主題有 4 種不同的模板樣式，不同模板樣式會有不同的樣式變數，所以當點開 `_variables` 資料夾，你還會看到其他 4 個以樣式模板名稱命名的 styl 檔案

![_variables 資料夾內的檔案](https://ithelp.ithome.com.tw/upload/images/20250519/20172694V8D87bfhih.png)

再對照 `main.styl` 檔，模板樣式變數的引入位置，是在 `base.styl` 檔之後 ( 下圖紅框處 ) ，那麼就可以知道後面引入的檔案內容，會覆蓋前面引入的設定內容

![模板樣式變數的引入位置](https://ithelp.ithome.com.tw/upload/images/20250519/201726949nxtnpQljM.png)

也就是說假設你調整了 base 檔的變數設定，卻沒反應可以到你使用的模板樣式變數檔看看，是否有一樣名稱的變數把 base 檔的設定覆蓋了

了解如何尋找被引入的檔案在哪之後，如果有想客製化修改的樣式，修改步驟就會和 landscape 主題在客製化時的方式很類似

只要利用開發者工具找到要修改的 CSS 程式碼大約在哪，在回到 `main.styl` 檔尋找該程式碼可能在哪個檔案中，就可以修改看看、觀察網站樣式是否有變動，如果有的話就恭喜你找到它囉🎉

補充：styl 檔除了 CSS 之外也可以寫 SCSS 喔 ~ 有 SCSS 就能更有效率的寫網站樣式的程式碼了

---

### 補充：languages 資料夾介紹

在 next 資料夾中有一個 languages 的資料夾，點開裡面會有各種語言的翻譯文字，繁體中文在 `zh-TW.yml` 檔內，所以如果有文字翻譯想調整，可以來看看是否有在這個檔案中

![zh-TW.yml 檔案內容](https://ithelp.ithome.com.tw/upload/images/20250519/20172694Zii5TvXf8n.png)

## 結語

這篇文章前面主要簡單介紹 NexT 主題的 config 檔在客製化上面有哪些設定，後面才提到如果有直接修改原本檔案的需求時，要怎麼找到想找的程式碼在哪

我本人比較懶，所以 NexT 主題的 config 檔直接設定一些內容，真的很棒 ~ 如果你正在努力客製 NexT 主題 Hexo 網站，希望這篇文章能幫助你製作出你理想的 Hexo 網站

那我們就下篇文章見囉 ~
