---
title: HTMLSelectElement.checkValidity()
slug: Web/API/HTMLSelectElement/checkValidity
---
<div>{{ APIRef("HTML DOM") }}</div>

<p><code><strong>HTMLSelectElement.checkValidity()</strong></code> 会检查元素是否有任何输入约束条件，并且检查值是否符合约束条件. 如果值是不符合约束条件的, 浏览器就会在该元素上触发一个可以撤销的 {{event("invalid")}} 事件,  然后返回 <code>false</code>.</p>

<h2 id="Syntax">Syntax</h2>

<pre class="brush: js"><code class="language-html">var <em>result</em> = <em>selectElt</em>.checkValidity();</code></pre>

<h2 id="Specifications">Specifications</h2>

{{Specifications}}

<h2 id="Browser_compatibility">Browser compatibility</h2>

{{Compat("api.HTMLSelectElement.checkValidity")}}

<h2 id="See_also">See also</h2>

<ul>
 <li><a href="/en-US/docs/Web/Guide/HTML/HTML5/Constraint_validation">Form validation.</a></li>
</ul>