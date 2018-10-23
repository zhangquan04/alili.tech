---
title: import、require、export、module.exports 混合使用详解
reprint: true
categories: reprint
abbrlink: 5a5dfc0d
date: 2018-10-23 18:37:28
---

{% raw %}

                    
<blockquote>2018.3.1&#x66F4;&#xFF1A;</blockquote>
<p>&#x6709;&#x8D5E;&#xB7;&#x5FAE;&#x5546;&#x57CE;(base&#x676D;&#x5DDE;)&#x90E8;&#x95E8;&#x62DB;&#x524D;&#x7AEF;&#x5566;&#xFF0C;&#x6700;&#x8FD1;&#x7684;&#x524D;&#x7AEF;hc&#x6709;&#x5341;&#x591A;&#x4E2A;&#xFF0C;&#x8DEA;&#x6C42;&#x5927;&#x4F6C;&#x6254;&#x7B80;&#x5386;&#xFF0C;&#x6211;&#x76F4;&#x63A5;&#x8FDB;&#x884C;&#x5185;&#x63A8;&#x5B9E;&#x65F6;&#x53CD;&#x9988;&#x8FDB;&#x5EA6;&#xFF0C;&#x6709;&#x5174;&#x8DA3;&#x7684;&#x90AE;&#x4EF6; lvdada#youzan.com&#xFF0C;&#x6216;&#x76F4;&#x63A5;&#x5FAE;&#x4FE1;&#x52FE;&#x642D;&#x6211; wsldd225 &#x4E86;&#x89E3;&#x8DDF;&#x591A;</p>
<p>&#x6709;&#x8D5E;&#x5F00;&#x6E90;&#x7EC4;&#x4EF6;&#x5E93;&#xB7;<a href="https://www.youzanyun.com/zanui" rel="nofollow noreferrer" target="_blank">zanUI</a></p>
<hr>
<h2 id="articleHeader0">&#x524D;&#x8A00;</h2>
<p>&#x81EA;&#x4ECE;&#x4F7F;&#x7528;&#x4E86; es6 &#x7684;&#x6A21;&#x5757;&#x7CFB;&#x7EDF;&#x540E;&#xFF0C;&#x5404;&#x79CD;&#x5730;&#x65B9;&#x6109;&#x5FEB;&#x5730;&#x4F7F;&#x7528; <code>import</code> <code>export default</code>&#xFF0C;&#x4F46;&#x4E5F;&#x4F1A;&#x5728;&#x8001;&#x9879;&#x76EE;&#x4E2D;&#x770B;&#x5230;&#x4F7F;&#x7528;commonjs&#x89C4;&#x8303;&#x7684; <code>require</code> <code>module.exports</code>&#x3002;&#x751A;&#x81F3;&#x6709;&#x65F6;&#x5019;&#x4E5F;&#x4F1A;&#x5E38;&#x5E38;&#x770B;&#x5230;&#x4E24;&#x8005;&#x4E92;&#x7528;&#x7684;&#x573A;&#x666F;&#x3002;&#x4F7F;&#x7528;&#x6CA1;&#x6709;&#x95EE;&#x9898;&#xFF0C;&#x4F46;&#x5176;&#x4E2D;&#x7684;&#x5173;&#x8054;&#x4E0E;&#x533A;&#x522B;&#x4E0D;&#x5F97;&#x5176;&#x89E3;&#xFF0C;&#x4F7F;&#x7528;&#x8D77;&#x6765;&#x4E5F;&#x7CCA;&#x91CC;&#x7CCA;&#x6D82;&#x3002;&#x6BD4;&#x5982;&#xFF1A;</p>
<ol>
<li>&#x4E3A;&#x4F55;&#x6709;&#x7684;&#x5730;&#x65B9;&#x4F7F;&#x7528; <code>require</code> &#x53BB;&#x5F15;&#x7528;&#x4E00;&#x4E2A;&#x6A21;&#x5757;&#x65F6;&#x9700;&#x8981;&#x52A0;&#x4E0A; <code>default</code>&#xFF1F; <code>require(&apos;xx&apos;).default</code>
</li>
<li>&#x7ECF;&#x5E38;&#x5728;&#x5404;&#x5927;UI&#x7EC4;&#x4EF6;&#x5F15;&#x7528;&#x7684;&#x6587;&#x6863;&#x4E0A;&#x4F1A;&#x770B;&#x5230;&#x8BF4;&#x660E; <code>import { button } from &apos;xx-ui&apos;</code> &#x8FD9;&#x6837;&#x4F1A;&#x5F15;&#x5165;&#x6240;&#x6709;&#x7EC4;&#x4EF6;&#x5185;&#x5BB9;&#xFF0C;&#x9700;&#x8981;&#x6DFB;&#x52A0;&#x989D;&#x5916;&#x7684; babel &#x914D;&#x7F6E;&#xFF0C;&#x6BD4;&#x5982; <code>babel-plugin-component</code>&#xFF1F;</li>
<li>&#x4E3A;&#x4EC0;&#x4E48;&#x53EF;&#x4EE5;&#x4F7F;&#x7528; es6 &#x7684; import &#x53BB;&#x5F15;&#x7528; commonjs &#x89C4;&#x8303;&#x5B9A;&#x4E49;&#x7684;&#x6A21;&#x5757;&#xFF0C;&#x6216;&#x8005;&#x53CD;&#x8FC7;&#x6765;&#x4E5F;&#x53EF;&#x4EE5;&#x53C8;&#x662F;&#x4E3A;&#x4EC0;&#x4E48;&#xFF1F;</li>
<li>&#x6211;&#x4EEC;&#x5728;&#x6D4F;&#x89C8;&#x4E00;&#x4E9B; npm &#x4E0B;&#x8F7D;&#x4E0B;&#x6765;&#x7684; UI &#x7EC4;&#x4EF6;&#x6A21;&#x5757;&#x65F6;&#xFF08;&#x6BD4;&#x5982;&#x8BF4; element-ui &#x7684; lib &#x6587;&#x4EF6;&#x4E0B;&#xFF09;&#xFF0C;&#x770B;&#x5230;&#x7684;&#x90FD;&#x662F; webpack &#x7F16;&#x8BD1;&#x597D;&#x7684; js &#x6587;&#x4EF6;&#xFF0C;&#x53EF;&#x4EE5;&#x4F7F;&#x7528; import &#x6216; require &#x518D;&#x53BB;&#x5F15;&#x7528;&#x3002;&#x4F46;&#x662F;&#x6211;&#x4EEC;&#x5E73;&#x65F6;&#x7F16;&#x8BD1;&#x597D;&#x7684; js &#x662F;&#x65E0;&#x6CD5;&#x518D;&#x88AB;&#x5176;&#x4ED6;&#x6A21;&#x5757; import &#x7684;&#xFF0C;&#x8FD9;&#x662F;&#x4E3A;&#x4EC0;&#x4E48;&#xFF1F;</li>
<li>babel &#x5728;&#x6A21;&#x5757;&#x5316;&#x7684;&#x573A;&#x666F;&#x4E2D;&#x5145;&#x5F53;&#x4E86;&#x4EC0;&#x4E48;&#x89D2;&#x8272;&#xFF1F;&#x4EE5;&#x53CA; webpack &#xFF1F;&#x54EA;&#x4E2A;&#x542F;&#x5230;&#x4E86;&#x5173;&#x952E;&#x4F5C;&#x7528;&#xFF1F;</li>
<li>&#x542C;&#x8BF4; es6 &#x8FD8;&#x6709; <code>tree-shaking</code> &#x529F;&#x80FD;&#xFF0C;&#x600E;&#x4E48;&#x624D;&#x80FD;&#x4F7F;&#x7528;&#x8FD9;&#x4E2A;&#x529F;&#x80FD;&#xFF1F;</li>
</ol>
<p>&#x5982;&#x679C;&#x4F60;&#x5BF9;&#x8FD9;&#x4E9B;&#x95EE;&#x9898;&#x90FD;&#x4E86;&#x7136;&#x4E8E;&#x5FC3;&#xFF0C;&#x90A3;&#x4E48;&#x53EF;&#x4EE5;&#x5173;&#x6389;&#x672C;&#x6587;&#x4E86;&#xFF0C;&#x5982;&#x679C;&#x6709;&#x7591;&#x95EE;&#xFF0C;&#x8FD9;&#x7BC7;&#x6587;&#x7AE0;&#x5C31;&#x662F;&#x4E3A;&#x4F60;&#x51C6;&#x5907;&#x7684;&#xFF01;</p>
<h2 id="articleHeader1">webpack &#x4E0E; babel &#x5728;&#x6A21;&#x5757;&#x5316;&#x4E2D;&#x7684;&#x4F5C;&#x7528;</h2>
<h3 id="articleHeader2">webpack &#x6A21;&#x5757;&#x5316;&#x7684;&#x539F;&#x7406;</h3>
<p>webpack &#x672C;&#x8EAB;&#x7EF4;&#x62A4;&#x4E86;&#x4E00;&#x5957;&#x6A21;&#x5757;&#x7CFB;&#x7EDF;&#xFF0C;&#x8FD9;&#x5957;&#x6A21;&#x5757;&#x7CFB;&#x7EDF;&#x517C;&#x5BB9;&#x4E86;&#x6240;&#x6709;&#x524D;&#x7AEF;&#x5386;&#x53F2;&#x8FDB;&#x7A0B;&#x4E0B;&#x7684;&#x6A21;&#x5757;&#x89C4;&#x8303;&#xFF0C;&#x5305;&#x62EC; <code>amd</code> <code>commonjs</code> <code>es6</code> &#x7B49;&#xFF0C;&#x672C;&#x6587;&#x4E3B;&#x8981;&#x9488;&#x5BF9; <code>commonjs es6</code> &#x89C4;&#x8303;&#x8FDB;&#x884C;&#x8BF4;&#x660E;&#x3002;&#x6A21;&#x5757;&#x5316;&#x7684;&#x5B9E;&#x73B0;&#x5176;&#x5B9E;&#x5C31;&#x5728;&#x6700;&#x540E;&#x7F16;&#x8BD1;&#x7684;&#x6587;&#x4EF6;&#x5185;&#x3002;</p>
<p>&#x6211;&#x7F16;&#x5199;&#x4E86;&#x4E00;&#x4E2A; demo &#x66F4;&#x597D;&#x7684;&#x5C55;&#x793A;&#x6548;&#x679C;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="// webpack

