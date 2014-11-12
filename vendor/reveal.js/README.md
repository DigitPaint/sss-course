<h1>reveal.js <a href="https://travis-ci.org/hakimel/reveal.js"><img src="https://travis-ci.org/hakimel/reveal.js.png?branch=master" alt="Build Status"></a></h1>

<p>A framework for easily creating beautiful presentations using HTML. <a href="http://lab.hakim.se/reveal-js/">Check out the live demo</a>.</p>

<p>reveal.js comes with a broad range of features including <a href="https://github.com/hakimel/reveal.js#markup">nested slides</a>, <a href="https://github.com/hakimel/reveal.js#markdown">markdown contents</a>, <a href="https://github.com/hakimel/reveal.js#pdf-export">PDF export</a>, <a href="https://github.com/hakimel/reveal.js#speaker-notes">speaker notes</a> and a <a href="https://github.com/hakimel/reveal.js#api">JavaScript API</a>. It&#39;s best viewed in a browser with support for CSS 3D transforms but <a href="https://github.com/hakimel/reveal.js/wiki/Browser-Support">fallbacks</a> are available to make sure your presentation can still be viewed elsewhere.</p>

<h4>More reading:</h4>

<ul>
<li><a href="#installation">Installation</a>: Step-by-step instructions for getting reveal.js running on your computer.</li>
<li><a href="https://github.com/hakimel/reveal.js/releases">Changelog</a>: Up-to-date version history.</li>
<li><a href="https://github.com/hakimel/reveal.js/wiki/Example-Presentations">Examples</a>: Presentations created with reveal.js, add your own!</li>
<li><a href="https://github.com/hakimel/reveal.js/wiki/Browser-Support">Browser Support</a>: Explanation of browser support and fallbacks.</li>
</ul>

<h2>Online Editor</h2>

<p>Presentations are written using HTML or markdown but there&#39;s also an online editor for those of you who prefer a graphical interface. Give it a try at <a href="http://slid.es">http://slid.es</a>.</p>

<h2>Instructions</h2>

<h3>Markup</h3>

<p>Markup hierarchy needs to be <code>&lt;div class=&quot;reveal&quot;&gt; &lt;div class=&quot;slides&quot;&gt; &lt;section&gt;</code> where the <code>&lt;section&gt;</code> represents one slide and can be repeated indefinitely. If you place multiple <code>&lt;section&gt;</code>&#39;s inside of another <code>&lt;section&gt;</code> they will be shown as vertical slides. The first of the vertical slides is the &quot;root&quot; of the others (at the top), and it will be included in the horizontal sequence. For example:</p>

<p><code>html
&lt;div class=&quot;reveal&quot;&gt;
    &lt;div class=&quot;slides&quot;&gt;
        &lt;section&gt;Single Horizontal Slide&lt;/section&gt;
        &lt;section&gt;
            &lt;section&gt;Vertical Slide 1&lt;/section&gt;
            &lt;section&gt;Vertical Slide 2&lt;/section&gt;
        &lt;/section&gt;
    &lt;/div&gt;
&lt;/div&gt;
</code></p>

<h3>Markdown</h3>

<p>It&#39;s possible to write your slides using Markdown. To enable Markdown, add the <code>data-markdown</code> attribute to your <code>&lt;section&gt;</code> elements and wrap the contents in a <code>&lt;script type=&quot;text/template&quot;&gt;</code> like the example below.</p>

<p>This is based on <a href="https://gist.github.com/1343518">data-markdown</a> from <a href="https://github.com/paulirish">Paul Irish</a> modified to use <a href="https://github.com/chjj/marked">marked</a> to support <a href="https://help.github.com/articles/github-flavored-markdown">Github Flavoured Markdown</a>. Sensitive to indentation (avoid mixing tabs and spaces) and line breaks (avoid consecutive breaks).</p>

<p>```html
<section data-markdown>
    <script type="text/template">
        ## Page title</p>

<pre><code>    A paragraph with some text and a [link](http://hakim.se).
&lt;/script&gt;
</code></pre>

<p></section>
```</p>

<h4>External Markdown</h4>

<p>You can write your content as a separate file and have reveal.js load it at runtime. Note the separator arguments which determine how slides are delimited in the external file. The <code>data-charset</code> attribute is optional and specifies which charset to use when loading the external file.</p>

<p>When used locally, this feature requires that reveal.js <a href="#full-setup">runs from a local web server</a>.</p>

<p><code>html
&lt;section data-markdown=&quot;example.md&quot;  
         data-separator=&quot;^\n\n\n&quot;  
         data-vertical=&quot;^\n\n&quot;  
         data-notes=&quot;^Note:&quot;  
         data-charset=&quot;iso-8859-15&quot;&gt;
&lt;/section&gt;
</code></p>

<h4>Element Attributes</h4>

<p>Special syntax (in html comment) is available for adding attributes to Markdown elements. This is useful for fragments, amongst other things.</p>

<p><code>html
&lt;section data-markdown&gt;
    &lt;script type=&quot;text/template&quot;&gt;
        - Item 1 &lt;!-- .element: class=&quot;fragment&quot; data-fragment-index=&quot;2&quot; --&gt;
        - Item 2 &lt;!-- .element: class=&quot;fragment&quot; data-fragment-index=&quot;1&quot; --&gt;
    &lt;/script&gt;
&lt;/section&gt;
</code></p>

<h4>Slide Attributes</h4>

