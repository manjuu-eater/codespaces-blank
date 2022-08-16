---
title: Animation.id
slug: Web/API/Animation/id
---
<p>{{ SeeCompatTable() }}{{ APIRef("Web Animations API") }}</p>

<p><a href="/en-US/docs/Web/API/Web_Animations_API">Web Animations API</a> 的 <code><strong>Animation</strong></code><strong><code>.id </code></strong>属性可返回或设置用于识别某个动画的唯一标识。</p>

<h2 id="获取与设置_animation.id">获取与设置 <code>animation.<em>id</em></code></h2>

<div class="syntaxbox">
<pre class="brush: js">// 获取动画的 id
var animationsId = animation.<em>id</em>;

// 设置动画的 id
animation.<em>id</em> = "newId";
</pre>
</div>

<h2 id="返回值">返回值</h2>

<p>当该动画已被分配 id，返回一个 {{domxref("DOMString")}}, 当该动画未被分配 id 则返回 null.</p>

<h2 id="示例">示例</h2>

<p>在 <a href="http://codepen.io/rachelnabors/pen/eJyWzm?editors=0010">Follow the White Rabbit example</a> 这个例子里，你可以像下面的方式一样，为 <code>rabbitDownAnimation</code> 分配一个 id:</p>

<pre class="brush: js">rabbitDownAnimation.effect.<em>id</em> = "rabbitGo";
</pre>

<h2 id="规范">规范</h2>

{{Specifications}}

<h2 id="浏览器支持">浏览器支持</h2>

{{Compat("api.Animation.id")}}

<h2 id="相关文档">相关文档</h2>

<ul>
 <li><a href="/en-US/docs/Web/API/KeyframeEffect">KeyframeEffect Interface</a></li>
 <li><a href="/en-US/docs/Web/API/Web_Animations_API">Web Animations API</a></li>
 <li>{{domxref("Animation")}}</li>
</ul>