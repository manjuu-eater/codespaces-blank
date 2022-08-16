---
title: 使用屏幕捕获 API
slug: Web/API/Screen_Capture_API/Using_Screen_Capture
---
<p>{{DefaultAPISidebar("Screen Capture API")}}</p>

<p>在这篇文章中，我们将研究如何使用屏幕捕获 API 和它的{{domxref("MediaDevices.getDisplayMedia", "getDisplayMedia()")}}方法来捕获部分或全部屏幕进行流媒体传输，通过<a href="/en-US/docs/Web/API/WebRTC_API">WebRTC</a>录制或分享。</p>

<div class="blockIndicator note">
<p><strong>Note:</strong> It may be useful to note that recent versions of the <a href="https://github.com/webrtcHacks/adapter">WebRTC adapter.js shim</a> include implementations of <code>getDisplayMedia()</code> to enable screen sharing on browsers that support it but do not implement the current standard API. This works with at least Chrome, Edge, and Firefox.</p>
</div>

<h2 id="捕捉屏幕内容">捕捉屏幕内容</h2>

<p>Capturing screen contents as a live {{domxref("MediaStream")}} is initiated by calling {{domxref("MediaDevices.getDisplayMedia", "navigator.mediaDevices.getDisplayMedia()")}}, which returns a promise that resolves to a stream containing the live screen contents.</p>

<p>开始屏幕捕捉：使用<code>async</code>/<code>await</code> 风格</p>

<pre class="brush: js notranslate">async function startCapture(displayMediaOptions) {
  let captureStream = null;

  try {
    captureStream = await navigator.mediaDevices.getDisplayMedia(displayMediaOptions);
  } catch(err) {
    console.error("Error: " + err);
  }
  return captureStream;
}</pre>

<p>You can write this code either using an asynchronous function and the <code><a href="/en-US/docs/Web/JavaScript/Reference/Operators/await">await</a></code> operator, as shown above, or using the {{jsxref("Promise")}} directly, as seen below.</p>

<p>开始屏幕捕获：使用 <code>Promise</code> 风格</p>

<pre class="brush: js notranslate">function startCapture(displayMediaOptions) {
 let captureStream = null;

 return navigator.mediaDevices.getDisplayMedia(displayMediaOptions)
    .catch(err =&gt; { console.error("Error:" + err); return null; });
}</pre>

<p>Either way, the {{Glossary("user agent")}} responds by presenting a user interface that prompts the user to choose the screen area to share. Both of these implementations of <code>startCapture()</code> return the {{domxref("MediaStream")}} containing the captured display imagery.</p>

<p>See <a href="#options_and_constraints">Options and constraints</a>, below, for more on both how to specify the type of surface you want as well as other ways to adjust the resulting stream.</p>

<p><em>Example of a window allowing the user to select a display surface to capture</em></p>

<p><img alt="Screenshot of Chrome's window for picking a source surface" src="chrome-screen-capture-window.png"></p>

<p>You can then use the captured stream, <code>captureStream</code>, for anything that accepts a stream as input. The <a href="#示例">examples</a> below show a few ways to make use of the stream.</p>

<h3 id="Visible_vs_logical_display_surfaces">Visible vs logical display surfaces</h3>

<p>For the purposes of the Screen Capture API, a <strong>display surface</strong> is any content object that can be selected by the API for sharing purposes. Sharing surfaces include the contents of a browser tab, a complete window, all of the applications of a window combined into a single surface, and a monitor (or group of monitors combined together into one surface).</p>

<p>There are two types of display surface. A <strong>visible display surface</strong> is a surface which is entirely visible on the screen, such as the frontmost window or tab, or the entire screen.</p>

<p>A <strong>logical display surface</strong> is one which is in part or completely obscured, either by being overlapped by another object to some extent, or by being entirely hidden or offscreen. How these are handled by the Screen Capture API varies. Generally, the browser will provide an image which obscures the hidden portion of the logical display surface in some way, such as by blurring or replacing with a color or pattern. This is done for security reasons, as the content that cannot be seen by the user may contain data which they do not want to share.</p>

<p>A user agent might allow the capture of the entire content of an obscured window after gaining permission from the user to do so. In this case, the user agent may include the obscured content, either by getting the current contents of the hidden portion of the window or by presenting the most-recently-visible contents if the current contents are not available.</p>