<p>Special syntax (in html comment) is available for adding attributes to the slide <code>&lt;section&gt;</code> elements generated by your Markdown.</p>

<p><code>html
&lt;section data-markdown&gt;
    &lt;script type=&quot;text/template&quot;&gt;
    &lt;!-- .slide: data-background=&quot;#ff0000&quot; --&gt;
        Mardown content
    &lt;/script&gt;
&lt;/section&gt;
</code></p>

<h3>Configuration</h3>

<p>At the end of your page you need to initialize reveal by running the following code. Note that all config values are optional and will default as specified below.</p>

<p>```javascript
Reveal.initialize({</p>

<pre><code>// Display controls in the bottom right corner
controls: true,

// Display a presentation progress bar
progress: true,

// Display the page number of the current slide
slideNumber: false,

// Push each slide change to the browser history
history: false,

// Enable keyboard shortcuts for navigation
keyboard: true,

// Enable the slide overview mode
overview: true,

// Vertical centering of slides
center: true,

// Enables touch navigation on devices with touch input
touch: true,

// Loop the presentation
loop: false,

// Change the presentation direction to be RTL
rtl: false,

// Turns fragments on and off globally
fragments: true,

// Flags if the presentation is running in an embedded mode,
// i.e. contained within a limited portion of the screen
embedded: false,

// Number of milliseconds between automatically proceeding to the
// next slide, disabled when set to 0, this value can be overwritten
// by using a data-autoslide attribute on your slides
autoSlide: 0,

// Stop auto-sliding after user input
autoSlideStoppable: true,

// Enable slide navigation via mouse wheel
mouseWheel: false,

// Hides the address bar on mobile devices
hideAddressBar: true,

// Opens links in an iframe preview overlay
previewLinks: false,

// Transition style
transition: &#39;default&#39;, // default/cube/page/concave/zoom/linear/fade/none

// Transition speed
transitionSpeed: &#39;default&#39;, // default/fast/slow

// Transition style for full page slide backgrounds
backgroundTransition: &#39;default&#39;, // default/none/slide/concave/convex/zoom

// Number of slides away from the current that are visible
viewDistance: 3,

// Parallax background image
parallaxBackgroundImage: &#39;&#39;, // e.g. &quot;&#39;https://s3.amazonaws.com/hakim-static/reveal-js/reveal-parallax-1.jpg&#39;&quot;

// Parallax background size
parallaxBackgroundSize: &#39;&#39; // CSS syntax, e.g. &quot;2100px 900px&quot;
</code></pre>

<p>});
```</p>

<p>Note that the new default vertical centering option will break compatibility with slides that were using transitions with backgrounds (<code>cube</code> and <code>page</code>). To restore the previous behavior, set <code>center</code> to <code>false</code>.</p>

<p>The configuration can be updated after initialization using the <code>configure</code> method:</p>

<p>```javascript
// Turn autoSlide off
Reveal.configure({ autoSlide: 0 });</p>

<p>// Start auto-sliding every 5s
Reveal.configure({ autoSlide: 5000 });
```</p>

<h3>Dependencies</h3>

<p>Reveal.js doesn&#39;t <em>rely</em> on any third party scripts to work but a few optional libraries are included by default. These libraries are loaded as dependencies in the order they appear, for example:</p>

<p>```javascript
Reveal.initialize({
    dependencies: [
        // Cross-browser shim that fully implements classList - https://github.com/eligrey/classList.js/
        { src: &#39;lib/js/classList.js&#39;, condition: function() { return !document.body.classList; } },</p>

<pre><code>    // Interpret Markdown in &lt;section&gt; elements
    { src: &#39;plugin/markdown/marked.js&#39;, condition: function() { return !!document.querySelector( &#39;[data-markdown]&#39; ); } },
    { src: &#39;plugin/markdown/markdown.js&#39;, condition: function() { return !!document.querySelector( &#39;[data-markdown]&#39; ); } },

    // Syntax highlight for &lt;code&gt; elements
    { src: &#39;plugin/highlight/highlight.js&#39;, async: true, callback: function() { hljs.initHighlightingOnLoad(); } },

    // Zoom in and out with Alt+click
    { src: &#39;plugin/zoom-js/zoom.js&#39;, async: true, condition: function() { return !!document.body.classList; } },

    // Speaker notes
    { src: &#39;plugin/notes/notes.js&#39;, async: true, condition: function() { return !!document.body.classList; } },

    // Remote control your reveal.js presentation using a touch device
    { src: &#39;plugin/remotes/remotes.js&#39;, async: true, condition: function() { return !!document.body.classList; } },

    // MathJax
    { src: &#39;plugin/math/math.js&#39;, async: true }
]
</code></pre>

<p>});
```</p>

<p>You can add your own extensions using the same syntax. The following properties are available for each dependency object:
- <strong>src</strong>: Path to the script to load
- <strong>async</strong>: [optional] Flags if the script should load after reveal.js has started, defaults to false
- <strong>callback</strong>: [optional] Function to execute when the script has loaded
- <strong>condition</strong>: [optional] Function which must return true for the script to be loaded</p>

<h3>Presentation Size</h3>

<p>All presentations have a normal size, that is the resolution at which they are authored. The framework will automatically scale presentations uniformly based on this size to ensure that everything fits on any given display or viewport.</p>

<p>See below for a list of configuration options related to sizing, including default values:</p>

