#### Autogrow Textarea

``` html
<textarea class="textbox" rows="1"
  v-model="item.text" 
  placeholder='required' 
  spellcheck="false" 
  onfocus="this.style.height=this.scrollHeight+'px'"
  oninput="this.style.height=this.scrollHeight+'px'">
</textarea>
```
