---
title: Attr
slug: Web/API/Attr
---
<div>{{APIRef("DOM")}}</div>

<p>该类型使用对象来表示一个 DOM 元素的属性。在大多数 DOM 方法中，你可能会直接通过字符串的方式获取属性值（例如{{domxref("Element.getAttribute()")}}），但是一些函数（例如{{domxref("Element.getAttributeNode()")}}）或通过迭代器访问时则返回<code>Attr</code>类型。</p>

<p>{{InheritanceDiagram}}</p>

<div class="warning"><strong>警告：</strong>从 Gecko 7.0 开始{{geckoRelease("7.0")}}，控制台会输出这些方法和属性将会被移除的警告信息。你应该对代码进行相应的修正。点击<a href="#废弃的属性和方法">废弃的属性和方法</a>查看完整的列表。</div>

<div class="warning">在<a href="https://www.w3.org/standards/history/dom">DOM4[REC]</a>中，为了规范化 Attr 的实现，它不再继承自{{domxref("Node")}}。在目前<a href="https://www.w3.org/standards/history/dom41">DOM4.1[WD]</a>中又有变动，因此不建议使用 Attr 对象上有关{{domxref("Node")}}的属性和方法。</div>

<h2 id="属性">属性</h2>

<dl>
 <dt>{{domxref("Attr.name", "name")}} {{readOnlyInline}}</dt>
 <dd>该属性的名称</dd>
 <dt>{{domxref("Attr.namespaceURI", "namespaceURI")}} {{readOnlyInline}}</dt>
 <dd>
 <p>表示该属性的命名空间 URI{{domxref("DOMString")}}，如果该元素不在命名空间中，则返回 null。</p>
 </dd>
 <dt>{{domxref("Attr.localName", "localName")}} {{readOnlyInline}}</dt>
 <dd>
 <p>表示该属性的命名空间限定的本地名称{{domxref("DOMString")}}。</p>
 </dd>
 <dt>{{domxref("Attr.prefix", "prefix")}} {{readOnlyInline}}</dt>
 <dd>表示该属性的命名空间前缀{{domxref("DOMString")}}，如果没有前缀指定则返回 null。</dd>
 <dt>{{domxref("Attr.ownerElement", "ownerElement")}} {{readOnlyInline}}</dt>
 <dd>
 <p>该属性所附属的元素节点。</p>

 <div class="note">
 <p><strong>注意：</strong> DOM Level 4 移除了这个方法。由于当你从{{domxref("Element")}}中获得<code>Attr</code>对象时，你应已知相关的元素。<br>
  在某些场景下并一定能够得到相关的元素，比如通过{{domxref("Document.evaluate")}}返回的 Attr 对象，最新的 DOM 草案再次引入该属性。</p>

 <p>Gecko 从 Gecko 7.0 {{geckoRelease("7.0")}}开始会输出一个废弃的提示信息。 该提示信息在 Gecko 49.0 {{geckoRelease("49.0")}}再次被删除。</p>
 </div>
 </dd>
 <dt>{{domxref("Attr.specified", "specified")}} {{readOnlyInline}}</dt>
 <dd>该属性将返回<code>真</code>。如果这个属性你在源代码或者在脚本中明确指定的话，它总是返回真。否则它是由文档的 DTD 默认定义的，将总是返回<code>假</code>。</dd>
 <dt>{{domxref("Attr.value", "value")}}</dt>
 <dd>属性的值</dd>
</dl>

<div class="note">
<p><strong>注意：</strong> DOM Level 3 定义<code>namespaceURI</code>, <code>localName</code>和<code>prefix</code>为{{domxref("Node")}}接口。在 DOM4 中被移至<code>Attr</code>。</p>

<p>Chrome 46.0 版本以上、Firefox 48.0 版本以上实现了该改动。</p>
</div>

<h2 id="废弃的属性和方法">废弃的属性和方法</h2>

<p>这些属性已经被废弃，可以使用合适的属性替代。</p>