<p>```javascript
Reveal.initialize({</p>

<pre><code>...

// The &quot;normal&quot; size of the presentation, aspect ratio will be preserved
// when the presentation is scaled to fit different resolutions. Can be
// specified using percentage units.
width: 960,
height: 700,

// Factor of the display size that should remain empty around the content
margin: 0.1,

// Bounds for smallest/largest possible scale to apply to content
minScale: 0.2,
maxScale: 1.0
</code></pre>

<p>});
```</p>

<h3>Auto-sliding</h3>

<p>Presentations can be configure to progress through slides automatically, without any user input. To enable this you will need to tell the framework how many milliseconds it should wait between slides:</p>

<p><code>javascript
// Slide every five seconds
Reveal.configure({
  autoSlide: 5000
});
</code></p>

<p>When this is turned on a control element will appear that enables users to pause and resume auto-sliding. Sliding is also paused automatically as soon as the user starts navigating. You can disable these controls by specifying <code>autoSlideStoppable: false</code> in your reveal.js config.</p>

<p>You can also override the slide duration for individual slides by using the <code>data-autoslide</code> attribute on individual sections:</p>

<p><code>html
&lt;section data-autoslide=&quot;10000&quot;&gt;This will remain on screen for 10 seconds&lt;/section&gt;
</code></p>

<h3>Keyboard Bindings</h3>

<p>If you&#39;re unhappy with any of the default keyboard bindings you can override them using the <code>keyboard</code> config option:</p>

<p><code>javascript
Reveal.configure({
  keyboard: {
    13: &#39;next&#39;, // go to the next slide when the ENTER key is pressed
    27: function() {}, // do something custom when ESC is pressed
    32: null // don&#39;t do anything when SPACE is pressed (i.e. disable a reveal.js default binding)
  }
});
</code></p>

<h3>API</h3>

<p>The <code>Reveal</code> class provides a JavaScript API for controlling navigation and reading state:</p>

<p>```javascript
// Navigation
Reveal.slide( indexh, indexv, indexf );
Reveal.left();
Reveal.right();
Reveal.up();
Reveal.down();
Reveal.prev();
Reveal.next();
Reveal.prevFragment();
Reveal.nextFragment();
Reveal.toggleOverview();
Reveal.togglePause();</p>

<p>// Retrieves the previous and current slide elements
Reveal.getPreviousSlide();
Reveal.getCurrentSlide();</p>

<p>Reveal.getIndices(); // { h: 0, v: 0 } }</p>

<p>// State checks
Reveal.isFirstSlide();
Reveal.isLastSlide();
Reveal.isOverview();
Reveal.isPaused();
```</p>

<h3>Ready Event</h3>

<p>The &#39;ready&#39; event is fired when reveal.js has loaded all (synchronous) dependencies and is ready to start navigating.</p>

<p><code>javascript
Reveal.addEventListener( &#39;ready&#39;, function( event ) {
    // event.currentSlide, event.indexh, event.indexv
} );
</code></p>

<h3>Slide Changed Event</h3>

<p>An &#39;slidechanged&#39; event is fired each time the slide is changed (regardless of state). The event object holds the index values of the current slide as well as a reference to the previous and current slide HTML nodes.</p>

<p>Some libraries, like MathJax (see <a href="https://github.com/hakimel/reveal.js/issues/226#issuecomment-10261609">#226</a>), get confused by the transforms and display states of slides. Often times, this can be fixed by calling their update or render function from this callback.</p>

<p><code>javascript
Reveal.addEventListener( &#39;slidechanged&#39;, function( event ) {
    // event.previousSlide, event.currentSlide, event.indexh, event.indexv
} );
</code></p>

<h3>States</h3>

<p>If you set <code>data-state=&quot;somestate&quot;</code> on a slide <code>&lt;section&gt;</code>, &quot;somestate&quot; will be applied as a class on the document element when that slide is opened. This allows you to apply broad style changes to the page based on the active slide.</p>

<p>Furthermore you can also listen to these changes in state via JavaScript:</p>

<p><code>javascript
Reveal.addEventListener( &#39;somestate&#39;, function() {
    // TODO: Sprinkle magic
}, false );
</code></p>

<h3>Slide Backgrounds</h3>

<p>Slides are contained within a limited portion of the screen by default to allow them to fit any display and scale uniformly. You can apply full page background colors or images by applying a <code>data-background</code> attribute to your <code>&lt;section&gt;</code> elements. Below are a few examples.</p>

<p><code>html
&lt;section data-background=&quot;#ff0000&quot;&gt;
    &lt;h2&gt;All CSS color formats are supported, like rgba() or hsl().&lt;/h2&gt;
&lt;/section&gt;
&lt;section data-background=&quot;http://example.com/image.png&quot;&gt;
    &lt;h2&gt;This slide will have a full-size background image.&lt;/h2&gt;
&lt;/section&gt;
&lt;section data-background=&quot;http://example.com/image.png&quot; data-background-size=&quot;100px&quot; data-background-repeat=&quot;repeat&quot;&gt;
    &lt;h2&gt;This background image will be sized to 100px and repeated.&lt;/h2&gt;
&lt;/section&gt;
</code></p>

<p>Backgrounds transition using a fade animation by default. This can be changed to a linear sliding transition by passing <code>backgroundTransition: &#39;slide&#39;</code> to the <code>Reveal.initialize()</code> call. Alternatively you can set <code>data-background-transition</code> on any section with a background to override that specific transition.</p>

<h3>Parallax Background</h3>

<p>If you want to use a parallax scrolling background, set the two following config properties when initializing reveal.js (the third one is optional).</p>

