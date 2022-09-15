---
title: FormData.delete()
slug: Web/API/FormData/delete
translation_of: Web/API/FormData/delete
---
<p>{{APIRef("XMLHttpRequest")}}</p>

<p>O metodo <code><strong>delete()</strong></code> da  interface {{domxref("FormData")}} deleta uma chave/valor pares do Objecto <code>FormData</code> .</p>

<div class="note">
<p><strong>Nota</strong>: Este metodo esta Disponivel em <a href="/en-US/docs/Web/API/Web_Workers_API">Web Workers</a>.</p>
</div>

<h2 id="Sintaxe">Sintaxe</h2>

<pre class="brush: js">formData.delete(name);</pre>

<h3 id="append()_Parameters" name="append()_Parameters">Parametros</h3>

<dl>
 <dt><code>name</code></dt>
 <dd>O name da chave que desejas apagar.</dd>
</dl>

<h3 id="Retorna">Retorna</h3>

<p>Void.</p>

<h2 id="Exemplo">Exemplo</h2>

<p>Esta linha cria um objecto <code>FormData</code> vazio e subistitui com a chave/valor pares de  form:</p>

<pre class="brush: js">var formData = new FormData(myForm);</pre>

<p>Podes deletar chave/valor pares usando <code>delete()</code>:</p>

<pre class="brush: js">formData.delete('username');
</pre>

<h2 id="Specificasões">Specificasões</h2>

<table class="standard-table">
 <tbody>
  <tr>
   <th scope="col">Specificasões</th>
   <th scope="col">Status</th>
   <th scope="col">Comment</th>
  </tr>
  <tr>
   <td>{{SpecName('XMLHttpRequest','#dom-formdata-delete','delete()')}}</td>
   <td>{{Spec2('XMLHttpRequest')}}</td>
   <td> </td>
  </tr>
 </tbody>
</table>

<h2 id="Browser_compatibility">Compatibilidade com navegadores</h2>

{{Compat("api.FormData.delete")}}

<h2 id="Veja_Tambem">Veja Tambem</h2>

<ul>
 <li>{{domxref("XMLHTTPRequest")}}</li>
 <li><a href="/en-US/docs/DOM/XMLHttpRequest/Using_XMLHttpRequest" title="Using XMLHttpRequest">Usando XMLHttpRequest</a></li>
 <li><a href="/en-US/docs/DOM/XMLHttpRequest/FormData/Using_FormData_Objects" title="DOM/XMLHttpRequest/FormData/Using_FormData_objects">Usando Objecto FormData</a></li>
 <li>{{HTMLElement("Form")}}</li>
</ul>