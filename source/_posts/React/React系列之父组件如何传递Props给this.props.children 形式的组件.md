---
title: React系列之父组件如何传递Props给this.props.children
date: 2017-09-08T19:33:33.000Z
tags: React
---

### 问题
React使用router之后,以下形式会经常出现.

```javascript
this.props.children
```
可是这样渲染出来的组件,父组件如何传递props给它呢?

### 解决


我们可以这样传递porps给子组件:

```javascript
{ 
    React.cloneElement(this.props.children,{A:xxx,B:xxx2,C:xxx3}) 
    
 }
```