<h3 id="Options_and_constraints">Options and constraints</h3>

<p>The constraints object passed into {{domxref("MediaDevices.getDisplayMedia", "getDisplayMedia()")}} is a {{domxref("DisplayMediaStreamConstraints")}} object which is used to configuring the resulting stream.</p>

<div class="blockIndicator note">
<p><strong>Note:</strong> Unlike most uses of constraints in media APIs, here it's solely used to define the stream configuration, and <em>not</em> to filter the available choices.</p>
</div>

<p>There are three new constraints added to <code>MediaTrackConstraints</code> (as well as to {{domxref("MediaTrackSupportedConstraints")}} and {{domxref("MediaTrackSettings")}}) for configuring a screen capture stream:</p>

<dl>
 <dt>{{domxref("MediaTrackConstraints.cursor", "cursor")}}</dt>
 <dd>
 <p>Indicates whether or not to capture the mouse cursor, and if so, whether to do so all the time or only while the mouse is in motion. The possible values are:</p>

 <dl>
  <dt><code>always</code></dt>
  <dd>The mouse cursor should always be captured in the generated stream.</dd>
  <dt><code>motion</code></dt>
  <dd>The cursor should only be visible while moving, and, at the discretion of the {{Glossary("user agent")}}, for a brief time before after moving. Then the cursor is removed from the stream.</dd>
  <dt><code>never</code></dt>
  <dd>The cursor should never be visible in the generated stream.</dd>
 </dl>
 </dd>
 <dt>{{domxref("MediaTrackConstraints.logicalSurface", "logicalSurface")}}</dt>
 <dd>A Boolean which if <code>true</code> indicates that the capture should include offscreen areas of the source, if there are any.</dd>
</dl>

<p>None of the constraints are applied in any way until after the content to capture has been selected. The contraints alter what you see in the resulting stream.</p>

<p>For example, if you specify a {{domxref("MediaTrackConstraints.width", "width")}} constraint for the video, it's applied by scaling the video after the user selects the area to share. It doesn't establish a restriction on the size of the source itself.</p>

<div class="blockIndicator note">
<p><strong>Note:</strong> Constraints <em>never</em> cause changes to the list of sources available for capture by the Screen Sharing API. This ensures that web applications can't force the user to share specific content by restricting the source list until only one item is left.</p>
</div>

<p>While display capture is in effect, the machine which is sharing screen contents will display some form of indicator so the user is aware that sharing is taking place.</p>

<div class="blockIndicator note">
<p><strong>Note:</strong> For privacy and security reasons, screen sharing sources are not enumerable using {{domxref("MediaDevices.enumerateDevices", "enumerateDevices()")}}. Related to this, the {{event("devicechange")}} event is never sent when there are changes to the sources available for <code>getDisplayMedia()</code>.</p>
</div>

<h3 id="Capturing_shared_audio">Capturing shared audio</h3>

<p>{{domxref("MediaDevices.getDisplayMedia", "getDisplayMedia()")}} is most commonly used to capture video of a user's screen (or parts thereof). However, {{Glossary("user agent", "user agents")}} may allow the capture of audio along with the video content. The source of this audio might be the selected window, the entire computer's audio system, or the user's microphone (or a combination of all of the above).</p>

<p>Before starting a project that will require sharing of audio, be sure to check the {{SectionOnPage("/en-US/docs/Web/API/MediaDevices/getDisplayMedia", "Browser compatibility", "code")}} to see if the browsers you wish compaibility with have support for audio in captured screen streams.</p>

<p>To request that the screen be shared with included audio, the options passed into <code>getDisplayMedia()</code> might look like this:</p>

<pre class="brush: js notranslate">const gdmOptions = {
  video: true,
  audio: true
}
</pre>

<p>This allows the user total freedom to select whatever they want, within the limits of what the user agent supports. This could be refined further by specifying additional information for each of <code>audio</code> and <code>video</code>:</p>

<pre class="brush: js notranslate">const gdmOptions = {
  video: {
    cursor: "always"
  },
  audio: {
    echoCancellation: true,
    noiseSuppression: true,
    sampleRate: 44100
  }
}
</pre>

