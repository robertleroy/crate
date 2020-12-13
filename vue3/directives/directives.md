## General Directives
> Vue 2 & Vue 3 ???

[v-focus](#v-focus)  
[v-copy](#v-copy)  

#### v-focus
``` js
/* vue 3 */
app.directive('focus', {
  mounted(el) {
    el.focus();
  }
})

/* <input v-focus type="text"> */
```


#### v-copy
``` js
export const copy = ("copy", {
  // /* vue 2 */ bind: function (el, binding) { 
  /* vue 3 */ mounted: function (el, binding) {

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
  }
});

// import { copy } from './directives/copy';

// directives: {
//   "copy": copy,
// },

// <div v-copy:lorem
//     class="icon btn btnCopy">content_copy</div>

// <p id="lorem">Lorem ipsum dolor ...</p>
```