const path = require(&apos;path&apos;);

module.exports = {
  entry: &apos;./a.js&apos;,
  output: {
    path: path.resolve(__dirname, &apos;dist&apos;),
    filename: &apos;bundle.js&apos;,
  }
};
" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="javascript hljs"><code class="javascript"><span class="hljs-comment">// webpack</span>

<span class="hljs-keyword">const</span> path = <span class="hljs-built_in">require</span>(<span class="hljs-string">&apos;path&apos;</span>);

<span class="hljs-built_in">module</span>.exports = {
  <span class="hljs-attr">entry</span>: <span class="hljs-string">&apos;./a.js&apos;</span>,
  <span class="hljs-attr">output</span>: {
    <span class="hljs-attr">path</span>: path.resolve(__dirname, <span class="hljs-string">&apos;dist&apos;</span>),
    <span class="hljs-attr">filename</span>: <span class="hljs-string">&apos;bundle.js&apos;</span>,
  }
};
</code></pre>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="
// a.js
import a from &apos;./c&apos;;

export default &apos;a.js&apos;;
console.log(a);
" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="javascript hljs"><code class="javascript">
<span class="hljs-comment">// a.js</span>
<span class="hljs-keyword">import</span> a <span class="hljs-keyword">from</span> <span class="hljs-string">&apos;./c&apos;</span>;

<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> <span class="hljs-string">&apos;a.js&apos;</span>;
<span class="hljs-built_in">console</span>.log(a);
</code></pre>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="
// c.js

export default 333;
" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="javascript hljs"><code class="javascript">
<span class="hljs-comment">// c.js</span>

<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> <span class="hljs-number">333</span>;
</code></pre>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="(function(modules) {

  
  function __webpack_require__(moduleId) {
    var module =  {
      i: moduleId,
      l: false,
      exports: {}
    };
    modules[moduleId].call(module.exports, module, module.exports, __webpack_require__);
    return module.exports;
  }

  return __webpack_require__(0);
})([
  (function (module, __webpack_exports__, __webpack_require__) {

    // &#x5F15;&#x7528; &#x6A21;&#x5757; 1
    &quot;use strict&quot;;
    Object.defineProperty(__webpack_exports__, &quot;__esModule&quot;, { value: true });
    /* harmony import */ var __WEBPACK_IMPORTED_MODULE_0__c__ = __webpack_require__(1);

/* harmony default export */ __webpack_exports__[&quot;default&quot;] = (&apos;a.js&apos;);
console.log(__WEBPACK_IMPORTED_MODULE_0__c__[&quot;a&quot; /* default */]);

  }),
  (function (module, __webpack_exports__, __webpack_require__) {

    // &#x8F93;&#x51FA;&#x672C;&#x6A21;&#x5757;&#x7684;&#x6570;&#x636E;
    &quot;use strict&quot;;
    /* harmony default export */ __webpack_exports__[&quot;a&quot;] = (333);
  })
]);
" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs javascript"><code>(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">modules</span>) </span>{

  
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">__webpack_require__</span>(<span class="hljs-params">moduleId</span>) </span>{
    <span class="hljs-keyword">var</span> <span class="hljs-built_in">module</span> =  {
      <span class="hljs-attr">i</span>: moduleId,
      <span class="hljs-attr">l</span>: <span class="hljs-literal">false</span>,
      <span class="hljs-attr">exports</span>: {}
    };
    modules[moduleId].call(<span class="hljs-built_in">module</span>.exports, <span class="hljs-built_in">module</span>, <span class="hljs-built_in">module</span>.exports, __webpack_require__);
    <span class="hljs-keyword">return</span> <span class="hljs-built_in">module</span>.exports;
  }

  <span class="hljs-keyword">return</span> __webpack_require__(<span class="hljs-number">0</span>);
})([
  (<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">module, __webpack_exports__, __webpack_require__</span>) </span>{

    <span class="hljs-comment">// &#x5F15;&#x7528; &#x6A21;&#x5757; 1</span>
<span class="hljs-meta">    &quot;use strict&quot;</span>;
    <span class="hljs-built_in">Object</span>.defineProperty(__webpack_exports__, <span class="hljs-string">&quot;__esModule&quot;</span>, { <span class="hljs-attr">value</span>: <span class="hljs-literal">true</span> });
    <span class="hljs-comment">/* harmony import */</span> <span class="hljs-keyword">var</span> __WEBPACK_IMPORTED_MODULE_0__c__ = __webpack_require__(<span class="hljs-number">1</span>);

<span class="hljs-comment">/* harmony default export */</span> __webpack_exports__[<span class="hljs-string">&quot;default&quot;</span>] = (<span class="hljs-string">&apos;a.js&apos;</span>);
<span class="hljs-built_in">console</span>.log(__WEBPACK_IMPORTED_MODULE_0__c__[<span class="hljs-string">&quot;a&quot;</span> <span class="hljs-comment">/* default */</span>]);

  }),
  (<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">module, __webpack_exports__, __webpack_require__</span>) </span>{

    <span class="hljs-comment">// &#x8F93;&#x51FA;&#x672C;&#x6A21;&#x5757;&#x7684;&#x6570;&#x636E;</span>
<span class="hljs-meta">    &quot;use strict&quot;</span>;
    <span class="hljs-comment">/* harmony default export */</span> __webpack_exports__[<span class="hljs-string">&quot;a&quot;</span>] = (<span class="hljs-number">333</span>);
  })
]);
</code></pre>
<p>&#x4E0A;&#x9762;&#x8FD9;&#x6BB5; js &#x5C31;&#x662F;&#x4F7F;&#x7528; webpack &#x7F16;&#x8BD1;&#x540E;&#x7684;&#x4EE3;&#x7801;&#xFF08;&#x7ECF;&#x8FC7;&#x7CBE;&#x7B80;&#xFF09;&#xFF0C;&#x5176;&#x4E2D;&#x5C31;&#x5305;&#x542B;&#x4E86; webpack&#x7684;&#x8FD0;&#x884C;&#x65F6;&#x4EE3;&#x7801;&#xFF0C;&#x5176;&#x4E2D;&#x5C31;&#x662F;&#x5173;&#x4E8E;&#x6A21;&#x5757;&#x7684;&#x5B9E;&#x73B0;&#x3002;</p>
<p>&#x6211;&#x4EEC;&#x518D;&#x7CBE;&#x7B80;&#x4E0B;&#x4EE3;&#x7801;&#xFF0C;&#x4F1A;&#x53D1;&#x73B0;&#x8FD9;&#x662F;&#x4E2A;&#x81EA;&#x6267;&#x884C;&#x51FD;&#x6570;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="(function(modules) {

})([]);
" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs clojure"><code>(<span class="hljs-name">function</span>(<span class="hljs-name">modules</span>) {

})([])<span class="hljs-comment">;</span>
</code></pre>
<p>&#x81EA;&#x6267;&#x884C;&#x51FD;&#x6570;&#x7684;&#x5165;&#x53C2;&#x662F;&#x4E2A;&#x6570;&#x7EC4;&#xFF0C;&#x8FD9;&#x4E2A;&#x6570;&#x7EC4;&#x5305;&#x542B;&#x4E86;&#x6240;&#x6709;&#x7684;&#x6A21;&#x5757;&#xFF0C;&#x5305;&#x88F9;&#x5728;&#x51FD;&#x6570;&#x4E2D;&#x3002;</p>
<p>&#x81EA;&#x6267;&#x884C;&#x51FD;&#x6570;&#x4F53;&#x91CC;&#x7684;&#x903B;&#x8F91;&#x5C31;&#x662F;&#x5904;&#x7406;&#x6A21;&#x5757;&#x7684;&#x903B;&#x8F91;&#x3002;&#x5173;&#x952E;&#x5728;&#x4E8E; <code>__webpack_require__</code> &#x51FD;&#x6570;&#xFF0C;&#x8FD9;&#x4E2A;&#x51FD;&#x6570;&#x5C31;&#x662F; <code>require</code> &#x6216;&#x8005;&#x662F; <code>import</code> &#x7684;&#x66FF;&#x4EE3;&#xFF0C;&#x6211;&#x4EEC;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x5728;&#x51FD;&#x6570;&#x4F53;&#x5185;&#x5148;&#x5B9A;&#x4E49;&#x4E86;&#x8FD9;&#x4E2A;&#x51FD;&#x6570;&#xFF0C;&#x7136;&#x540E;&#x8C03;&#x7528;&#x4E86;&#x4ED6;&#x3002;&#x8FD9;&#x91CC;&#x4F1A;&#x4F20;&#x5165;&#x4E00;&#x4E2A; <code>moduleId</code>&#xFF0C;&#x8FD9;&#x4E2A;&#x4F8B;&#x5B50;&#x4E2D;&#x662F;0&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&#x6211;&#x4EEC;&#x7684;&#x5165;&#x53E3;&#x6A21;&#x5757; <code>a.js</code> &#x7684;&#x5185;&#x5BB9;&#x3002;</p>
<p>&#x6211;&#x4EEC;&#x518D;&#x770B; <code>__webpack_require__</code> &#x5185;&#x6267;&#x884C;&#x4E86;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="modules[moduleId].call(module.exports, module, module.exports, __webpack_require__);
return module.exports&#xFF1B;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs java"><code>modules[moduleId].call(<span class="hljs-keyword">module</span>.<span class="hljs-keyword">exports</span>, <span class="hljs-keyword">module</span>, <span class="hljs-keyword">module</span>.<span class="hljs-keyword">exports</span>, __webpack_require__);
<span class="hljs-keyword">return</span> <span class="hljs-keyword">module</span>.<span class="hljs-keyword">exports</span>&#xFF1B;</code></pre>
<p>&#x5373;&#x4ECE;&#x5165;&#x53C2;&#x7684; modules &#x6570;&#x7EC4;&#x4E2D;&#x53D6;&#x7B2C;&#x4E00;&#x4E2A;&#x51FD;&#x6570;&#x8FDB;&#x884C;&#x8C03;&#x7528;&#xFF0C;&#x5E76;&#x5165;&#x53C2;</p>
<ul>
<li>module</li>
<li>module.exports</li>
<li><strong>webpack_require</strong></li>
</ul>
<p>&#x6211;&#x4EEC;&#x518D;&#x770B;&#x7B2C;&#x4E00;&#x4E2A;&#x51FD;&#x6570;&#xFF08;&#x5373;&#x5165;&#x53E3;&#x6A21;&#x5757;&#xFF09;&#x7684;&#x903B;&#x8F91;&#xFF08;&#x7CBE;&#x7B80;&#xFF09;&#xFF1A;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="function (module, __webpack_exports__, __webpack_require__) {

