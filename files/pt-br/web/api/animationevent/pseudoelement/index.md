---
title: AnimationEvent.pseudoElement
slug: Web/API/AnimationEvent/pseudoElement
tags:
  - AnimationEvent
  - Animação Web
  - Apps
  - CSSOM
  - Propriedade
  - Referencia
translation_of: Web/API/AnimationEvent/pseudoElement
---
<p>{{SeeCompatTable}}{{ apiref("Web Animations API") }}</p>

<h2 id="Sumário">Sumário</h2>

<p>O <code><strong>AnimationEvent.pseudoElement</strong></code> é uma propriedade só de leitura do {{domxref("DOMString")}}, começando com <code>'::'</code>, contendo o nome do <a href="/en-US/docs/Web/CSS/Pseudo-elements" title="/en-US/docs/Web/CSS/Pseudo-elements">pseudo-element</a> em que a animação roda. Se a animação não roda em um pseudo-elemento mas em um elemento, então temos uma<em> string</em> vazia : <code>''</code><code>.</code></p>

<h2 id="Síntaxe">Síntaxe</h2>

<pre class="syntaxbox"><em>name</em> = <em>AnimationEvent</em>.pseudoElement</pre>

<h2 id="Especificações">Especificações</h2>

<table class="standard-table">
 <thead>
  <tr>
   <th scope="col">Especificação</th>
   <th scope="col">Estado</th>
   <th scope="col">Comentário</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>{{ SpecName('CSS3 Animations', '#AnimationEvent-pseudoElement', 'AnimationEvent.pseudoElement') }}</td>
   <td>{{ Spec2('CSS3 Animations')}}</td>
   <td>Initial definition.</td>
  </tr>
 </tbody>
</table>

<h2 id="Browser_compatibility">Compatibilidade com navegadores</h2>

{{Compat("api.AnimationEvent.pseudoElement")}}

<h2 id="See_also">See also</h2>

<ul>
 <li><a href="https://developer.mozilla.org/en-US/docs/CSS/Using_CSS_animations">Using CSS animations</a></li>
 <li>{{cssxref("animation")}}, {{cssxref("animation-delay")}}, {{cssxref("animation-direction")}}, {{cssxref("animation-duration")}}, {{cssxref("animation-fill-mode")}}, {{cssxref("animation-iteration-count")}}, {{cssxref("animation-name")}}, {{cssxref("animation-play-state")}}, {{cssxref("animation-timing-function")}}, {{cssxref("@keyframes")}}.</li>
 <li>The {{domxref("AnimationEvent")}} interface it belongs to.</li>
</ul>