<p>```javascript
Reveal.initialize({</p>

<pre><code>// Parallax background image
parallaxBackgroundImage: &#39;&#39;, // e.g. &quot;https://s3.amazonaws.com/hakim-static/reveal-js/reveal-parallax-1.jpg&quot;

// Parallax background size
parallaxBackgroundSize: &#39;&#39;, // CSS syntax, e.g. &quot;2100px 900px&quot; - currently only pixels are supported (don&#39;t use % or auto)

// This slide transition gives best results:
transition: linear
</code></pre>

<p>});
```</p>

<p>Make sure that the background size is much bigger than screen size to allow for some scrolling. <a href="http://lab.hakim.se/reveal-js/?parallaxBackgroundImage=https%3A%2F%2Fs3.amazonaws.com%2Fhakim-static%2Freveal-js%2Freveal-parallax-1.jpg&amp;parallaxBackgroundSize=2100px%20900px">View example</a>.</p>

<h3>Slide Transitions</h3>

<p>The global presentation transition is set using the <code>transition</code> config value. You can override the global transition for a specific slide by using the <code>data-transition</code> attribute:</p>

<p>```html
<section data-transition="zoom">
    <h2>This slide will override the presentation transition and zoom!</h2>
</section></p>

<p><section data-transition-speed="fast">
    <h2>Choose from three transition speeds: default, fast or slow!</h2>
</section>
```</p>

<p>Note that this does not work with the page and cube transitions.</p>

<h3>Internal links</h3>

<p>It&#39;s easy to link between slides. The first example below targets the index of another slide whereas the second targets a slide with an ID attribute (<code>&lt;section id=&quot;some-slide&quot;&gt;</code>):</p>

<p><code>html
&lt;a href=&quot;#/2/2&quot;&gt;Link&lt;/a&gt;
&lt;a href=&quot;#/some-slide&quot;&gt;Link&lt;/a&gt;
</code></p>

<p>You can also add relative navigation links, similar to the built in reveal.js controls, by appending one of the following classes on any element. Note that each element is automatically given an <code>enabled</code> class when it&#39;s a valid navigation route based on the current slide.</p>

<p><code>html
&lt;a href=&quot;#&quot; class=&quot;navigate-left&quot;&gt;
&lt;a href=&quot;#&quot; class=&quot;navigate-right&quot;&gt;
&lt;a href=&quot;#&quot; class=&quot;navigate-up&quot;&gt;
&lt;a href=&quot;#&quot; class=&quot;navigate-down&quot;&gt;
&lt;a href=&quot;#&quot; class=&quot;navigate-prev&quot;&gt; &lt;!-- Previous vertical or horizontal slide --&gt;
&lt;a href=&quot;#&quot; class=&quot;navigate-next&quot;&gt; &lt;!-- Next vertical or horizontal slide --&gt;
</code></p>

<h3>Fragments</h3>

<p>Fragments are used to highlight individual elements on a slide. Every element with the class <code>fragment</code> will be stepped through before moving on to the next slide. Here&#39;s an example: http://lab.hakim.se/reveal-js/#/fragments</p>

<p>The default fragment style is to start out invisible and fade in. This style can be changed by appending a different class to the fragment:</p>

<p><code>html
&lt;section&gt;
    &lt;p class=&quot;fragment grow&quot;&gt;grow&lt;/p&gt;
    &lt;p class=&quot;fragment shrink&quot;&gt;shrink&lt;/p&gt;
    &lt;p class=&quot;fragment roll-in&quot;&gt;roll-in&lt;/p&gt;
    &lt;p class=&quot;fragment fade-out&quot;&gt;fade-out&lt;/p&gt;
    &lt;p class=&quot;fragment current-visible&quot;&gt;visible only once&lt;/p&gt;
    &lt;p class=&quot;fragment highlight-current-blue&quot;&gt;blue only once&lt;/p&gt;
    &lt;p class=&quot;fragment highlight-red&quot;&gt;highlight-red&lt;/p&gt;
    &lt;p class=&quot;fragment highlight-green&quot;&gt;highlight-green&lt;/p&gt;
    &lt;p class=&quot;fragment highlight-blue&quot;&gt;highlight-blue&lt;/p&gt;
&lt;/section&gt;
</code></p>

<p>Multiple fragments can be applied to the same element sequentially by wrapping it, this will fade in the text on the first step and fade it back out on the second.</p>

<p><code>html
&lt;section&gt;
    &lt;span class=&quot;fragment fade-in&quot;&gt;
        &lt;span class=&quot;fragment fade-out&quot;&gt;I&#39;ll fade in, then out&lt;/span&gt;
    &lt;/span&gt;
&lt;/section&gt;
</code></p>

<p>The display order of fragments can be controlled using the <code>data-fragment-index</code> attribute.</p>

<p><code>html
&lt;section&gt;
    &lt;p class=&quot;fragment&quot; data-fragment-index=&quot;3&quot;&gt;Appears last&lt;/p&gt;
    &lt;p class=&quot;fragment&quot; data-fragment-index=&quot;1&quot;&gt;Appears first&lt;/p&gt;
    &lt;p class=&quot;fragment&quot; data-fragment-index=&quot;2&quot;&gt;Appears second&lt;/p&gt;
&lt;/section&gt;
</code></p>

<h3>Fragment events</h3>

<p>When a slide fragment is either shown or hidden reveal.js will dispatch an event.</p>

