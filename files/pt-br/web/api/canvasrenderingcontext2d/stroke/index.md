---
title: CanvasRenderingContext2D.stroke()
slug: Web/API/CanvasRenderingContext2D/stroke
tags:
  - API
  - Canvas
  - CanvasRenderingContext2D
  - Referencia
  - metodo
translation_of: Web/API/CanvasRenderingContext2D/stroke
---
<div>{{APIRef}}</div>

<p>O método <code><strong>CanvasRenderingContext2D</strong></code><strong><code>.stroke()</code></strong> da API Canvas 2D contorna um dado <em>path</em> ou o <em>path</em> atual com o estilo atual de traçado usando uma regra de controle diferente de zero.</p>

<h2 id="Sintaxe">Sintaxe</h2>

<pre class="syntaxbox">void <var><em>ctx</em>.stroke();</var>
void <var><em>ctx</em>.stroke(path);</var>
</pre>

<h3 id="Parâmetros">Parâmetros</h3>

<dl>
 <dt><code>path</code></dt>
 <dd>Um <em>path</em> de {{domxref("Path2D")}} para contorno.</dd>
</dl>

<h2 id="Exemplos">Exemplos</h2>

<h3 id="Usando_o_método_stroke">Usando o método <code>stroke</code></h3>

<p>Isto é só um simples trecho de código que usa o método <code>stroke</code> para contornar um <em>path</em>.</p>

<h4 id="HTML">HTML</h4>

<pre class="brush: html">&lt;canvas id="canvas"&gt;&lt;/canvas&gt;
</pre>

<h4 id="JavaScript">JavaScript</h4>

<pre class="brush: js">var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');
ctx.rect(10, 10, 100, 100);
ctx.stroke();
</pre>

<p>Edite o código abaixo e veja as alterações instantâneas no canvas:</p>

<div class="hidden">
<h6 id="Playable_code">Playable code</h6>

<pre class="brush: html">&lt;canvas id="canvas" width="400" height="200" class="playable-canvas"&gt;&lt;/canvas&gt;
&lt;div class="playable-buttons"&gt;
  &lt;input id="edit" type="button" value="Edit" /&gt;
  &lt;input id="reset" type="button" value="Reset" /&gt;
&lt;/div&gt;
&lt;textarea id="code" class="playable-code"&gt;
ctx.rect(10, 10, 100, 100);
ctx.stroke();&lt;/textarea&gt;
</pre>

<pre class="brush: js">var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");
var textarea = document.getElementById("code");
var reset = document.getElementById("reset");
var edit = document.getElementById("edit");
var code = textarea.value;

function drawCanvas() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  eval(textarea.value);
}

reset.addEventListener("click", function() {
  textarea.value = code;
  drawCanvas();
});

edit.addEventListener("click", function() {
  textarea.focus();
})

textarea.addEventListener("input", drawCanvas);
window.addEventListener("load", drawCanvas);
</pre>
</div>

<p>{{ EmbedLiveSample('Playable_code', 700, 360) }}</p>

<h2 id="Especificações">Especificações</h2>

<table class="standard-table">
 <tbody>
  <tr>
   <th scope="col">Especificação</th>
   <th scope="col">Estado</th>
   <th scope="col">Comentário</th>
  </tr>
  <tr>
   <td>{{SpecName('HTML WHATWG', "scripting.html#dom-context-2d-stroke", "CanvasRenderingContext2D.stroke")}}</td>
   <td>{{Spec2('HTML WHATWG')}}</td>
   <td> </td>
  </tr>
 </tbody>
</table>

<h2 id="Browser_compatibility">Compatibilidade com navegadores</h2>

{{Compat("api.CanvasRenderingContext2D.stroke")}}

<h2 id="Veja_também">Veja também</h2>

<ul>
 <li>A definição da interface {{domxref("CanvasRenderingContext2D")}}.</li>
</ul>