# Enhanced Highlight.js for personal usage

Forked from [isagalaev/highlight.js][ih]

[ih]: https://github.com/isagalaev/highlight.js

Added line numbers display, reference [Highlight.js line numbers][hln]

[hln]: http://www.minh.io/tech/2013/08/17/highlightjs-line-numbers/

Also added some features and styles to improve experience of line numbers display.
Hence, place `lineNumbers` in the class property of `code` tag:

```html
<pre>
<code class="lineNumbers">@requires_authorization
def somefunc(param1='', param2=0):
    r'''A docstring'''
    if param1 &gt; param2: # interesting
        print 'Gre\'ater'
    return (param2 - param1 + 1 + 0b10l) or None

class SomeClass:<br>    pass

&gt;&gt;&gt; message = '''interpreter
... prompt'''
</code></pre>
```

---

# Highlight.js

Highlight.js highlights syntax in code examples on blogs, forums and,
in fact, on any web page. It's very easy to use because it works
automatically: finds blocks of code, detects a language, highlights it.

Autodetection can be fine tuned when it fails by itself (see "Heuristics").


## Basic usage

Link the library and a stylesheet from your page and hook highlighting to
the page load event:

```html
<link rel="stylesheet" href="styles/default.css">
<script src="highlight.pack.js"></script>
<script>hljs.initHighlightingOnLoad();</script>
```

This will highlight all code on the page marked up as `<pre><code> .. </code></pre>`.
If you use different markup or need to apply highlighting dynamically, read
"Custom initialization" below.

- You can download your own customized version of "highlight.pack.js" or
  use the hosted one as described on the download page:
  <http://highlightjs.org/download/>

- Style themes are available in the download package or as hosted files.
  To create a custom style for your site see the class reference in the file
  [CSS classes reference][cr] from the downloaded package.

[cr]: http://highlightjs.readthedocs.org/en/latest/css-classes-reference.html


## node.js

Highlight.js can be used under node.js. The package with all supported languages is
installable from NPM:

    npm install highlight.js

Alternatively, you can build it from the source with only languages you need:

    python3 tools/build.py -tnode lang1 lang2 ..

Using the library:

```javascript
var hljs = require('highlight.js');

// If you know the language
hljs.highlight(lang, code).value;

// Automatic language detection
hljs.highlightAuto(code).value;
```


## AMD

Highlight.js can be used with an AMD loader.  You will need to build it from
source in order to do so:

```bash
$ python3 tools/build.py -tamd lang1 lang2 ..
```

Which will generate a `build/highlight.pack.js` which will load as an AMD
module with support for the built languages and can be used like so:

```javascript
require(["highlight.js/build/highlight.pack"], function(hljs){

  // If you know the language
  hljs.highlight(lang, code).value;

  // Automatic language detection
  hljs.highlightAuto(code).value;
});
```


## Tab replacement

You can replace TAB ('\x09') characters used for indentation in your code
with some fixed number of spaces or with a `<span>` to give them special
styling:

```html
<script type="text/javascript">
  hljs.configure({tabReplace: '    '}); // 4 spaces
  // ... or
  hljs.configure({tabReplace: '<span class="indent">\t</span>'});

  hljs.initHighlightingOnLoad();
</script>
```

## Custom initialization

If you use different markup for code blocks you can initialize them manually
with `highlightBlock(code)` function.
It takes a DOM element containing the code to highlight.

Initialization using, for example, jQuery might look like this:

```javascript
$(document).ready(function() {
  $('pre code').each(function(i, e) {hljs.highlightBlock(e)});
});
```

You can use `highlightBlock` to highlight blocks dynamically inserted into
the page. Just make sure you don't do it twice for already highlighted
blocks.

If your code container relies on `<br>` tags instead of line breaks (i.e. if
it's not `<pre>`) set the `useBR` option to `true`:

```javascript
hljs.configure({useBR: true});
$('div.code').each(function(i, e) {hljs.highlightBlock(e)});
```


## Heuristics

Autodetection of a code's language is done using a simple heuristic:
the program tries to highlight a fragment with all available languages and
counts all syntactic structures that it finds along the way. The language
with greatest count wins.

This means that in short fragments the probability of an error is high
(and it really happens sometimes). In this cases you can set the fragment's
language explicitly by assigning a class to the `<code>` element:

```html
<pre><code class="html">...</code></pre>
```

You can use class names recommended in HTML5: "language-html",
"language-php". Classes also can be assigned to the `<pre>` element.

To disable highlighting of a fragment altogether use "no-highlight" class:

```html
<pre><code class="no-highlight">...</code></pre>
```


## Export

File export.html contains a little program that allows you to paste in a code
snippet and then copy and paste the resulting HTML code generated by the
highlighter. This is useful in situations when you can't use the script itself
on a site.


## Meta

- Version: 8.0
- URL:     http://highlightjs.org/

For the license terms see LICENSE files.
For authors and contributors see AUTHORS.en.txt file.