<p>Some libraries, like MathJax (see #505), get confused by the initially hidden fragment elements. Often times this can be fixed by calling their update or render function from this callback.</p>

<p><code>javascript
Reveal.addEventListener( &#39;fragmentshown&#39;, function( event ) {
    // event.fragment = the fragment DOM element
} );
Reveal.addEventListener( &#39;fragmenthidden&#39;, function( event ) {
    // event.fragment = the fragment DOM element
} );
</code></p>

<h3>Code syntax highlighting</h3>

<p>By default, Reveal is configured with <a href="http://softwaremaniacs.org/soft/highlight/en/">highlight.js</a> for code syntax highlighting. Below is an example with clojure code that will be syntax highlighted. When the <code>data-trim</code> attribute is present surrounding whitespace is automatically removed.</p>

<p><code>html
&lt;section&gt;
    &lt;pre&gt;&lt;code data-trim&gt;
(def lazy-fib
  (concat
   [0 1]
   ((fn rfib [a b]
        (lazy-cons (+ a b) (rfib b (+ a b)))) 0 1)))
    &lt;/code&gt;&lt;/pre&gt;
&lt;/section&gt;
</code></p>

<h3>Slide number</h3>

<p>If you would like to display the page number of the current slide you can do so using the <code>slideNumber</code> configuration value.</p>

<p><code>javascript
Reveal.configure({ slideNumber: true });
</code></p>

<h3>Overview mode</h3>

<p>Press &quot;Esc&quot; or &quot;o&quot; keys to toggle the overview mode on and off. While you&#39;re in this mode, you can still navigate between slides,
as if you were at 1,000 feet above your presentation. The overview mode comes with a few API hooks:</p>

<p>```javascript
Reveal.addEventListener( &#39;overviewshown&#39;, function( event ) { /* ... <em>/ } );
Reveal.addEventListener( &#39;overviewhidden&#39;, function( event ) { /</em> ... */ } );</p>

<p>// Toggle the overview mode programmatically
Reveal.toggleOverview();
```</p>

<h3>Fullscreen mode</h3>

<p>Just press »F« on your keyboard to show your presentation in fullscreen mode. Press the »ESC« key to exit fullscreen mode.</p>

<h3>Embedded media</h3>

<p>Embedded HTML5 <code>&lt;video&gt;</code>/<code>&lt;audio&gt;</code> and YouTube iframes are automatically paused when you navigate away from a slide. This can be disabled by decorating your element with a <code>data-ignore</code> attribute.</p>

<p>Add <code>data-autoplay</code> to your media element if you want it to automatically start playing when the slide is shown:</p>

<p><code>html
&lt;video data-autoplay src=&quot;http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4&quot;&gt;&lt;/video&gt;
</code></p>

<p>Additionally the framework automatically pushes two <a href="https://developer.mozilla.org/en-US/docs/Web/API/Window.postMessage">post messages</a> to all iframes, <code>slide:start</code> when the slide containing the iframe is made visible and <code>slide:stop</code> when it is hidden.</p>

<h3>Stretching elements</h3>

<p>Sometimes it&#39;s desirable to have an element, like an image or video, stretch to consume as much space as possible within a given slide. This can be done by adding the <code>.stretch</code> class to an element as seen below:</p>

<p><code>html
&lt;section&gt;
    &lt;h2&gt;This video will use up the remaining space on the slide&lt;/h2&gt;
    &lt;video class=&quot;stretch&quot; src=&quot;http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4&quot;&gt;&lt;/video&gt;
&lt;/section&gt;
</code></p>

<p>Limitations:
- Only direct descendants of a slide section can be stretched
- Only one descendant per slide section can be stretched</p>

<h2>PDF Export</h2>

<p>Presentations can be exported to PDF via a special print stylesheet. This feature requires that you use <a href="http://google.com/chrome">Google Chrome</a>.
Here&#39;s an example of an exported presentation that&#39;s been uploaded to SlideShare: http://www.slideshare.net/hakimel/revealjs-13872948.</p>

<ol>
<li>Open your presentation with <a href="https://github.com/hakimel/reveal.js/blob/master/css/print/pdf.css">css/print/pdf.css</a> included on the page. The default index HTML lets you add <em>print-pdf</em> anywhere in the query to include the stylesheet, for example: <a href="http://lab.hakim.se/reveal-js?print-pdf">lab.hakim.se/reveal-js?print-pdf</a>.</li>
<li>Open the in-browser print dialog (CMD+P).</li>
<li>Change the <strong>Destination</strong> setting to <strong>Save as PDF</strong>.</li>
<li>Change the <strong>Layout</strong> to <strong>Landscape</strong>.</li>
<li>Change the <strong>Margins</strong> to <strong>None</strong>.</li>
<li>Click <strong>Save</strong>.</li>
</ol>

<p><img src="https://s3.amazonaws.com/hakim-static/reveal-js/pdf-print-settings.png" alt="Chrome Print Settings"></p>

<h2>Theming</h2>

<p>The framework comes with a few different themes included:</p>

<ul>
<li>default: Gray background, white text, blue links</li>
<li>beige: Beige background, dark text, brown links</li>
<li>sky: Blue background, thin white text, blue links</li>
<li>night: Black background, thick white text, orange links</li>
<li>serif: Cappuccino background, gray text, brown links</li>
<li>simple: White background, black text, blue links</li>
<li>solarized: Cream-colored background, dark green text, blue links</li>
</ul>

