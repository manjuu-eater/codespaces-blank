---
title: AudioBuffer.duration
slug: Web/API/AudioBuffer/duration
---
<p>{{ APIRef("Web Audio API") }}</p>

<div>
<p>{{domxref("AudioBuffer")}}接口的 duration 属性返回一个双精度数，表示缓冲区中存储的 PCM 数据的持续时间（以秒为单位）</p>
</div>

<h2 id="语法">语法</h2>

<pre class="brush: js; highlight[22]">var myArrayBuffer = audioCtx.createBuffer(2, frameCount, audioCtx.sampleRate);
myArrayBuffer.duration;</pre>

<h3 id="值">值</h3>

<p>双精度值</p>

<h2 id="例子">例子</h2>

<pre class="brush: js; highlight[22]">// Stereo
var channels = 2;

// Create an empty two second stereo buffer at the
// sample rate of the AudioContext
var frameCount = audioCtx.sampleRate * 2.0;
var myArrayBuffer = audioCtx.createBuffer(2, frameCount, audioCtx.sampleRate);

button.onclick = function() {
  // Fill the buffer with white noise;
  // just random values between -1.0 and 1.0
  for (var channel = 0; channel &lt; channels; channel++) {
    // This gives us the actual ArrayBuffer that contains the data
    var nowBuffering = myArrayBuffer.getChannelData(channel);
    for (var i = 0; i &lt; frameCount; i++) {
      // Math.random() is in [0; 1.0]
      // audio needs to be in [-1.0; 1.0]
      nowBuffering[i] = Math.random() * 2 - 1;
    }
  }

  console.log(myArrayBuffer.duration);
}
</pre>

<h2 id="规范">规范</h2>

{{Specifications}}

<h2 id="浏览器兼容性">浏览器兼容性</h2>

{{Compat("api.AudioBuffer.duration")}}

<h2 id="See_also">See also</h2>

<ul>
 <li><a href="/en-US/docs/Web/API/Web_Audio_API/Using_Web_Audio_API">Using the Web Audio API</a></li>
</ul>