<p>In this example the cursor will always be visible in the capture, and the audio track should ideally have noise suppression and echo cancellation features enabled, as well as an ideal audio sample rate of 44.1kHz.</p>

<p>Capturing audio is always optional, and even when web content requests a stream with both audio and video, the returned {{domxref("MediaStream")}} may still have only one video track, with no audio.</p>

<div class="blockIndicator note">
<p><strong>Note:</strong> Some properties are not widely implemented and might not be used by the engine. <code>cursor</code>, for example, <a href="/en-US/docs/Web/API/MediaTrackConstraints/cursor#Browser_compatibility">has limited support</a>.</p>
</div>

<h2 id="使用捕获的数据流">使用捕获的数据流</h2>

<p>The {{jsxref("promise")}} returned by {{domxref("MediaDevices.getDisplayMedia", "getDisplayMedia()")}} resolves to a {{domxref("MediaStream")}} that contains at least one video stream that contains the screen or screen area, and which is adjusted or filtered based upon the constraints specifed when <code>getDisplayMedia()</code> was called.</p>

<h2 id="安全">安全</h2>

<p>As is always the case when sharing content over a network, it's important to consider the privacy and safety implications of screen sharing.</p>

<h3 id="潜在的风险">潜在的风险</h3>

<p>Privacy and security issues surrounding screen sharing are usually not overly serious, but they do exist. The largest potential issue is users inadvertently sharing content they did not wish to share.</p>

<p>For example, privacy and/or security violations can easily occur if the user is sharing their screen and a visible background window happens to contain personal information, or if their password manager is visible in the shared stream. This effect can be amplified when capturing logical display surfaces, which may contain content that the user doesn't know about at all, let alone see.</p>

<p>User agents which take privacy seriously should obfuscate content that is not actually visible onscreen, unless authorization has been given to share that content specifically.</p>

<h3 id="Authorizing_capture_of_display_contents">Authorizing capture of display contents</h3>

<p>Before streaming of captured screen contents can begin, the {{Glossary("user agent")}} will ask the user to confirm the sharing request, and to select the content to share.</p>
</figcaption>
</figure>

<h2 id="示例">示例</h2>

<h3 id="Simple_screen_capture">Simple screen capture</h3>

<p>In this example, the contents of the captured screen area are simply streamed into a {{HTMLElement("video")}} element on the same page.</p>

<h4 id="JavaScript">JavaScript</h4>

<p>There isn't all that much code needed in order to make this work, and if you're familiar with using {{domxref("MediaDevices.getUserMedia", "getUserMedia()")}} to capture video from a camera, you'll find {{domxref("MediaDevices.getDisplayMedia", "getDisplayMedia()")}} to be very familiar.</p>

<h5 id="Setup">Setup</h5>

<p>First, some constants are set up to reference the elements on the page to which we'll need access: the {{HTMLElement("video")}} into which the captured screen contents will be streamed, a box into which logged output will be drawn, and the start and stop buttons that will turn on and off capture of screen imagery.</p>

<p>The object <code>displayMediaOptions</code> contains the {{domxref("MediaStreamConstraints")}} to pass into <code>getDisplayMedia()</code>; here, the {{domxref("MediaTrackConstraints.cursor", "cursor")}} property is set to <code>always</code>, indicating that the mouse cursor should always be included in the captured media.</p>

<div class="blockIndicator note">
<p><strong>Note:</strong> Some properties are not widely implemented and might not be used by the engine. <code>cursor</code>, for example, <a href="/en-US/docs/Web/API/MediaTrackConstraints/cursor#Browser_compatibility">has limited support</a>.</p>
</div>

<p>Finally, event listeners are established to detect user clicks on the start and stop buttons.</p>

<pre class="brush: js notranslate">const videoElem = document.getElementById("video");
const logElem = document.getElementById("log");
const startElem = document.getElementById("start");
const stopElem = document.getElementById("stop");

// Options for getDisplayMedia()

var displayMediaOptions = {
  video: {
    cursor: "always"
  },
  audio: false
};

// Set event listeners for the start and stop buttons
startElem.addEventListener("click", function(evt) {
  startCapture();
}, false);

stopElem.addEventListener("click", function(evt) {
  stopCapture();
}, false);</pre>

<h5 id="Logging_content">Logging content</h5>