<p>Each theme is available as a separate stylesheet. To change theme you will need to replace <strong>default</strong> below with your desired theme name in index.html:</p>

<p><code>html
&lt;link rel=&quot;stylesheet&quot; href=&quot;css/theme/default.css&quot; id=&quot;theme&quot;&gt;
</code></p>

<p>If you want to add a theme of your own see the instructions here: <a href="https://github.com/hakimel/reveal.js/blob/master/css/theme/README.md">/css/theme/README.md</a>.</p>

<h2>Speaker Notes</h2>

<p>reveal.js comes with a speaker notes plugin which can be used to present per-slide notes in a separate browser window. The notes window also gives you a preview of the next upcoming slide so it may be helpful even if you haven&#39;t written any notes. Press the &#39;s&#39; key on your keyboard to open the notes window.</p>

<p>Notes are defined by appending an <code>&lt;aside&gt;</code> element to a slide as seen below. You can add the <code>data-markdown</code> attribute to the aside element if you prefer writing notes using Markdown.</p>

<p>When used locally, this feature requires that reveal.js <a href="#full-setup">runs from a local web server</a>.</p>

<p>```html
<section>
    <h2>Some Slide</h2></p>

<pre><code>&lt;aside class=&quot;notes&quot;&gt;
    Oh hey, these are some notes. They&#39;ll be hidden in your presentation, but you can see them if you open the speaker notes window (hit &#39;s&#39; on your keyboard).
&lt;/aside&gt;
</code></pre>

<p></section>
```</p>

<p>If you&#39;re using the external Markdown plugin, you can add notes with the help of a special delimiter:</p>

<p>```html
<section data-markdown="example.md" data-separator="^\n\n\n" data-vertical="^\n\n" data-notes="^Note:"></section></p>

<h1>Title</h1>

<h2>Sub-title</h2>

<p>Here is some content...</p>

<p>Note:
This will only display in the notes window.
```</p>

<h2>Server Side Speaker Notes</h2>

<p>In some cases it can be desirable to run notes on a separate device from the one you&#39;re presenting on. The Node.js-based notes plugin lets you do this using the same note definitions as its client side counterpart. Include the required scripts by adding the following dependencies:</p>

<p>```javascript
Reveal.initialize({
    ...</p>

<pre><code>dependencies: [
    { src: &#39;socket.io/socket.io.js&#39;, async: true },
    { src: &#39;plugin/notes-server/client.js&#39;, async: true }
]
</code></pre>

<p>});
```</p>

<p>Then:</p>

<ol>
<li>Install <a href="http://nodejs.org/">Node.js</a></li>
<li>Run <code>npm install</code></li>
<li>Run <code>node plugin/notes-server</code></li>
</ol>

<h2>Multiplexing</h2>

<p>The multiplex plugin allows your audience to view the slides of the presentation you are controlling on their own phone, tablet or laptop. As the master presentation navigates the slides, all client presentations will update in real time. See a demo at <a href="http://revealjs.jit.su">http://revealjs.jit.su/</a>.</p>

<p>The multiplex plugin needs the following 3 things to operate:</p>

<ol>
<li>Master presentation that has control</li>
<li>Client presentations that follow the master</li>
<li>Socket.io server to broadcast events from the master to the clients</li>
</ol>

<p>More details:</p>

<h4>Master presentation</h4>

