---
title: Document.designMode
slug: Web/API/Document/designMode
translation_of: Web/API/Document/designMode
---
<div>{{ ApiRef() }}</div>

<div> </div>

<h2 id="Summary" name="Summary">Sumário</h2>

<p><code>document.designMode</code> controla se o documento todo é editável. Valores validos são <code>"on"</code> e <code>"off"</code>. De acordo com a especificação, esta propriedade é por padrão <code>"off"</code>. Firefox segue este padrão. Nas versões anteriores do Chrome e IE o padrão é <code>"inherit"</code>. No IE6-10, o valor é capitalizado.</p>

<h2 id="Sintaxe">Sintaxe</h2>

<pre class="brush: js">var mode = document.designMode;
document.designMode = "on";
document.designMode = "off";</pre>

<h2 id="Example" name="Example">Exemplo</h2>

<p>Cria um documento {{HTMLElement("iframe")}} editável:</p>

<pre>iframe_node.contentDocument.designMode = "on";
</pre>

<h2 id="Especificação">Especificação</h2>

<table class="standard-table">
 <tbody>
  <tr>
   <th scope="col">Specification</th>
   <th scope="col">Status</th>
   <th scope="col">Comment</th>
  </tr>
  <tr>
   <td>{{SpecName('HTML WHATWG', '#making-entire-documents-editable:-the-designmode-idl-attribute', 'designMode')}}</td>
   <td>{{Spec2('HTML WHATWG')}}</td>
   <td>Initial definition.</td>
  </tr>
 </tbody>
</table>

<h2 id="Browser_compatibility">Compatibilidade com navegadores</h2>

{{Compat("api.Document.designMode")}}

<h2 id="See_also" name="See_also"> </h2>

<h2 id="See_also" name="See_also">Veja também:</h2>

<ul>
 <li><a href="/en-US/docs/Rich-Text_Editing_in_Mozilla">Rich-Text Editing in Mozilla</a></li>
 <li>{{domxref("HTMLElement.contentEditable")}}</li>
 <li><a href="https://msdn.microsoft.com/en-us/library/ms533720(v=vs.85).aspx">designMode property</a> on MSDN</li>
</ul>