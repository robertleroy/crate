## `Hilightjs`

1. import library (in directive)
2. add default style
3. add style

``` html
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.10/highlight.min.js"></script>
``` 

``` css
@import url("https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.10/styles/default.min.css");
@import url("https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.10/styles/solarized-dark.min.css");
```

Place v-highlightjs attribute on `pre` tag.  
Specify language in `class` or `lang`  
attributes of `code` tag.

Enter snippets:
1. directly with escaped code
2. interpolate with curly braces
3. interpolate into `v-highlightjs` attribute

``` html
<pre v-highlightjs="sourcecode">
  <code class="html"></code>
</pre>

<pre v-highlightjs>
	<code class="html">{{sourcecode}}</code>
</pre>
```

#### `app.js` 
``` js
import { highlightjs } from "./directives/highlightjs";


const app = new Vue({ 
  el: '#app',
  directives: {
    "highlightjs": highlightjs,
  },
	...
```  

#### `hilightjs directive`
``` js 
import hljs from 'highlightjs';

export const highlightjs = ("highlightjs", {
  deep: true,
  bind: function (el, binding) {
    let targets = el.querySelectorAll('code')
    targets.forEach((target) => {
      if (binding.value) {
        target.textContent = binding.value
      }
      hljs.highlightBlock(target)
    })
  },
  componentUpdated: function (el, binding) {
    let targets = el.querySelectorAll('code')
    targets.forEach((target) => {
      if (binding.value) {
        target.textContent = binding.value
        hljs.highlightBlock(target)
      }
    })
  }
})
```