/* harmony import */ var __WEBPACK_IMPORTED_MODULE_0__c__ = __webpack_require__(1);

    /* harmony default export */ __webpack_exports__[&quot;default&quot;] = (&apos;a.js&apos;);
    console.log(__WEBPACK_IMPORTED_MODULE_0__c__[&quot;a&quot; /* default */]);

  }" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs sqf"><code>function (module, <span class="hljs-variable">__webpack_exports__</span>, <span class="hljs-variable">__webpack_require__</span>) {

<span class="hljs-comment">/* harmony import */</span> var <span class="hljs-variable">__WEBPACK_IMPORTED_MODULE_0__c__</span> = <span class="hljs-variable">__webpack_require__</span>(<span class="hljs-number">1</span>);

    <span class="hljs-comment">/* harmony default export */</span> <span class="hljs-variable">__webpack_exports__</span>[<span class="hljs-string">&quot;default&quot;</span>] = (<span class="hljs-string">&apos;a.js&apos;</span>);
    console.<span class="hljs-built_in">log</span>(<span class="hljs-variable">__WEBPACK_IMPORTED_MODULE_0__c__</span>[<span class="hljs-string">&quot;a&quot;</span> <span class="hljs-comment">/* default */</span>]);

  }</code></pre>
<p>&#x6211;&#x4EEC;&#x53EF;&#x4EE5;&#x770B;&#x5230;&#x5165;&#x53E3;&#x6A21;&#x5757;&#x53C8;&#x8C03;&#x7528;&#x4E86; <code>__webpack_require__(1)</code> &#x53BB;&#x5F15;&#x7528;&#x5165;&#x53C2;&#x6570;&#x7EC4;&#x91CC;&#x7684;&#x7B2C;2&#x4E2A;&#x51FD;&#x6570;&#x3002;</p>
<p>&#x7136;&#x540E;&#x4F1A;&#x5C06;&#x5165;&#x53C2;&#x7684; <code>__webpack_exports__</code> &#x5BF9;&#x8C61;&#x6DFB;&#x52A0; <code>default</code> &#x5C5E;&#x6027;&#xFF0C;&#x5E76;&#x8D4B;&#x503C;&#x3002;</p>
<p>&#x8FD9;&#x91CC;&#x6211;&#x4EEC;&#x5C31;&#x80FD;&#x770B;&#x5230;&#x6A21;&#x5757;&#x5316;&#x7684;&#x5B9E;&#x73B0;&#x539F;&#x7406;&#xFF0C;&#x8FD9;&#x91CC;&#x7684; <code>__webpack_exports__</code> &#x5C31;&#x662F;&#x8FD9;&#x4E2A;&#x6A21;&#x5757;&#x7684; <code>module.exports</code> &#x901A;&#x8FC7;&#x5BF9;&#x8C61;&#x7684;&#x5F15;&#x7528;&#x4F20;&#x53C2;&#xFF0C;&#x95F4;&#x63A5;&#x7684;&#x7ED9; module.exports &#x6DFB;&#x52A0;&#x5C5E;&#x6027;&#x3002;</p>
<p>&#x6700;&#x540E;&#x4F1A;&#x5C06; module.exports return &#x51FA;&#x6765;&#x3002;&#x5C31;&#x5B8C;&#x6210;&#x4E86; <code>__webpack_require__</code> &#x51FD;&#x6570;&#x7684;&#x4F7F;&#x547D;&#x3002;</p>
<p>&#x6BD4;&#x5982;&#x5728;&#x5165;&#x53E3;&#x6A21;&#x5757;&#x4E2D;&#x53C8;&#x8C03;&#x7528;&#x4E86; <code>__webpack_require__(1)</code>&#xFF0C;&#x5C31;&#x4F1A;&#x5F97;&#x5230;&#x8FD9;&#x4E2A;&#x6A21;&#x5757;&#x8FD4;&#x56DE;&#x7684; <code>module.exports</code>&#x3002;</p>
<p><strong>&#x4F46;&#x5728;&#x8FD9;&#x4E2A;&#x81EA;&#x6267;&#x884C;&#x51FD;&#x6570;&#x7684;&#x5E95;&#x90E8;&#xFF0C;<code>webpack</code> &#x4F1A;&#x5C06;&#x5165;&#x53E3;&#x6A21;&#x5757;&#x7684;&#x8F93;&#x51FA;&#x4E5F;&#x8FDB;&#x884C;&#x8FD4;&#x56DE; </strong></p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="return __webpack_require__(0);" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs aspectj"><code style="word-break: break-word; white-space: initial;"><span class="hljs-function"><span class="hljs-keyword">return</span> <span class="hljs-title">__webpack_require__</span><span class="hljs-params">(<span class="hljs-number">0</span>)</span></span>;</code></pre>
<p>&#x76EE;&#x524D;&#x8FD9;&#x79CD;&#x7F16;&#x8BD1;&#x540E;&#x7684;js&#xFF0C;&#x5C06;&#x5165;&#x53E3;&#x6A21;&#x5757;&#x7684;&#x8F93;&#x51FA;&#xFF08;&#x5373; <code>module.exports</code>&#xFF09; &#x8FDB;&#x884C;&#x8F93;&#x51FA;&#x6CA1;&#x6709;&#x4EFB;&#x4F55;&#x4F5C;&#x7528;&#xFF0C;&#x53EA;&#x4F1A;&#x4F5C;&#x7528;&#x4E8E;&#x5F53;&#x524D;&#x4F5C;&#x7528;&#x57DF;&#x3002;&#x8FD9;&#x4E2A;js&#x5E76;&#x4E0D;&#x80FD;&#x88AB;&#x5176;&#x4ED6;&#x6A21;&#x5757;&#x7EE7;&#x7EED;&#x4EE5; <code>require</code> &#x6216; <code>import</code> &#x7684;&#x65B9;&#x5F0F;&#x5F15;&#x7528;&#x3002;</p>
<h3 id="articleHeader3">babel &#x7684;&#x4F5C;&#x7528;</h3>
<p>&#x6309;&#x7406;&#x8BF4; webpack &#x7684;&#x6A21;&#x5757;&#x5316;&#x65B9;&#x6848;&#x5DF2;&#x7ECF;&#x5F88;&#x597D;&#x7684;&#x5C06;es6 &#x6A21;&#x5757;&#x5316;&#x8F6C;&#x6362;&#x6210; webpack &#x7684;&#x6A21;&#x5757;&#x5316;&#xFF0C;&#x4F46;&#x662F;&#x5176;&#x4F59;&#x7684; es6 &#x8BED;&#x6CD5;&#x8FD8;&#x9700;&#x8981;&#x505A;&#x517C;&#x5BB9;&#x6027;&#x5904;&#x7406;&#x3002;babel &#x4E13;&#x95E8;&#x7528;&#x4E8E;&#x5904;&#x7406; es6 &#x8F6C;&#x6362; es5&#x3002;&#x5F53;&#x7136;&#x8FD9;&#x4E5F;&#x5305;&#x62EC; es6 &#x7684;&#x6A21;&#x5757;&#x8BED;&#x6CD5;&#x7684;&#x8F6C;&#x6362;&#x3002;</p>
<p><strong>&#x5176;&#x5B9E;&#x4E24;&#x8005;&#x7684;&#x8F6C;&#x6362;&#x601D;&#x8DEF;&#x5DEE;&#x4E0D;&#x591A;&#xFF0C;&#x533A;&#x522B;&#x5728;&#x4E8E; webpack &#x7684;&#x539F;&#x751F;&#x8F6C;&#x6362; &#x53EF;&#x4EE5;&#x591A;&#x505A;&#x4E00;&#x6B65;&#x9759;&#x6001;&#x5206;&#x6790;&#xFF0C;&#x4F7F;&#x7528;tree-shaking &#x6280;&#x672F;&#xFF08;&#x4E0B;&#x9762;&#x4F1A;&#x8BB2;&#x5230;&#xFF09;</strong></p>
<blockquote>babel &#x80FD;&#x63D0;&#x524D;&#x5C06; es6 &#x7684; import &#x7B49;&#x6A21;&#x5757;&#x5173;&#x952E;&#x5B57;&#x8F6C;&#x6362;&#x6210; commonjs &#x7684;&#x89C4;&#x8303;&#x3002;&#x8FD9;&#x6837; webpack &#x5C31;&#x65E0;&#x9700;&#x518D;&#x505A;&#x5904;&#x7406;&#xFF0C;&#x76F4;&#x63A5;&#x4F7F;&#x7528; webpack &#x8FD0;&#x884C;&#x65F6;&#x5B9A;&#x4E49;&#x7684; <code>__webpack_require__</code> &#x5904;&#x7406;&#x3002;</blockquote>
<p>&#x8FD9;&#x91CC;&#x5C31;&#x89E3;&#x91CA;&#x4E86; <strong>&#x95EE;&#x9898;5</strong>&#x3002;</p>
<blockquote>babel &#x5728;&#x6A21;&#x5757;&#x5316;&#x7684;&#x573A;&#x666F;&#x4E2D;&#x5145;&#x5F53;&#x4E86;&#x4EC0;&#x4E48;&#x89D2;&#x8272;&#xFF1F;&#x4EE5;&#x53CA; webpack &#xFF1F;&#x54EA;&#x4E2A;&#x542F;&#x5230;&#x4E86;&#x5173;&#x952E;&#x4F5C;&#x7528;&#xFF1F;</blockquote>
<p>&#x90A3;&#x4E48; babel &#x662F;&#x5982;&#x4F55;&#x8F6C;&#x6362; es6 &#x7684;&#x6A21;&#x5757;&#x8BED;&#x6CD5;&#x5462;&#xFF1F;</p>
<h4>&#x5BFC;&#x51FA;&#x6A21;&#x5757;</h4>
<p>es6 &#x7684;&#x5BFC;&#x51FA;&#x6A21;&#x5757;&#x5199;&#x6CD5;&#x6709;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="export default 123;