<p>To make logging of errors and other issues easy, this example overrides certain {{domxref("Console")}} methods to output their messages to the {{HTMLElement("pre")}} block whose ID is <code>log</code>.</p>

<pre class="brush: js notranslate">console.log = msg =&gt; logElem.innerHTML += `${msg}&lt;br&gt;`;
console.error = msg =&gt; logElem.innerHTML += `&lt;span class="error"&gt;${msg}&lt;/span&gt;&lt;br&gt;`;
console.warn = msg =&gt; logElem.innerHTML += `&lt;span class="warn"&gt;${msg}&lt;span&gt;&lt;br&gt;`;
console.info = msg =&gt; logElem.innerHTML += `&lt;span class="info"&gt;${msg}&lt;/span&gt;&lt;br&gt;`;</pre>

<p>This allows us to use the familiar {{domxref("console.log()")}}, {{domxref("console.error()")}}, and so on to log information to the log box in the document.</p>

<h5 id="Starting_display_capture">Starting display capture</h5>

<p>The <code>startCapture()</code> method, below, starts the capture of a {{domxref("MediaStream")}} whose contents are taken from a user-selected area of the screen. <code>startCapture()</code> is called when the "Start Capture" button is clicked.</p>

<pre class="brush: js notranslate">async function startCapture() {
  logElem.innerHTML = "";

  try {
    videoElem.srcObject = await navigator.mediaDevices.getDisplayMedia(displayMediaOptions);
    dumpOptionsInfo();
  } catch(err) {
    console.error("Error: " + err);
  }
}</pre>

<p>After clearing the contents of the log in order to get rid of any leftover text from the previous attempt to connect, <code>startCapture()</code> calls {{domxref("MediaDevices.getDisplayMedia", "getDisplayMedia()")}}, passing into it the constraints object defined by <code>displayMediaOptions</code>. Using {{jsxref("await")}}, the following line of code does not get executed until after the {{jsxref("promise")}} returned by <code>getDisplayMedia()</code> resolves. Upon resolution, the promise returns a {{domxref("MediaStream")}}, which will stream the contents of the screen, window, or other region selected by the user.</p>

<p>The stream is connected to the {{HTMLElement("video")}} element by storing the returned <code>MediaStream</code> into the element's {{domxref("HTMLMediaElement.srcObject", "srcObject")}}.</p>

<p>The <code>dumpOptionsInfo()</code> function—which we will look at in a moment—dumps information about the stream to the log box for educational purposes.</p>

<p>If any of that fails, the <code><a href="/en-US/docs/Web/JavaScript/Reference/Statements/try...catch">catch()</a></code> clause outputs an error message to the log box.</p>

<h5 id="Stopping_display_capture">Stopping display capture</h5>

<p>The <code>stopCapture()</code> method is called when the "Stop Capture" button is clicked. It stops the stream by getting its track list using {{domxref("MediaStream.getTracks()")}}, then calling each track's {domxref("MediaStreamTrack.stop, "stop()")}} method. Once that's done, <code>srcObject</code> is set to <code>null</code> to make sure it's understood by anyone interested that there's no stream connected.</p>

<pre class="brush: js notranslate">function stopCapture(evt) {
  let tracks = videoElem.srcObject.getTracks();

  tracks.forEach(track =&gt; track.stop());
  videoElem.srcObject = null;
}</pre>

<h5 id="Dumping_configuration_information">Dumping configuration information</h5>

<p>For informational purposes, the <code>startCapture()</code> method shown above calls a method named <code>dumpOptions()</code>, which outputs the current track settings as well as the constraints that were placed upon the stream when it was created.</p>

<pre class="brush: js notranslate">function dumpOptionsInfo() {
  const videoTrack = videoElem.srcObject.getVideoTracks()[0];

  console.info("Track settings:");
  console.info(JSON.stringify(videoTrack.getSettings(), null, 2));
  console.info("Track constraints:");
  console.info(JSON.stringify(videoTrack.getConstraints(), null, 2));
}</pre>

<p>The track list is obtained by calling {{domxref("MediaStream.getVideoTracks", "getVideoTracks()")}} on the capture'd screen's {{domxref("MediaStream")}}. The settings currently in effect are obtained using {{domxref("MediaStreamTrack.getSettings", "getSettings()")}} and the established constraints are gotten with {{domxref("MediaStreamTrack.getConstraints", "getConstraints()")}}</p>

