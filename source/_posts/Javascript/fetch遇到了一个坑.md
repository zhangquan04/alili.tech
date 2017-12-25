---
title: fetch遇到了一个坑
date: 2016-06-08T22:52:35.000Z
tags: null
---
fetch 在跨域的情况下,不带cookie;

解决办法:

带上参数{credentials: 'include'}后才可以在请求里面带上cookie

```javascript
fetch('doAct.action', {credentials: 'include'}).then(function(res) {
    // ...
})
```