export const a = 123;

const b = 3;
const c = 4;
export { b, c };" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs cpp"><code><span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> <span class="hljs-number">123</span>;

<span class="hljs-keyword">export</span> <span class="hljs-keyword">const</span> a = <span class="hljs-number">123</span>;

<span class="hljs-keyword">const</span> b = <span class="hljs-number">3</span>;
<span class="hljs-keyword">const</span> c = <span class="hljs-number">4</span>;
<span class="hljs-keyword">export</span> { b, c };</code></pre>
<p>babel &#x4F1A;&#x5C06;&#x8FD9;&#x4E9B;&#x7EDF;&#x7EDF;&#x8F6C;&#x6362;&#x6210; commonjs &#x7684; exports&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="exports.default = 123;
exports.a = 123;
exports.b = 3;
exports.c = 4;
exports.__esModule = true;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs java"><code><span class="hljs-keyword">exports</span>.<span class="hljs-keyword">default</span> = <span class="hljs-number">123</span>;
<span class="hljs-keyword">exports</span>.a = <span class="hljs-number">123</span>;
<span class="hljs-keyword">exports</span>.b = <span class="hljs-number">3</span>;
<span class="hljs-keyword">exports</span>.c = <span class="hljs-number">4</span>;
<span class="hljs-keyword">exports</span>.__esModule = <span class="hljs-keyword">true</span>;</code></pre>
<p>babel &#x8F6C;&#x6362; es6 &#x7684;&#x6A21;&#x5757;&#x8F93;&#x51FA;&#x903B;&#x8F91;&#x975E;&#x5E38;&#x7B80;&#x5355;&#xFF0C;&#x5373;&#x5C06;&#x6240;&#x6709;&#x8F93;&#x51FA;&#x90FD;&#x8D4B;&#x503C;&#x7ED9; exports&#xFF0C;&#x5E76;&#x5E26;&#x4E0A;&#x4E00;&#x4E2A;&#x6807;&#x5FD7; <code>__esModule</code> &#x8868;&#x660E;&#x8FD9;&#x662F;&#x4E2A;&#x7531; es6 &#x8F6C;&#x6362;&#x6765;&#x7684; commonjs &#x8F93;&#x51FA;&#x3002;</p>
<p>babel&#x5C06;&#x6A21;&#x5757;&#x7684;&#x5BFC;&#x51FA;&#x8F6C;&#x6362;&#x4E3A;commonjs&#x89C4;&#x8303;&#x540E;&#xFF0C;&#x4E5F;&#x4F1A;&#x5C06;&#x5F15;&#x5165; import &#x4E5F;&#x8F6C;&#x6362;&#x4E3A; commonjs &#x89C4;&#x8303;&#x3002;&#x5373;&#x91C7;&#x7528; require &#x53BB;&#x5F15;&#x7528;&#x6A21;&#x5757;&#xFF0C;&#x518D;&#x52A0;&#x4EE5;&#x4E00;&#x5B9A;&#x7684;&#x5904;&#x7406;&#xFF0C;&#x7B26;&#x5408;es6&#x7684;&#x4F7F;&#x7528;&#x610F;&#x56FE;&#x3002;</p>
<h4>&#x5F15;&#x5165; default</h4>
<p>&#x5BF9;&#x4E8E;&#x6700;&#x5E38;&#x89C1;&#x7684;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="import a from &apos;./a.js&apos;;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs clean"><code style="word-break: break-word; white-space: initial;"><span class="hljs-keyword">import</span> a <span class="hljs-keyword">from</span> <span class="hljs-string">&apos;./a.js&apos;</span>;</code></pre>
<p>&#x5728;es6&#x4E2D; import a from &apos;./a.js&apos; &#x7684;&#x672C;&#x610F;&#x662F;&#x60F3;&#x53BB;&#x5F15;&#x5165;&#x4E00;&#x4E2A; es6 &#x6A21;&#x5757;&#x4E2D;&#x7684; default &#x8F93;&#x51FA;&#x3002;</p>
<p>&#x901A;&#x8FC7;babel&#x8F6C;&#x6362;&#x540E;&#x5F97;&#x5230; <code>var a = require(./a.js)</code> &#x5F97;&#x5230;&#x7684;&#x5BF9;&#x8C61;&#x5374;&#x662F;&#x6574;&#x4E2A;&#x5BF9;&#x8C61;&#xFF0C;&#x80AF;&#x5B9A;&#x4E0D;&#x662F; es6 &#x8BED;&#x53E5;&#x7684;&#x672C;&#x610F;&#xFF0C;&#x6240;&#x4EE5;&#x9700;&#x8981;&#x5BF9; a &#x505A;&#x4E9B;&#x6539;&#x53D8;&#x3002;</p>
<p>&#x6211;&#x4EEC;&#x5728;&#x5BFC;&#x51FA;&#x63D0;&#x5230;&#xFF0C;default &#x8F93;&#x51FA;&#x4F1A;&#x8D4B;&#x503C;&#x7ED9;&#x5BFC;&#x51FA;&#x5BF9;&#x8C61;&#x7684;default&#x5C5E;&#x6027;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="exports.default = 123;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs delphi"><code style="word-break: break-word; white-space: initial;"><span class="hljs-keyword">exports</span>.<span class="hljs-keyword">default</span> = <span class="hljs-number">123</span>;</code></pre>
<p>&#x6240;&#x4EE5; babel &#x52A0;&#x4E86;&#x4E2A; help  <code>_interopRequireDefault</code> &#x51FD;&#x6570;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="function _interopRequireDefault(obj) {
    return obj &amp;&amp; obj.__esModule
        ? obj
        : { &apos;default&apos;: obj };
}

var _a = require(&apos;assert&apos;);
var _a2 = _interopRequireDefault(_a);

var a = _a2[&apos;default&apos;];" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs javascript"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">_interopRequireDefault</span>(<span class="hljs-params">obj</span>) </span>{
    <span class="hljs-keyword">return</span> obj &amp;&amp; obj.__esModule
        ? obj
        : { <span class="hljs-string">&apos;default&apos;</span>: obj };
}

<span class="hljs-keyword">var</span> _a = <span class="hljs-built_in">require</span>(<span class="hljs-string">&apos;assert&apos;</span>);
<span class="hljs-keyword">var</span> _a2 = _interopRequireDefault(_a);

