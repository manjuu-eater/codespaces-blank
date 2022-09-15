---
title: Event()
slug: Web/API/Event/Event
translation_of: Web/API/Event/Event
---
<p>{{APIRef("DOM")}}</p>

<p>O <code><strong>Event()</strong></code> cria uma nova {{domxref("Event")}}.</p>

<h2 id="Sintaxe">Sintaxe</h2>

<pre class="syntaxbox"> <em>event</em> = new Event(<em>typeArg</em>, <em>eventInit</em>);</pre>

<h3 id="Valores">Valores</h3>

<dl>
 <dt><em>typeArg</em></dt>
 <dd>É uma {{domxref("DOMString")}} representa o nome do evento.</dd>
 <dt><em>eventInit</em>{{optional_inline}}</dt>
 <dd>É um dicionário <code>EventInit</code>, tendo os seguintes campos:

 <ul>
  <li><code>"bubbles"</code>, opcional e false por default, do tipo {{jsxref("Boolean")}}, indica se o evento é bubbles ou não.</li>
  <li><code>"cancelable"</code>, opcional e false por default, do tipo {{jsxref("Boolean")}}, indica se o evento pode ser cancelado ou não.</li>
 </ul>
 </dd>
</dl>

<h2 id="Exemplo">Exemplo</h2>

<pre class="brush: js">// criar um evento com bubbles true e que não pode ser cancelado

var ev = new Event("look", {"bubbles":true, "cancelable":false});
document.dispatchEvent(ev);
</pre>

<h2 id="Especificações">Especificações</h2>

<table class="standard-table" style="height: 49px; width: 1000px;">
 <thead>
  <tr>
   <th scope="col">Especificação</th>
   <th scope="col">Status</th>
   <th scope="col">Comentário</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>{{SpecName('DOM WHATWG','#interface-event','Event()')}}</td>
   <td>{{Spec2('DOM WHATWG')}}</td>
   <td>Definição inicial.</td>
  </tr>
 </tbody>
</table>

<h2 id="Browser_compatibility">Compatibilidade com navegadores</h2>



<p>{{Compat("api.Event.Event")}}</p>

<h2 id="Veja_também">Veja também</h2>

<ul>
 <li>{{domxref("Event")}}</li>
</ul>