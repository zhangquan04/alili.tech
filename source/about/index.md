---
title: About Me
date: 2016-05-27T14:31:51.000Z
---

# 联系方式

- Email：incomparable9527@foxmail.com 

---

# 个人信息

 - Fan/男/1992
 - 大专/计算机应用
 - 工作年限：4年
 - 技术博客：http://alili.tech 
 - Github：https://github.com/Fantasy9527
 - 期望职位：高级Web前端开发工程师
 - 期望城市：杭州

---

# 工作经历

## 深圳市彩虹云宝网络有限公司 （ 2014年12月 ~ 2017年3月 ）
> 负责公司前端规范的制定，组建前端团队。所有的前端项目核心代码的编写,以及项目工程化的相关工作。

### 食通宝后台管理系统
用于餐馆数据、菜品数据、促销活动、会员卡、微信公众平台配置 ,餐馆营业报表的统计展示,餐馆营业实时数据展示

应用类型:SPA 单页面应用

本项目一共有将近200个页面。 为了更好的组织代码,本人做了以下处理:

* 所有的代码文件,根据业务类型分类。

* 基于Angular兼容了旧的Ractive.js

* 基于 requirejs,Angularjs实现了按需加载。 并且实现了Angularjs官方没有实现的第三方模块热加载功能。不会因为Angularjs启动时就加载所有第三方模块，导致首页加载极慢。

* 基于自动化工具,提取Angularjs所有的html模板文件合并到一个js文件里（200多个页面的模板合并后，加上Gzip的压缩只有100k+，文件体积是可以接受的）。当页面加载时，会把所有模板注入到Angularjs。

* 当切换页面的时候，每个页面只会加载一个很小的js文件（业务代码）。因为减少了模板文件请求，提升了所有的页面加载速度。

* bower管理第三方库。用Grunt以及其插件实现代码的压缩,合并,丑化,自动依赖注入,编译less,postcss,文件名添加MD5后缀,自动构建压缩 zip,自动上传部署, 等一系列任务。

最终只要一个命令的持续集成。


本地开发时,运用Grunt实现了非常智能的请求代理功能 (比webpack的代理要好用灵活非常多) 前端开发的电脑上不需要安装任何的后台服务,新同事从Github上clone项目下来,

运行一下命令便可启动整个前端项目：
```
npm install //安装npm依赖

npm start // 映射的是grunt serve
```

最终实现了：

* 不需要配置CORS跨域（因为大量的option请求看着很糟心）。
* 不需要mock。
* 可以随意配置数据源
* 随时随地，任意电脑直接开发

运用 echarts 做数据的可视化。
使用 webscoket 实现了门店的实时数据的展示。

使用的主要开源库与工具有: 
* AngularJs
* echarts 
* jQuery
* RequireJs
* Bootstrap 
* Grunt 
* Bower 
* Ractive.js



### 食通宝微信(支付宝)点餐 （2015.12 ~ 2017.03）
所有的前端功能的设计与开发 

应用类型:移动端 SPA 单页面应用


这次项目我最满意地方是: 

 为了在移动端保证更快的加载速度,去除了除 AngularJs,RequireJs 以外的所有插件。 代码合并压缩 gzip 之后不超过70k。 并且使用了 application cahe,缓存了很多经常使用的资源。 加载速度又一次得到了一定的提升

功能运用场景: 餐厅的餐桌贴上特制的二维码,可以直接可以用微信(支付宝)扫一扫直接进行点菜,加菜,支付的一系列操作。

使用的主要开源库与工具有: 

* AngularJs
* RequireJs
* Grunt
* Bower

### 其他项目

- 食通宝融合支付/微信与支付宝 (2017年2月 ~ 2017年3月)

- 食通宝进销存管理系统 (2016年10月 ~ 2017年3月)

- 食通宝运营支撑系统 (2016年4月 ~ 2017年3月)

- 食通宝微信会员 (2015年7月 ~ 2017年3月)

- 食通宝老板助手 (2017年2月 ~ 2017年3月)

- 食通宝打赏小二 (2015年8月 ~ 2015年11月)

- 食通宝pad电子菜单 (2017年2月 ~ 2017年3月)

 
## 广西易谷网络科技有限公司 （ 2013年7月 ~ 2014年9月 ）

### 大愿说法 佛经电子书 
一款嵌入 ios 的 web 电子书应用,主要开发任务为利用 Javascript,HTML5，css3特性,根据不同屏幕大小自动排版文字与图片


---


## 开源项目

 - [everygreen](https://github.com/Fantasy9527/everygreen)：Hack github contribution,让你的contribution面板一绿到底
 - [AliToSingn](https://github.com/Fantasy9527/AliToSign) :基于nodejs的阿里云API签名生成工具


# 技能清单
以下均为我熟练使用的技能

- 前端框架：AngularJS/Angular2.0+/React/Vue
- 前端工具：Bower/Grunt/Less/webpack/create-react-app/vue-cli/angular-cli
- 后台框架：Express ,Egg.js
- 数据库 ：Mysql
- 版本工具：Git

---
## 自我评价

4年WEB前端开发经验,从事餐饮收银软件开发2年多。

独自一人在上一家公司完成了12个项目的前端所有工作,期间独自踩过无数的坑。

熟练掌握CSS3.0和W3C标准。并深刻了解移动端浏览器与PC主流浏览器之间的兼容性。

熟悉原生JavaScript,Typescript以及Angularjs、React、Vue、jQuery、zepto等框架,

Antd for React、NG-ZORRO、Angularstrap、vux、ElementUI、bootstrap,weUI, 等UI组件库的使用经验

create-react-app,vue-cli,Grunt,bower,RequireJs,LESS,Sass,webpack,Git等工具的使用经验。

熟悉HTML5最新规范。能熟练开发移动端WebAPP。

有Express，Egg.js的后台开发经验,能够紧密的与后台人员进行对接。

能快速接手项目进行开发工作。

喜欢逛Github,npmjs,stackoverflow等网站。
业余时间喜欢研究Nodejs写点小工具，树莓派爱好者。

---

# 致谢
感谢您花时间阅读我的简历，期待能有机会和您共事。