<span class="hljs-keyword">var</span> a = _a2[<span class="hljs-string">&apos;default&apos;</span>];</code></pre>
<p>&#x6240;&#x4EE5;&#x8FD9;&#x91CC;&#x6700;&#x540E;&#x7684; a &#x53D8;&#x91CF;&#x5C31;&#x662F; require &#x7684;&#x503C;&#x7684; default &#x5C5E;&#x6027;&#x3002;&#x5982;&#x679C;&#x539F;&#x5148;&#x5C31;&#x662F;commonjs&#x89C4;&#x8303;&#x7684;&#x6A21;&#x5757;&#xFF0C;&#x90A3;&#x4E48;&#x5C31;&#x662F;&#x90A3;&#x4E2A;&#x6A21;&#x5757;&#x7684;&#x5BFC;&#x51FA;&#x5BF9;&#x8C61;&#x3002;</p>
<h4>&#x5F15;&#x5165; * &#x901A;&#x914D;&#x7B26;</h4>
<p>&#x6211;&#x4EEC;&#x4F7F;&#x7528; <code>import * as a from &apos;./a.js&apos;</code> es6&#x8BED;&#x6CD5;&#x7684;&#x672C;&#x610F;&#x662F;&#x60F3;&#x5C06; es6 &#x6A21;&#x5757;&#x7684;&#x6240;&#x6709;&#x547D;&#x540D;&#x8F93;&#x51FA;&#x4EE5;&#x53CA;defalut&#x8F93;&#x51FA;&#x6253;&#x5305;&#x6210;&#x4E00;&#x4E2A;&#x5BF9;&#x8C61;&#x8D4B;&#x503C;&#x7ED9;a&#x53D8;&#x91CF;&#x3002;</p>
<p>&#x5DF2;&#x77E5;&#x4EE5; commonjs &#x89C4;&#x8303;&#x5BFC;&#x51FA;&#xFF1A;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="exports.default = 123;
exports.a = 123;
exports.b = 3;
exports.__esModule = true;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs java"><code><span class="hljs-keyword">exports</span>.<span class="hljs-keyword">default</span> = <span class="hljs-number">123</span>;
<span class="hljs-keyword">exports</span>.a = <span class="hljs-number">123</span>;
<span class="hljs-keyword">exports</span>.b = <span class="hljs-number">3</span>;
<span class="hljs-keyword">exports</span>.__esModule = <span class="hljs-keyword">true</span>;</code></pre>
<p>&#x90A3;&#x4E48;&#x5BF9;&#x4E8E; es6 &#x8F6C;&#x6362;&#x6765;&#x7684;&#x8F93;&#x51FA;&#x901A;&#x8FC7; <code>var a = require(&apos;./a.js&apos;)</code> &#x5BFC;&#x5165;&#x8FD9;&#x4E2A;&#x5BF9;&#x8C61;&#x5C31;&#x5DF2;&#x7ECF;&#x7B26;&#x5408;&#x610F;&#x56FE;&#x3002;</p>
<p>&#x6240;&#x4EE5;&#x76F4;&#x63A5;&#x8FD4;&#x56DE;&#x8FD9;&#x4E2A;&#x5BF9;&#x8C61;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="if (obj &amp;&amp; obj.__esModule) {
   return obj;
}" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs kotlin"><code><span class="hljs-keyword">if</span> (obj &amp;&amp; obj.__esModule) {
   <span class="hljs-keyword">return</span> obj;
}</code></pre>
<p>&#x5982;&#x679C;&#x672C;&#x6765;&#x5C31;&#x662F; commonjs &#x89C4;&#x8303;&#x7684;&#x6A21;&#x5757;&#xFF0C;&#x5BFC;&#x51FA;&#x65F6;&#x6CA1;&#x6709;default&#x5C5E;&#x6027;&#xFF0C;&#x9700;&#x8981;&#x6DFB;&#x52A0;&#x4E00;&#x4E2A;default&#x5C5E;&#x6027;&#xFF0C;&#x5E76;&#x628A;&#x6574;&#x4E2A;&#x6A21;&#x5757;&#x5BF9;&#x8C61;&#x518D;&#x6B21;&#x8D4B;&#x503C;&#x7ED9;default&#x5C5E;&#x6027;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="function _interopRequireWildcard(obj) {
    if (obj &amp;&amp; obj.__esModule) {
        return obj;
    }
    else {
        var newObj = {}; // (A)
        if (obj != null) {
            for (var key in obj) {
                if (Object.prototype.hasOwnProperty.call(obj, key))
                    newObj[key] = obj[key];
            }
        }
        newObj.default = obj;
        return newObj;
    }
}" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs javascript"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">_interopRequireWildcard</span>(<span class="hljs-params">obj</span>) </span>{
    <span class="hljs-keyword">if</span> (obj &amp;&amp; obj.__esModule) {
        <span class="hljs-keyword">return</span> obj;
    }
    <span class="hljs-keyword">else</span> {
        <span class="hljs-keyword">var</span> newObj = {}; <span class="hljs-comment">// (A)</span>
        <span class="hljs-keyword">if</span> (obj != <span class="hljs-literal">null</span>) {
            <span class="hljs-keyword">for</span> (<span class="hljs-keyword">var</span> key <span class="hljs-keyword">in</span> obj) {
                <span class="hljs-keyword">if</span> (<span class="hljs-built_in">Object</span>.prototype.hasOwnProperty.call(obj, key))
                    newObj[key] = obj[key];
            }
        }
        newObj.default = obj;
        <span class="hljs-keyword">return</span> newObj;
    }
}</code></pre>
<h4>import { a } from &apos;./a.js&apos;</h4>
<p>&#x76F4;&#x63A5;&#x8F6C;&#x6362;&#x6210; <code>require(&apos;./a.js&apos;).a</code> &#x5373;&#x53EF;&#x3002;</p>
<h4>&#x603B;&#x7ED3;</h4>
<p>&#x7ECF;&#x8FC7;&#x4E0A;&#x9762;&#x7684;&#x8F6C;&#x6362;&#x5206;&#x6790;&#xFF0C;&#x6211;&#x4EEC;&#x5F97;&#x77E5;&#x5373;&#x4F7F;&#x6211;&#x4EEC;&#x4F7F;&#x7528;&#x4E86; es6 &#x7684;&#x6A21;&#x5757;&#x7CFB;&#x7EDF;&#xFF0C;&#x5982;&#x679C;&#x501F;&#x52A9; babel &#x7684;&#x8F6C;&#x6362;&#xFF0C;es6 &#x7684;&#x6A21;&#x5757;&#x7CFB;&#x7EDF;&#x6700;&#x7EC8;&#x8FD8;&#x662F;&#x4F1A;&#x8F6C;&#x6362;&#x6210; commonjs &#x7684;&#x89C4;&#x8303;&#x3002;&#x6240;&#x4EE5;&#x6211;&#x4EEC;&#x5982;&#x679C;&#x662F;&#x4F7F;&#x7528; babel &#x8F6C;&#x6362; es6 &#x6A21;&#x5757;&#xFF0C;&#x6DF7;&#x5408;&#x4F7F;&#x7528; es6 &#x7684;&#x6A21;&#x5757;&#x548C; commonjs &#x7684;&#x89C4;&#x8303;&#x662F;&#x6CA1;&#x6709;&#x95EE;&#x9898;&#x7684;&#xFF0C;&#x56E0;&#x4E3A;&#x6700;&#x7EC8;&#x90FD;&#x4F1A;&#x8F6C;&#x6362;&#x6210; commonjs&#x3002;</p>
<p><strong>&#x8FD9;&#x91CC;&#x89E3;&#x91CA;&#x4E86;&#x95EE;&#x9898;3</strong></p>
<blockquote>&#x4E3A;&#x4EC0;&#x4E48;&#x53EF;&#x4EE5;&#x4F7F;&#x7528; es6 &#x7684; import &#x53BB;&#x5F15;&#x7528; commonjs &#x89C4;&#x8303;&#x5B9A;&#x4E49;&#x7684;&#x6A21;&#x5757;&#xFF0C;&#x6216;&#x8005;&#x53CD;&#x8FC7;&#x6765;&#x4E5F;&#x53EF;&#x4EE5;&#x53C8;&#x662F;&#x4E3A;&#x4EC0;&#x4E48;&#xFF1F;</blockquote>
<h3 id="articleHeader4">babel5 &amp; babel6</h3>
<p>&#x6211;&#x4EEC;&#x5728;&#x4E0A;&#x6587; babel &#x5BF9;&#x5BFC;&#x51FA;&#x6A21;&#x5757;&#x7684;&#x8F6C;&#x6362;&#x63D0;&#x5230;&#xFF0C;es6 &#x7684; <code>export default</code> &#x90FD;&#x4F1A;&#x88AB;&#x8F6C;&#x6362;&#x6210; <code>exports.default</code>&#xFF0C;&#x5373;&#x4F7F;&#x8FD9;&#x4E2A;&#x6A21;&#x5757;&#x53EA;&#x6709;&#x8FD9;&#x4E00;&#x4E2A;&#x8F93;&#x51FA;&#x3002;</p>
<p><strong>&#x8FD9;&#x4E5F;&#x89E3;&#x91CA;&#x4E86;&#x95EE;&#x9898;1</strong></p>
<blockquote>&#x4E3A;&#x4F55;&#x6709;&#x7684;&#x5730;&#x65B9;&#x4F7F;&#x7528; <code>require</code> &#x53BB;&#x5F15;&#x7528;&#x4E00;&#x4E2A;&#x6A21;&#x5757;&#x65F6;&#x9700;&#x8981;&#x52A0;&#x4E0A; <code>default</code>&#xFF1F; <code>require(&apos;xx&apos;).default</code>
</blockquote>
<p>&#x6211;&#x4EEC;&#x7ECF;&#x5E38;&#x4F1A;&#x4F7F;&#x7528; es6 &#x7684; export default &#x6765;&#x8F93;&#x51FA;&#x6A21;&#x5757;&#xFF0C;&#x800C;&#x4E14;&#x8FD9;&#x4E2A;&#x8F93;&#x51FA;&#x662F;&#x8FD9;&#x4E2A;&#x6A21;&#x5757;&#x7684;&#x552F;&#x4E00;&#x8F93;&#x51FA;&#xFF0C;&#x6211;&#x4EEC;&#x4F1A;&#x8BEF;&#x4EE5;&#x4E3A;&#x8FD9;&#x79CD;&#x5199;&#x6CD5;&#x8F93;&#x51FA;&#x7684;&#x662F;&#x6A21;&#x5757;&#x7684;&#x9ED8;&#x8BA4;&#x8F93;&#x51FA;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="// a.js

export default 123;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs cpp"><code><span class="hljs-comment">// a.js</span>

<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> <span class="hljs-number">123</span>;</code></pre>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="// b.js &#x9519;&#x8BEF;

var foo = require(&apos;./a.js&apos;)" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs javascript"><code><span class="hljs-comment">// b.js &#x9519;&#x8BEF;</span>

