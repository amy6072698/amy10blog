---
title: '404 你被傳送到了秘密空間 Σ(っ°Д°;)っ'
date: 2020-09-12 23:01:35
comments: false
permalink: /404.html
---

<!-- markdownlint-disable MD039 MD033 -->

### 這裡似乎不是你想去的地方...

別擔心！<b id="timeout">10</b> 秒後傳送魔法會將你送回首頁(ﾉ◕ヮ◕)ﾉ*:･ﾟ✧

如果你不想等，可以 **[點這裡](https://amy6072698.github.io/amy10blog/)** 自己施展魔法回首頁~

![404頁面](https://images.unsplash.com/photo-1514539079130-25950c84af65?q=80&w=600&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D)

<script>
let countTime = 10;

function count() {
  
  document.getElementById('timeout').textContent = countTime;
  countTime -= 1;
  if(countTime === 0){
    location.href = 'https://amy6072698.github.io/amy10blog/'; // 記得改成自己網址 Url
  }
  setTimeout(() => {
    count();
  }, 1000);
}

count();
</script>