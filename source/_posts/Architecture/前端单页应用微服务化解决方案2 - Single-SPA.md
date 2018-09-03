---
title: 前端单页应用微服务化解决方案2 - Single-SPA 
date: 2018-09-02 22:17:36
tags: 前端架构
---
# 技术选型

经过各种技术调研我们最终选择的方案是基于 [Single-SPA](https://single-spa.js.org/) 来实现我们的前端微服务化.

# Single-SPA

> 一个用于前端微服务化的JavaScript前端解决方案
 
 使用Single-SPA之后,你可以这样做:

* 在同一个页面中使用多种技术框架(React, Vue, AngularJS, Angular, Ember等任意技术框架),并且不需要刷新页面.
* 使用新的技术框架编写代码,现有项目中的代码无需重构.
* 每个独立模块的代码可做到按需加载,不浪费额外资源.

下面是一个微前端的演示页面
 [https://single-spa.surge.sh/](https://single-spa.surge.sh/)