<span class="hljs-keyword">var</span> foo = <span class="hljs-built_in">require</span>(<span class="hljs-string">&apos;./a.js&apos;</span>)</code></pre>
<p>&#x5728;&#x4F7F;&#x7528; <code>require</code> &#x8FDB;&#x884C;&#x5F15;&#x7528;&#x65F6;&#xFF0C;&#x6211;&#x4EEC;&#x4E5F;&#x4F1A;&#x8BEF;&#x4EE5;&#x4E3A;&#x5F15;&#x5165;&#x7684;&#x662F;a&#x6587;&#x4EF6;&#x7684;&#x9ED8;&#x8BA4;&#x8F93;&#x51FA;&#x3002;</p>
<p>&#x7ED3;&#x679C;&#x8FD9;&#x91CC;&#x9700;&#x8981;&#x6539;&#x6210; <code>var foo = require(&apos;./a.js&apos;).default</code></p>
<p>&#x8FD9;&#x4E2A;&#x573A;&#x666F;&#x5728;&#x5199; webpack &#x4EE3;&#x7801;&#x5206;&#x5272;&#x903B;&#x8F91;&#x65F6;&#x7ECF;&#x5E38;&#x4F1A;&#x9047;&#x5230;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="require.ensure([], (require) =&gt; {
   callback(null, [
     require(&apos;./src/pages/profitList&apos;).default,
   ]);
 });" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs coffeescript"><code><span class="hljs-built_in">require</span>.ensure([], <span class="hljs-function"><span class="hljs-params">(<span class="hljs-built_in">require</span>)</span> =&gt;</span> {
   callback(<span class="hljs-literal">null</span>, [
     <span class="hljs-built_in">require</span>(<span class="hljs-string">&apos;./src/pages/profitList&apos;</span>).<span class="hljs-keyword">default</span>,
   ]);
 });</code></pre>
<p>&#x8FD9;&#x662F; babel6 &#x7684;&#x53D8;&#x66F4;&#xFF0C;&#x5728; babel5 &#x7684;&#x65F6;&#x5019;&#x53EF;&#x4E0D;&#x662F;&#x8FD9;&#x6837;&#x7684;&#x3002;</p>
<p><span class="img-wrap"><img data-src="/img/remote/1460000012386581?w=1694&amp;h=336" src="https://static.alili.tech/v-5bbf1b3b/global/img/squares.svg" alt="" title="" style="cursor: pointer;"></span></p>
<p><a href="http://babeljs.io/docs/plugins/transform-es2015-modules-commonjs/#strict" rel="nofollow noreferrer" target="_blank">http://babeljs.io/docs/plugin...</a></p>
<p>&#x5728; babel5 &#x65F6;&#x4EE3;&#xFF0C;&#x5927;&#x90E8;&#x5206;&#x4EBA;&#x5728;&#x7528; require &#x53BB;&#x5F15;&#x7528; es6 &#x8F93;&#x51FA;&#x7684; default&#xFF0C;&#x53EA;&#x662F;&#x628A; default &#x8F93;&#x51FA;&#x770B;&#x4F5C;&#x662F;&#x4E00;&#x4E2A;&#x6A21;&#x5757;&#x7684;&#x9ED8;&#x8BA4;&#x8F93;&#x51FA;&#xFF0C;&#x6240;&#x4EE5; babel5 &#x5BF9;&#x8FD9;&#x4E2A;&#x903B;&#x8F91;&#x505A;&#x4E86; hack&#xFF0C;&#x5982;&#x679C;&#x4E00;&#x4E2A; es6 &#x6A21;&#x5757;&#x53EA;&#x6709;&#x4E00;&#x4E2A; default &#x8F93;&#x51FA;&#xFF0C;&#x90A3;&#x4E48;&#x5728;&#x8F6C;&#x6362;&#x6210; commonjs &#x7684;&#x65F6;&#x5019;&#x4E5F;&#x4E00;&#x8D77;&#x8D4B;&#x503C;&#x7ED9; <code>module.exports</code>&#xFF0C;&#x5373;&#x6574;&#x4E2A;&#x5BFC;&#x51FA;&#x5BF9;&#x8C61;&#x88AB;&#x8D4B;&#x503C;&#x4E86; default &#x6240;&#x5BF9;&#x5E94;&#x7684;&#x503C;&#x3002;</p>
<p>&#x8FD9;&#x6837;&#x5C31;&#x4E0D;&#x9700;&#x8981;&#x52A0; default&#xFF0C;<code>require(&apos;./a.js&apos;)</code> &#x7684;&#x503C;&#x5C31;&#x662F;&#x60F3;&#x8981;&#x7684; default&#x503C;&#x3002;</p>
<p>&#x4F46;&#x8FD9;&#x6837;&#x505A;&#x662F;&#x4E0D;&#x7B26;&#x5408; es6 &#x7684;&#x5B9A;&#x4E49;&#x7684;&#xFF0C;&#x5728;es6 &#x7684;&#x5B9A;&#x4E49;&#x91CC;&#xFF0C;default &#x53EA;&#x662F;&#x4E2A;&#x540D;&#x5B57;&#xFF0C;&#x6CA1;&#x6709;&#x4EFB;&#x4F55;&#x610F;&#x4E49;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="export default = 123;
export const a = 123;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs cpp"><code><span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> = <span class="hljs-number">123</span>;
<span class="hljs-keyword">export</span> <span class="hljs-keyword">const</span> a = <span class="hljs-number">123</span>;</code></pre>
<p>&#x8FD9;&#x4E24;&#x8005;&#x542B;&#x4E49;&#x662F;&#x4E00;&#x6837;&#x7684;&#xFF0C;&#x5206;&#x522B;&#x4E3A;&#x8F93;&#x51FA;&#x540D;&#x4E3A; default &#x548C; a &#x7684;&#x53D8;&#x91CF;&#x3002;</p>
<p>&#x8FD8;&#x6709;&#x4E00;&#x4E2A;&#x5F88;&#x91CD;&#x8981;&#x7684;&#x95EE;&#x9898;&#xFF0C;&#x4E00;&#x65E6; a.js &#x6587;&#x4EF6;&#x91CC;&#x53C8;&#x6DFB;&#x52A0;&#x4E86;&#x4E00;&#x4E2A;&#x5177;&#x540D;&#x7684;&#x8F93;&#x51FA;&#xFF0C;&#x90A3;&#x4E48;&#x5F15;&#x5165;&#x65B9;&#x5C31;&#x4F1A;&#x51FA;&#x9EBB;&#x70E6;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="// a.js

export default 123;

export const a = 123; // &#x65B0;&#x589E;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs cpp"><code><span class="hljs-comment">// a.js</span>

<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> <span class="hljs-number">123</span>;

<span class="hljs-keyword">export</span> <span class="hljs-keyword">const</span> a = <span class="hljs-number">123</span>; <span class="hljs-comment">// &#x65B0;&#x589E;</span></code></pre>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="// b.js 

var foo = require(&apos;./a.js&apos;);

// &#x7531;&#x4E4B;&#x524D;&#x7684; &#x8F93;&#x51FA; 123
// &#x53D8;&#x6210; { default: 123, a: 123 }" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs javascript"><code><span class="hljs-comment">// b.js </span>

<span class="hljs-keyword">var</span> foo = <span class="hljs-built_in">require</span>(<span class="hljs-string">&apos;./a.js&apos;</span>);