<dl>
 <dt><code>attributes</code></dt>
 <dd>
 <p>当前该属性总是返回 <code>NULL</code></p>
 </dd>
 <dt><code>childNodes</code> {{Deprecated_Inline}}</dt>
 <dd>当前该属性总是返回一个空的 {{domxref("NodeList")}}.</dd>
 <dt><code>firstChild</code> {{Deprecated_Inline}}</dt>
 <dd><code>当前该属性总是返回 NULL</code></dd>
 <dt><code>isId</code> {{readOnlyInline}}</dt>
 <dd>表明该属性是否一个“ID 属性”。“ID 属性”的值在整个 DOM 文档中应当是唯一。在 HTML DOM 文档中属性“id”是一个 ID 属性，也是唯一一个 ID 属性；但是在 XML 文档中可以定义其他 ID 属性。一个属性是否是唯一的，通常由{{Glossary("DTD")}}或其他文档模式描述文件决定。</dd>
 <dt><code>lastChild</code></dt>
 <dd><code>当前该属性总是返回 NULL</code></dd>
 <dt><code>nextSibling</code></dt>
 <dd><code>当前该属性总是返回 NULL</code></dd>
 <dt><code>nodeName</code></dt>
 <dd>使用{{domxref("Attr.name")}}来代替</dd>
 <dt><code>nodeType</code></dt>
 <dd><code>当前该属性总是返回</code>2，表示<code>ATTRIBUTE_NODE</code></dd>
 <dt><code>nodeValue</code></dt>
 <dd>使用{{domxref("Attr.value")}}来代替</dd>
 <dt><code>ownerDocument</code></dt>
 <dd>这个属性本不应当在这里被使用，所以应该无须担心其演变</dd>
 <dt><code>parentNode</code></dt>
 <dd><code>当前该属性总是返回 NULL</code></dd>
 <dt><code>previousSibling</code></dt>
 <dd><code>当前该属性总是返回 NULL</code></dd>
 <dt><code>schemaTypeInfo</code> {{Deprecated_Inline}} {{readOnlyInline}}</dt>
 <dd>当前属性的类型信息。然而当加载完文档完或调用{{domxref("Document.normalizeDocument")}}后，这个被认定为绝对正确的包含在节点内的类型信息，会因为节点的移动而变得不可信。</dd>
 <dt><code>specified</code></dt>
 <dd><code>当前该属性总是返回 true</code></dd>
 <dt><code>textContent</code></dt>
 <dd>使用{{domxref("Attr.value")}}来代替</dd>
</dl>

<p>这些方法已经被废弃：</p>

<dl>
 <dt><code>appendChild()</code> {{Deprecated_Inline}}</dt>
 <dd>通过编辑{{domxref("Attr.value")}}属性来实现相同的效果</dd>
 <dt><code>cloneNode()</code></dt>
 <dd>这个方法本不应当在这里被使用，所以无须担心其演变</dd>
 <dt><code>createAttribute()</code></dt>
 <dd>使用{{domxref("Element.setAttribute()")}}来代替</dd>
 <dt><code>createAttributeNS()</code></dt>
 <dd>使用{{domxref("Element.setAttributeNS()")}}来代替</dd>
 <dt><code>getAttributeNode()</code></dt>
 <dd>使用{{domxref("Element.getAttribute()")}}来代替</dd>
 <dt><code>getAttributeNodeNS()</code></dt>
 <dd>使用{{domxref("Element.getAttributeNS()")}}来代替</dd>
 <dt><code>hasAttributes() </code> {{Deprecated_Inline}}</dt>
 <dd><code>当前该方法总是返回</code>false.</dd>
 <dt><code>hasChildNodes()</code></dt>
 <dd><code>当前该方法总是返回</code>false.</dd>
 <dt><code>insertBefore()</code></dt>
 <dd>通过编辑{{domxref("Attr.value")}}来实现相同效果</dd>
 <dt><code>isSupported()</code></dt>
 <dd>这个方法本不应当被在这里使用，所以无须担心其演变</dd>
 <dt><code>isEqualNode()</code></dt>
 <dd>这个方法本不应当被在这里使用，所以无须担心其演变</dd>
 <dt><code>normalize()</code></dt>
 <dd>这个方法本不应当被在这里使用，所以无须担心其演变</dd>
 <dt><code>removeAttributeNode()</code></dt>
 <dd>使用{{domxref("Element.removeAttribute()")}}来代替</dd>
 <dt><code>removeChild()</code> {{Deprecated_Inline}}</dt>
 <dd>通过编辑{{domxref("Attr.value")}}来实现相同效果</dd>
 <dt><code>replaceChild()</code> {{Deprecated_Inline}}</dt>
 <dd>通过编辑{{domxref("Attr.value")}}来实现相同效果</dd>
 <dt><code>setAttributeNode()</code></dt>
 <dd>使用{{domxref("Element.setAttribute()")}}来代替</dd>
 <dt><code>setAttributeNodeNS()</code></dt>
 <dd>使用{{domxref("Element.setAttributeNS()")}}来代替</dd>
</dl>

<h2 id="规格">规格</h2>

{{Specifications}}

<h2 id="浏览器兼容性">浏览器兼容性</h2>

{{Compat}}

<h2 id="参考">参考</h2>

<ul>
 <li><a href="http://www.w3.org/TR/DOM-Level-3-Core/core.html#ID-637646024">Document Object Model Core level 3: Interface Attr</a></li>
 <li><a href="http://www.w3.org/TR/dom/#interface-attr">Document Object Model 4: Interface Attr</a></li>
</ul>