<h4 id="HTML">HTML</h4>

<p>The HTML starts with a simple introductory paragraph, then gets into the meat of things.</p>

<ol>
</ol>

<pre class="brush: html notranslate">&lt;p&gt;This example shows you the contents of the selected part of your display.
Click the Start Capture button to begin.&lt;/p&gt;

&lt;p&gt;&lt;button id="start"&gt;Start Capture&lt;/button&gt;&amp;nbsp;&lt;button id="stop"&gt;Stop Capture&lt;/button&gt;&lt;/p&gt;

&lt;video id="video" autoplay&gt;&lt;/video&gt;
&lt;br&gt;

&lt;strong&gt;Log:&lt;/strong&gt;
&lt;br&gt;
&lt;pre id="log"&gt;&lt;/pre&gt;</pre>

<p>The key parts of the HTML are:</p>

<ol>
 <li>A {{HTMLElement("button")}} labeled "Start Capture" which, when clicked, calls the <code>startCapture()</code> function to request access to, and begin capturing, screen contents.</li>
 <li>A second button, "Stop Capture", which upon being clicked calls <code>stopCapture()</code> to terminate capture of screen contents.</li>
 <li>A {{HTMLElement("video")}} into which the captured screen contents are streamed.</li>
 <li>A {{HTMLElement("pre")}} block into which logged text is placed by the intercepted {{domxref("Console")}}method.</li>
</ol>

<h4 id="CSS">CSS</h4>

<p>The CSS is entirely cosmetic in this example. The video is given a border, and its width is set to occupy nearly the entire available horizontal space (<code>width: 98%</code>). {{cssxref("max-width")}} is set to <code>860px</code> to set an absolute upper limit on the video's size,</p>

<p>The <code>error</code>, <code>warn</code>, and <code>info</code> classes are used to style the corresponding console output types.</p>

<pre class="brush: css notranslate">#video {
  border: 1px solid #999;
  width: 98%;
  max-width: 860px;
}

.error {
  color: red;
}

.warn {
  color: orange;
}

.info {
  color: darkgreen;
}</pre>

<h4 id="Result">Result</h4>

<p>The final product looks like this. If your browser supports Screen Capture API, clicking "Start Capture" will present the {{Glossary("user agent", "user agent's")}} interface for selecting a screen, window, or tab to share.</p>

<p>{{EmbedLiveSample("Simple_screen_capture", 640, 680, "", "", "", "display-capture")}}</p>

<h2 id="安全_2">安全</h2>

<p>In order to function when <a href="/en-US/docs/Web/HTTP/Feature_Policy">Feature Policy</a> is enabled, you will need the <code>display-capture</code> permission. This can be done using the {{HTTPHeader("Feature-Policy")}} {{Glossary("HTTP")}} header or—if you're using the Screen Capture API in an {{HTMLElement("iframe")}}, the <code>&lt;iframe&gt;</code> element's {{htmlattrxref("allow", "iframe")}} attribute.</p>

<p>For example, this line in the HTTP headers will enable Screen Capture API for the document and any embedded {{HTMLElement("iframe")}} elements that are loaded from the same origin:</p>

<pre class="notranslate">Feature-Policy: display-capture 'self'</pre>

<p>If you're performing screen capture within an <code>&lt;iframe&gt;</code>, you can request permission just for that frame, which is clearly more secure than requesting a more general permission:</p>

<pre class="brush: html notranslate">&lt;iframe src="https://mycode.example.net/etc" allow="display-capture"&gt;
&lt;/iframe&gt;
</pre>

<h2 id="相关链接">相关链接</h2>

<ul>
 <li><a href="/en-US/docs/Web/API/Screen_Capture_API">Screen Capture API</a></li>
 <li><a href="/en-US/docs/Web/API/Media_Streams_API">Media Capture and Streams API</a></li>
 <li><a href="/en-US/docs/Web/API/WebRTC_API/Taking_still_photos">Taking still photos with WebRTC</a></li>
 <li>{{domxref("HTMLCanvasElement.captureStream()")}} to obtain a {{domxref("MediaStream")}} with the live contents of a {{HTMLElement("canvas")}}</li>
</ul>
</figure>