<span class="hljs-comment">// &#x7531;&#x4E4B;&#x524D;&#x7684; &#x8F93;&#x51FA; 123</span>
<span class="hljs-comment">// &#x53D8;&#x6210; { default: 123, a: 123 }</span></code></pre>
<p>&#x6240;&#x4EE5; babel6 &#x53BB;&#x6389;&#x4E86;&#x8FD9;&#x4E2A;hack&#xFF0C;&#x8FD9;&#x662F;&#x4E2A;&#x6B63;&#x786E;&#x7684;&#x51B3;&#x5B9A;&#xFF0C;&#x5347;&#x7EA7; babel6 &#x540E;&#x4EA7;&#x751F;&#x7684;&#x4E0D;&#x517C;&#x5BB9;&#x95EE;&#x9898; &#x53EF;&#x4EE5;&#x901A;&#x8FC7;&#x5F15;&#x5165; <a href="https://www.npmjs.com/package/babel-plugin-add-module-exports" rel="nofollow noreferrer" target="_blank">babel-plugin-add-module-exports</a> &#x89E3;&#x51B3;&#x3002;</p>
<h2 id="articleHeader5">webpack &#x7F16;&#x8BD1;&#x540E;&#x7684;js&#xFF0C;&#x5982;&#x4F55;&#x518D;&#x88AB;&#x5176;&#x4ED6;&#x6A21;&#x5757;&#x5F15;&#x7528;</h2>
<p>&#x901A;&#x8FC7; webpack &#x6A21;&#x5757;&#x5316;&#x539F;&#x7406;&#x7AE0;&#x8282;&#x7ED9;&#x51FA;&#x7684; webpack &#x914D;&#x7F6E;&#x7F16;&#x8BD1;&#x540E;&#x7684; js &#x662F;&#x65E0;&#x6CD5;&#x88AB;&#x5176;&#x4ED6;&#x6A21;&#x5757;&#x5F15;&#x7528;&#x7684;&#xFF0C;webpack &#x63D0;&#x4F9B;&#x4E86; <code>output.libraryTarget</code> &#x914D;&#x7F6E;&#x6307;&#x5B9A;&#x6784;&#x5EFA;&#x5B8C;&#x7684; js &#x7684;&#x7528;&#x9014;&#x3002;</p>
<h3 id="articleHeader6">&#x9ED8;&#x8BA4; var</h3>
<p>&#x5982;&#x679C;&#x6307;&#x5B9A;&#x4E86; <code>output.library = &apos;test&apos;</code><br>&#x5165;&#x53E3;&#x6A21;&#x5757;&#x8FD4;&#x56DE;&#x7684; module.exports &#x66B4;&#x9732;&#x7ED9;&#x5168;&#x5C40; var test = returned_module_exports</p>
<h3 id="articleHeader7">commonjs</h3>
<p>&#x5982;&#x679C;library: &apos;spon-ui&apos; &#x5165;&#x53E3;&#x6A21;&#x5757;&#x8FD4;&#x56DE;&#x7684; module.exports &#x8D4B;&#x503C;&#x7ED9; exports[&apos;spon-ui&apos;]</p>
<h3 id="articleHeader8">commonjs2</h3>
<p>&#x5165;&#x53E3;&#x6A21;&#x5757;&#x8FD4;&#x56DE;&#x7684; module.exports &#x8D4B;&#x503C;&#x7ED9; module.exports </p>
<p>&#x6240;&#x4EE5; element-ui &#x7684;&#x6784;&#x5EFA;&#x65B9;&#x5F0F;&#x91C7;&#x7528; commonjs2 &#xFF0C;&#x5BFC;&#x51FA;&#x7684;&#x7EC4;&#x4EF6;&#x7684;js &#x6700;&#x540E;&#x90FD;&#x4F1A;&#x8D4B;&#x503C;&#x7ED9; module.exports&#xFF0C;&#x4F9B;&#x5176;&#x4ED6;&#x6A21;&#x5757;&#x5F15;&#x7528;&#x3002;</p>
<p><span class="img-wrap"><img data-src="/img/remote/1460000012386582?w=1380&amp;h=474" src="https://static.alili.tech/v-5bbf1b3b/global/img/squares.svg" alt="" title="" style="cursor: pointer; display: inline;"></span></p>
<p><strong>&#x8FD9;&#x91CC;&#x89E3;&#x91CA;&#x4E86;&#x95EE;&#x9898;4</strong></p>
<blockquote>&#x6211;&#x4EEC;&#x5728;&#x6D4F;&#x89C8;&#x4E00;&#x4E9B; npm &#x4E0B;&#x8F7D;&#x4E0B;&#x6765;&#x7684; UI &#x7EC4;&#x4EF6;&#x6A21;&#x5757;&#x65F6;&#xFF08;&#x6BD4;&#x5982;&#x8BF4; element-ui &#x7684; lib &#x6587;&#x4EF6;&#x4E0B;&#xFF09;&#xFF0C;&#x770B;&#x5230;&#x7684;&#x90FD;&#x662F; webpack &#x7F16;&#x8BD1;&#x597D;&#x7684; js &#x6587;&#x4EF6;&#xFF0C;&#x53EF;&#x4EE5;&#x4F7F;&#x7528; import &#x6216; require &#x518D;&#x53BB;&#x5F15;&#x7528;&#x3002;&#x4F46;&#x662F;&#x6211;&#x4EEC;&#x5E73;&#x65F6;&#x7F16;&#x8BD1;&#x597D;&#x7684; js &#x662F;&#x65E0;&#x6CD5;&#x518D;&#x88AB;&#x5176;&#x4ED6;&#x6A21;&#x5757; import &#x7684;&#xFF0C;&#x8FD9;&#x662F;&#x4E3A;&#x4EC0;&#x4E48;&#xFF1F;</blockquote>
<h2 id="articleHeader9">&#x6A21;&#x5757;&#x4F9D;&#x8D56;&#x7684;&#x4F18;&#x5316;</h2>
<h3 id="articleHeader10">&#x6309;&#x9700;&#x52A0;&#x8F7D;&#x7684;&#x539F;&#x7406;</h3>
<p>&#x6211;&#x4EEC;&#x5728;&#x4F7F;&#x7528;&#x5404;&#x5927; UI &#x7EC4;&#x4EF6;&#x5E93;&#x65F6;&#x90FD;&#x4F1A;&#x88AB;&#x4ECB;&#x7ECD;&#x5230;&#x4E3A;&#x4E86;&#x907F;&#x514D;&#x5F15;&#x5165;&#x5168;&#x90E8;&#x6587;&#x4EF6;&#xFF0C;&#x8BF7;&#x4F7F;&#x7528; <code>babel-plugin-component</code> &#x7B49;babel &#x63D2;&#x4EF6;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="import { Button, Select } from &apos;element-ui&apos;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs clean"><code style="word-break: break-word; white-space: initial;"><span class="hljs-keyword">import</span> { Button, Select } <span class="hljs-keyword">from</span> <span class="hljs-string">&apos;element-ui&apos;</span></code></pre>
<p>&#x7531;&#x524D;&#x6587;&#x53EF;&#x77E5; import &#x4F1A;&#x5148;&#x8F6C;&#x6362;&#x4E3A; commonjs&#xFF0C; &#x5373;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="var a = require(&apos;element-ui&apos;);
var Button = a.Button;
var Select = a.Select;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs ebnf"><code><span class="hljs-attribute">var a</span> = require(<span class="hljs-string">&apos;element-ui&apos;</span>);
<span class="hljs-attribute">var Button</span> = a.Button;
<span class="hljs-attribute">var Select</span> = a.Select;</code></pre>
<p><code>var a = require(&apos;element-ui&apos;);</code> &#x8FD9;&#x4E2A;&#x8FC7;&#x7A0B;&#x5C31;&#x4F1A;&#x5C06;&#x6240;&#x6709;&#x7EC4;&#x4EF6;&#x90FD;&#x5F15;&#x5165;&#x8FDB;&#x6765;&#x4E86;&#x3002;</p>
<p>&#x6240;&#x4EE5; <code>babel-plugin-component</code>&#x5C31;&#x505A;&#x4E86;&#x4E00;&#x4EF6;&#x4E8B;&#xFF0C;&#x5C06; <code>import { Button, Select } from &apos;element-ui&apos;</code> &#x8F6C;&#x6362;&#x6210;&#x4E86;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="import Button from &apos;element-ui/lib/button&apos;
import Select from &apos;element-ui/lib/select&apos;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs clean"><code><span class="hljs-keyword">import</span> Button <span class="hljs-keyword">from</span> <span class="hljs-string">&apos;element-ui/lib/button&apos;</span>
<span class="hljs-keyword">import</span> Select <span class="hljs-keyword">from</span> <span class="hljs-string">&apos;element-ui/lib/select&apos;</span></code></pre>
<p>&#x5373;&#x4F7F;&#x8F6C;&#x6362;&#x6210;&#x4E86; commonjs &#x89C4;&#x8303;&#xFF0C;&#x4E5F;&#x53EA;&#x662F;&#x5F15;&#x5165;&#x81EA;&#x5DF1;&#x8FD9;&#x4E2A;&#x7EC4;&#x4EF6;&#x7684;js&#xFF0C;&#x5C06;&#x5F15;&#x5165;&#x91CF;&#x51CF;&#x5C11;&#x5230;&#x6700;&#x4F4E;&#x3002;</p>
<p>&#x6240;&#x4EE5;&#x6211;&#x4EEC;&#x4F1A;&#x770B;&#x5230;&#x51E0;&#x4E4E;&#x6240;&#x6709;&#x7684;UI&#x7EC4;&#x4EF6;&#x5E93;&#x7684;&#x76EE;&#x5F55;&#x5F62;&#x5F0F;&#x90FD;&#x662F;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="|-lib
||--component1
||--component2
||--component3
|-index.common.js" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs crystal"><code>|-<span class="hljs-class"><span class="hljs-keyword">lib</span></span>
||--component1
||--component2
||--component3
|-index.common.js</code></pre>
<p><code>index.common.js</code> &#x7ED9; <code>import element from &apos;element-ui&apos;</code> &#x8FD9;&#x79CD;&#x5F62;&#x5F0F;&#x8C03;&#x7528;&#x5168;&#x90E8;&#x7EC4;&#x4EF6;&#x3002;</p>
<p>lib &#x4E0B;&#x7684;&#x5404;&#x7EC4;&#x4EF6;&#x7528;&#x4E8E;&#x6309;&#x9700;&#x5F15;&#x7528;&#x3002;</p>
<p><strong>&#x8FD9;&#x91CC;&#x89E3;&#x91CA;&#x4E86;&#x95EE;&#x9898;2</strong></p>
<blockquote>&#x7ECF;&#x5E38;&#x5728;&#x5404;&#x5927;UI&#x7EC4;&#x4EF6;&#x5F15;&#x7528;&#x7684;&#x6587;&#x6863;&#x4E0A;&#x4F1A;&#x770B;&#x5230;&#x8BF4;&#x660E; <code>import { button } from &apos;xx-ui&apos;</code> &#x8FD9;&#x6837;&#x4F1A;&#x5F15;&#x5165;&#x6240;&#x6709;&#x7EC4;&#x4EF6;&#x5185;&#x5BB9;&#xFF0C;&#x9700;&#x8981;&#x6DFB;&#x52A0;&#x989D;&#x5916;&#x7684; babel &#x914D;&#x7F6E;&#xFF0C;&#x6BD4;&#x5982; <code>babel-plugin-component</code>&#xFF1F;</blockquote>
<h3 id="articleHeader11">tree-shaking</h3>
<p>webpack2 &#x5F00;&#x59CB;&#x5F15;&#x5165; tree-shaking &#x6280;&#x672F;&#xFF0C;&#x901A;&#x8FC7;&#x9759;&#x6001;&#x5206;&#x6790; es6 &#x7684;&#x8BED;&#x6CD5;&#xFF0C;&#x53EF;&#x4EE5;&#x5220;&#x9664;&#x6CA1;&#x6709;&#x88AB;&#x4F7F;&#x7528;&#x7684;&#x6A21;&#x5757;&#x3002;&#x4ED6;&#x53EA;&#x5BF9; es6 &#x7684;&#x6A21;&#x5757;&#x6709;&#x6548;&#xFF0C;&#x6240;&#x4EE5;&#x4E00;&#x65E6; babel &#x5C06; es6 &#x7684;&#x6A21;&#x5757;&#x8F6C;&#x6362;&#x6210; commonjs&#xFF0C;webpack2 &#x5C06;&#x65E0;&#x6CD5;&#x4F7F;&#x7528;&#x8FD9;&#x9879;&#x4F18;&#x5316;&#x3002;&#x6240;&#x4EE5;&#x8981;&#x4F7F;&#x7528;&#x8FD9;&#x9879;&#x6280;&#x672F;&#xFF0C;&#x6211;&#x4EEC;&#x53EA;&#x80FD;&#x4F7F;&#x7528; webpack &#x7684;&#x6A21;&#x5757;&#x5904;&#x7406;&#xFF0C;&#x52A0;&#x4E0A; babel &#x7684;es6&#x8F6C;&#x6362;&#x80FD;&#x529B;&#xFF08;&#x9700;&#x8981;&#x5173;&#x95ED;&#x6A21;&#x5757;&#x8F6C;&#x6362;&#xFF09;&#x3002;</p>
<p>&#x6700;&#x65B9;&#x4FBF;&#x7684;&#x4F7F;&#x7528;&#x65B9;&#x6CD5;&#x4E3A;&#x4FEE;&#x6539;babel&#x7684;&#x914D;&#x7F6E;&#x3002;</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="use: {
     loader: &apos;babel-loader&apos;,
     options: {
       presets: [[&apos;babel-preset-es2015&apos;, {modules: false}]],
     }
   }" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs less"><code><span class="hljs-attribute">use</span>: {
     <span class="hljs-attribute">loader</span>: <span class="hljs-string">&apos;babel-loader&apos;</span>,
     <span class="hljs-attribute">options</span>: {
       <span class="hljs-attribute">presets</span>: [[<span class="hljs-string">&apos;babel-preset-es2015&apos;</span>, {<span class="hljs-attribute">modules</span>: false}]],
     }
   }</code></pre>
