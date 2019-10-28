## Copy

Add `v-copy` directive to a button.   
Add target elements `ID` as an `arg`.   
`v-copy:lorem`

#### app.html

``` html
<button v-copy:lorem>copy</button>

<p id="lorem">
	Lorem ipsum dolor sit... 
</p>
```

#### app.js
``` js
import { copy } from "./directives/copy";

directives: {
  "copy": copy,
},
```


```js
export const copy = ("copy", {
  bind: function (el, binding) {

    if (!document.getElementById(binding.arg)) {
      console.log("error: element does not exist");
      return;
    }

    const copyToClipboard = function(e) {
      try {
        var elToCopy = document.getElementById(binding.arg);
        var range = document.createRange();  
        range.selectNodeContents(elToCopy);  
        window.getSelection().removeAllRanges();
        window.getSelection().addRange(range); 
        document.execCommand("copy");
        window.getSelection().removeAllRanges(); 
      } catch {
        console.log("error: an error occured");
      }
    }
    el.addEventListener("pointerdown", copyToClipboard);
  },
  unbind: function (el) {
    el.removeEventListener('pointerdown', copyToClipboard); 
  }
});
```