<p>Served from a static file server accessible (preferably) only to the presenter. This need only be on your (the presenter&#39;s) computer. (It&#39;s safer to run the master presentation from your own computer, so if the venue&#39;s Internet goes down it doesn&#39;t stop the show.) An example would be to execute the following commands in the directory of your master presentation: </p>

<ol>
<li><code>npm install node-static</code></li>
<li><code>static</code></li>
</ol>

<p>If you want to use the speaker notes plugin with your master presentation then make sure you have the speaker notes plugin configured correctly along with the configuration shown below, then execute <code>node plugin/notes-server</code> in the directory of your master presentation. The configuration below will cause it to connect to the socket.io server as a master, as well as launch your speaker-notes/static-file server.</p>

<p>You can then access your master presentation at <code>http://localhost:1947</code></p>

<p>Example configuration:
```javascript
Reveal.initialize({
    // other options...</p>

<pre><code>multiplex: {
    // Example values. To generate your own, see the socket.io server instructions.
    secret: &#39;13652805320794272084&#39;, // Obtained from the socket.io server. Gives this (the master) control of the presentation
    id: &#39;1ea875674b17ca76&#39;, // Obtained from socket.io server
    url: &#39;revealjs.jit.su:80&#39; // Location of socket.io server
},

// Don&#39;t forget to add the dependencies
dependencies: [
    { src: &#39;//cdnjs.cloudflare.com/ajax/libs/socket.io/0.9.10/socket.io.min.js&#39;, async: true },
    { src: &#39;plugin/multiplex/master.js&#39;, async: true },

    // and if you want speaker notes
    { src: &#39;plugin/notes-server/client.js&#39;, async: true }

    // other dependencies...
]
</code></pre>

<p>});
```</p>

<h4>Client presentation</h4>

<p>Served from a publicly accessible static file server. Examples include: GitHub Pages, Amazon S3, Dreamhost, Akamai, etc. The more reliable, the better. Your audience can then access the client presentation via <code>http://example.com/path/to/presentation/client/index.html</code>, with the configuration below causing them to connect to the socket.io server as clients.</p>

<p>Example configuration:
```javascript
Reveal.initialize({
    // other options...</p>

<pre><code>multiplex: {
    // Example values. To generate your own, see the socket.io server instructions.
    secret: null, // null so the clients do not have control of the master presentation
    id: &#39;1ea875674b17ca76&#39;, // id, obtained from socket.io server
    url: &#39;revealjs.jit.su:80&#39; // Location of socket.io server
},

// Don&#39;t forget to add the dependencies
dependencies: [
    { src: &#39;//cdnjs.cloudflare.com/ajax/libs/socket.io/0.9.10/socket.io.min.js&#39;, async: true },
    { src: &#39;plugin/multiplex/client.js&#39;, async: true }

    // other dependencies...
]
</code></pre>

<p>});
```</p>

<h4>Socket.io server</h4>

<p>Server that receives the slideChanged events from the master presentation and broadcasts them out to the connected client presentations. This needs to be publicly accessible. You can run your own socket.io server with the commands:</p>

<ol>
<li><code>npm install</code></li>
<li><code>node plugin/multiplex</code></li>
</ol>

<p>Or you use the socket.io server at <a href="http://revealjs.jit.su">http://revealjs.jit.su</a>.</p>

<p>You&#39;ll need to generate a unique secret and token pair for your master and client presentations. To do so, visit <code>http://example.com/token</code>, where <code>http://example.com</code> is the location of your socket.io server. Or if you&#39;re going to use the socket.io server at <a href="http://revealjs.jit.su">http://revealjs.jit.su</a>, visit <a href="http://revealjs.jit.su/token">http://revealjs.jit.su/token</a>.</p>

<p>You are very welcome to point your presentations at the Socket.io server running at <a href="http://revealjs.jit.su">http://revealjs.jit.su</a>, but availability and stability are not guaranteed. For anything mission critical I recommend you run your own server. It is simple to deploy to nodejitsu, heroku, your own environment, etc.</p>

<h5>socket.io server as file static server</h5>

<p>The socket.io server can play the role of static file server for your client presentation, as in the example at <a href="http://revealjs.jit.su">http://revealjs.jit.su</a>. (Open <a href="http://revealjs.jit.su">http://revealjs.jit.su</a> in two browsers. Navigate through the slides on one, and the other will update to match.) </p>

<p>Example configuration:
```javascript
Reveal.initialize({
    // other options...</p>

<pre><code>multiplex: {
    // Example values. To generate your own, see the socket.io server instructions.
    secret: null, // null so the clients do not have control of the master presentation
    id: &#39;1ea875674b17ca76&#39;, // id, obtained from socket.io server
    url: &#39;example.com:80&#39; // Location of your socket.io server
},

// Don&#39;t forget to add the dependencies
dependencies: [
    { src: &#39;//cdnjs.cloudflare.com/ajax/libs/socket.io/0.9.10/socket.io.min.js&#39;, async: true },
    { src: &#39;plugin/multiplex/client.js&#39;, async: true }

    // other dependencies...
]
</code></pre>

<p>```</p>

<p>It can also play the role of static file server for your master presentation and client presentations at the same time (as long as you don&#39;t want to use speaker notes). (Open <a href="http://revealjs.jit.su">http://revealjs.jit.su</a> in two browsers. Navigate through the slides on one, and the other will update to match. Navigate through the slides on the second, and the first will update to match.) This is probably not desirable, because you don&#39;t want your audience to mess with your slides while you&#39;re presenting. ;)</p>

<p>Example configuration:
```javascript
Reveal.initialize({
    // other options...</p>

<pre><code>multiplex: {
    // Example values. To generate your own, see the socket.io server instructions.
    secret: &#39;13652805320794272084&#39;, // Obtained from the socket.io server. Gives this (the master) control of the presentation
    id: &#39;1ea875674b17ca76&#39;, // Obtained from socket.io server
    url: &#39;example.com:80&#39; // Location of your socket.io server
},

// Don&#39;t forget to add the dependencies
dependencies: [
    { src: &#39;//cdnjs.cloudflare.com/ajax/libs/socket.io/0.9.10/socket.io.min.js&#39;, async: true },
    { src: &#39;plugin/multiplex/master.js&#39;, async: true },
    { src: &#39;plugin/multiplex/client.js&#39;, async: true }

    // other dependencies...
]
</code></pre>

<p>});
```</p>

<h2>Leap Motion</h2>

<p>The Leap Motion plugin lets you utilize your <a href="https://www.leapmotion.com/">Leap Motion</a> device to control basic navigation of your presentation. The gestures currently supported are:</p>

<h5>1 to 2 fingers</h5>

<p>Pointer &mdash; Point to anything on screen. Move your finger past the device to expand the pointer.</p>

<h5>1 hand + 3 or more fingers (left/right/up/down)</h5>

<p>Navigate through your slides. See config options to invert movements.</p>

<h5>2 hands upwards</h5>

<p>Toggle the overview mode. Do it a second time to exit the overview.</p>

<h4>Config Options</h4>

<p>You can edit the following options:</p>

<p>| Property          | Default           | Description
| ----------------- |:-----------------:| :-------------
| autoCenter        | true              | Center the pointer based on where you put your finger into the leap motions detection field.
| gestureDelay      | 500               | How long to delay between gestures in milliseconds.
| naturalSwipe      | true              | Swipe as though you were touching a touch screen. Set to false to invert.
| pointerColor      | #00aaff           | The color of the pointer.
| pointerOpacity    | 0.7               | The opacity of the pointer.
| pointerSize       | 15                | The minimum height and width of the pointer.
| pointerTolerance  | 120               | Bigger = slower pointer.</p>

<p>Example configuration:
```js
Reveal.initialize({</p>

<pre><code>// other options...

leap: {
    naturalSwipe   : false,    // Invert swipe gestures
    pointerOpacity : 0.5,      // Set pointer opacity to 0.5
    pointerColor   : &#39;#d80000&#39; // Red pointer
},

dependencies: [
    { src: &#39;plugin/leap/leap.js&#39;, async: true }
]
</code></pre>

<p>});
```</p>

<h2>MathJax</h2>

<p>If you want to display math equations in your presentation you can easily do so by including this plugin. The plugin is a very thin wrapper around the <a href="http://www.mathjax.org/">MathJax</a> library. To use it you&#39;ll need to include it as a reveal.js dependency, <a href="#dependencies">find our more about dependencies here</a>.</p>

<p>The plugin defaults to using <a href="http://en.wikipedia.org/wiki/LaTeX">LaTeX</a> but that can be adjusted through the <code>math</code> configuration object. Note that MathJax is loaded from a remote server. If you want to use it offline you&#39;ll need to download a copy of the library and adjust the <code>mathjax</code> configuration value. </p>

<p>Below is an example of how the plugin can be configured. If you don&#39;t intend to change these values you do not need to include the <code>math</code> config object at all.</p>

<p>```js
Reveal.initialize({</p>

<pre><code>// other options ...

math: {
    mathjax: &#39;http://cdn.mathjax.org/mathjax/latest/MathJax.js&#39;,
    config: &#39;TeX-AMS_HTML-full&#39;  // See http://docs.mathjax.org/en/latest/config-files.html
},

dependencies: [
    { src: &#39;plugin/math/math.js&#39;, async: true }
]
</code></pre>

<p>});
```</p>

<p>Read MathJax&#39;s documentation if you need <a href="http://docs.mathjax.org/en/latest/start.html#secure-access-to-the-cdn">HTTPS delivery</a> or serving of <a href="http://docs.mathjax.org/en/latest/configuration.html#loading-mathjax-from-the-cdn">specific versions</a> for stability.</p>

<h2>Installation</h2>

<p>The <strong>basic setup</strong> is for authoring presentations only. The <strong>full setup</strong> gives you access to all reveal.js features and plugins such as speaker notes as well as the development tasks needed to make changes to the source.</p>

<h3>Basic setup</h3>

<p>The core of reveal.js is very easy to install. You&#39;ll simply need to download a copy of this repository and open the index.html file directly in your browser.</p>

<ol>
<li><p>Download the latest version of reveal.js from <a href="https://github.com/hakimel/reveal.js/releases">https://github.com/hakimel/reveal.js/releases</a></p></li>
<li><p>Unzip and replace the example contents in index.html with your own</p></li>
<li><p>Open index.html in a browser to view it</p></li>
</ol>

<h3>Full setup</h3>

<p>Some reveal.js features, like external markdown and speaker notes, require that presentations run from a local web server. The following instructions will set up such a server as well as all of the development tasks needed to make edits to the reveal.js source code.</p>

<ol>
<li><p>Install <a href="http://nodejs.org/">Node.js</a></p></li>
<li><p>Install <a href="http://gruntjs.com/getting-started#installing-the-cli">Grunt</a></p></li>
<li><p>Clone the reveal.js repository
<code>sh
$ git clone https://github.com/hakimel/reveal.js.git
</code></p></li>
<li><p>Navigate to the reveal.js folder
<code>sh
$ cd reveal.js
</code></p></li>
<li><p>Install dependencies
<code>sh
$ npm install
</code></p></li>
<li><p>Serve the presentation and monitor source files for changes
<code>sh
$ grunt serve
</code></p></li>
<li><p>Open <a href="http://localhost:8000">http://localhost:8000</a> to view your presentation</p></li>
</ol>

<p>You can change the port by using <code>grunt serve --port 8001</code>.</p>

<h3>Folder Structure</h3>

<ul>
<li><strong>css/</strong> Core styles without which the project does not function</li>
<li><strong>js/</strong> Like above but for JavaScript</li>
<li><strong>plugin/</strong> Components that have been developed as extensions to reveal.js</li>
<li><strong>lib/</strong> All other third party assets (JavaScript, CSS, fonts)</li>
</ul>

<h3>Contributing</h3>

<p>Please keep the <a href="http://github.com/hakimel/reveal.js/issues">issue tracker</a> limited to <strong>bug reports</strong>, <strong>feature requests</strong> and <strong>pull requests</strong>. If you are reporting a bug make sure to include information about which browser and operating system you are using as well as the necessary steps to reproduce the issue.</p>

<p>If you have personal support questions use <a href="http://stackoverflow.com/questions/tagged/reveal.js">StackOverflow</a>.</p>

<h4>Pull requests</h4>

<ul>
<li>Should follow the coding style of the file you work in, most importantly:

<ul>
<li>Tabs to indent</li>
<li>Single-quoted strings</li>
</ul></li>
<li>Should be made towards the <strong>dev branch</strong></li>
<li>Should be submitted from a feature/topic branch (not your master)</li>
<li>Should not include the minified <strong>reveal.min.js</strong> file</li>
</ul>

<h2>License</h2>

<p>MIT licensed</p>

<p>Copyright (C) 2014 Hakim El Hattab, http://hakim.se</p>