<p>&#x4FEE;&#x6539;&#x6700;&#x5F00;&#x59CB;demo</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="// webpack

const path = require(&apos;path&apos;);

module.exports = {
  entry: &apos;./a.js&apos;,
  output: {
    path: path.resolve(__dirname, &apos;dist&apos;),
    filename: &apos;bundle.js&apos;,
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: &apos;babel-loader&apos;,
          options: {
            presets: [[&apos;babel-preset-es2015&apos;, {modules: false}]],
          }
        }
      }
    ]
  }
};
" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="javascript hljs"><code class="javascript"><span class="hljs-comment">// webpack</span>

<span class="hljs-keyword">const</span> path = <span class="hljs-built_in">require</span>(<span class="hljs-string">&apos;path&apos;</span>);

<span class="hljs-built_in">module</span>.exports = {
  <span class="hljs-attr">entry</span>: <span class="hljs-string">&apos;./a.js&apos;</span>,
  <span class="hljs-attr">output</span>: {
    <span class="hljs-attr">path</span>: path.resolve(__dirname, <span class="hljs-string">&apos;dist&apos;</span>),
    <span class="hljs-attr">filename</span>: <span class="hljs-string">&apos;bundle.js&apos;</span>,
  },
  <span class="hljs-attr">module</span>: {
    <span class="hljs-attr">rules</span>: [
      {
        <span class="hljs-attr">test</span>: <span class="hljs-regexp">/\.js$/</span>,
        <span class="hljs-attr">exclude</span>: <span class="hljs-regexp">/(node_modules|bower_components)/</span>,
        <span class="hljs-attr">use</span>: {
          <span class="hljs-attr">loader</span>: <span class="hljs-string">&apos;babel-loader&apos;</span>,
          <span class="hljs-attr">options</span>: {
            <span class="hljs-attr">presets</span>: [[<span class="hljs-string">&apos;babel-preset-es2015&apos;</span>, {<span class="hljs-attr">modules</span>: <span class="hljs-literal">false</span>}]],
          }
        }
      }
    ]
  }
};
</code></pre>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="
// a.js
import a from &apos;./c&apos;;

export default &apos;a.js&apos;;
console.log(a);
" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="javascript hljs"><code class="javascript">
<span class="hljs-comment">// a.js</span>
<span class="hljs-keyword">import</span> a <span class="hljs-keyword">from</span> <span class="hljs-string">&apos;./c&apos;</span>;

<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> <span class="hljs-string">&apos;a.js&apos;</span>;
<span class="hljs-built_in">console</span>.log(a);
</code></pre>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="
// c.js

export default 333;

const foo = 123;
export { foo };
" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="javascript hljs"><code class="javascript">
<span class="hljs-comment">// c.js</span>

<span class="hljs-keyword">export</span> <span class="hljs-keyword">default</span> <span class="hljs-number">333</span>;

<span class="hljs-keyword">const</span> foo = <span class="hljs-number">123</span>;
<span class="hljs-keyword">export</span> { foo };
</code></pre>
<p>&#x4FEE;&#x6539;&#x7684;&#x70B9;&#x5728;&#x4E8E;&#x589E;&#x52A0;&#x4E86;babel&#xFF0C;&#x5E76;&#x5173;&#x95ED;&#x5176;modules&#x529F;&#x80FD;&#x3002;&#x7136;&#x540E;&#x5728; c.js &#x4E2D;&#x589E;&#x52A0;&#x4E00;&#x4E2A;&#x8F93;&#x51FA; <code>export { foo }</code>&#xFF0C;&#x4F46;&#x662F; a.js &#x4E2D;&#x5E76;&#x4E0D;&#x5F15;&#x7528;&#x5B83;&#x3002;</p>
<p>&#x6700;&#x540E;&#x5728;&#x7F16;&#x8BD1;&#x51FA;&#x7684; js &#x4E2D;&#xFF0C;c.js &#x6A21;&#x5757;&#x5982;&#x4E0B;:</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="
&quot;use strict&quot;;
/* unused harmony export foo */
/* harmony default export */ __webpack_exports__[&quot;a&quot;] = (333);

var foo = 123;" title="" data-original-title="&#x590D;&#x5236;"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span>
      </div>
      </div><pre class="hljs javascript"><code><span class="hljs-meta">
&quot;use strict&quot;</span>;
<span class="hljs-comment">/* unused harmony export foo */</span>
<span class="hljs-comment">/* harmony default export */</span> __webpack_exports__[<span class="hljs-string">&quot;a&quot;</span>] = (<span class="hljs-number">333</span>);

<span class="hljs-keyword">var</span> foo = <span class="hljs-number">123</span>;</code></pre>
<p>foo &#x53D8;&#x91CF;&#x88AB;&#x6807;&#x8BB0;&#x4E3A;&#x6CA1;&#x6709;&#x4F7F;&#x7528;&#xFF0C;&#x5728;&#x6700;&#x540E;&#x538B;&#x7F29;&#x65F6;&#x8FD9;&#x6BB5;&#x4F1A;&#x88AB;&#x5220;&#x9664;&#x3002;</p>
<p>&#x9700;&#x8981;&#x8BF4;&#x660E;&#x7684;&#x662F;&#xFF0C;&#x5373;&#x4F7F;&#x5728; &#x5F15;&#x5165;&#x6A21;&#x5757;&#x65F6;&#x4F7F;&#x7528;&#x4E86; es6 &#xFF0C;&#x4F46;&#x662F;&#x5F15;&#x5165;&#x7684;&#x90A3;&#x4E2A;&#x6A21;&#x5757;&#x5374;&#x662F;&#x4F7F;&#x7528; commonjs &#x8FDB;&#x884C;&#x8F93;&#x51FA;&#xFF0C;&#x8FD9;&#x4E5F;&#x65E0;&#x6CD5;&#x4F7F;&#x7528;tree-shaking&#x3002;</p>
<p>&#x800C;&#x7B2C;&#x4E09;&#x65B9;&#x5E93;&#x5927;&#x591A;&#x662F;&#x9075;&#x5FAA; commonjs &#x89C4;&#x8303;&#x7684;&#xFF0C;&#x8FD9;&#x4E5F;&#x9020;&#x6210;&#x4E86;&#x5F15;&#x5165;&#x7B2C;&#x4E09;&#x65B9;&#x5E93;&#x65E0;&#x6CD5;&#x51CF;&#x5C11;&#x4E0D;&#x5FC5;&#x8981;&#x7684;&#x5F15;&#x5165;&#x3002;</p>
<p>&#x6240;&#x4EE5;&#x5BF9;&#x4E8E;&#x672A;&#x6765;&#x6765;&#x8BF4;&#x7B2C;&#x4E09;&#x65B9;&#x5E93;&#x8981;&#x540C;&#x65F6;&#x53D1;&#x5E03; commonjs &#x683C;&#x5F0F;&#x548C; es6 &#x683C;&#x5F0F;&#x7684;&#x6A21;&#x5757;&#x3002;es6 &#x6A21;&#x5757;&#x7684;&#x5165;&#x53E3;&#x7531; package.json &#x7684;&#x5B57;&#x6BB5; module &#x6307;&#x5B9A;&#x3002;&#x800C; commonjs &#x5219;&#x8FD8;&#x662F;&#x5728; main &#x5B57;&#x6BB5;&#x6307;&#x5B9A;&#x3002;</p>
<p><strong>&#x8FD9;&#x91CC;&#x89E3;&#x91CA;&#x4E86;&#x95EE;&#x9898;6</strong></p>
<blockquote>&#x542C;&#x8BF4; es6 &#x8FD8;&#x6709; <code>tree-shaking</code> &#x529F;&#x80FD;&#xFF0C;&#x600E;&#x4E48;&#x624D;&#x80FD;&#x4F7F;&#x7528;&#x8FD9;&#x4E2A;&#x529F;&#x80FD;&#xFF1F;</blockquote>

                
{% endraw %}

# 版权声明
本文资源来源互联网，仅供学习研究使用，版权归该资源的合法拥有者所有，
本文仅用于学习、研究和交流目的。转载请注明出处、完整链接以及原作者。
原作者若认为本站侵犯了您的版权，请联系我们，我们会立即删除！

## 原文标题
import、require、export、module.exports 混合使用详解

## 原文链接
[https://segmentfault.com/a/1190000012386576](https://segmentfault.com/a/1190000012386576)

