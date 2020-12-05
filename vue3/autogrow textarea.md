#### Autogrow Textarea

Can't figure out how to make it grow on draw, 
but will expand onfocus and grow oninput

``` html
<textarea class="textbox" rows="1"
  v-model="item.text" 
  placeholder='required' 
  spellcheck="false" 
  onfocus="this.style.height=this.scrollHeight+'px'"
  oninput="this.style.height=this.scrollHeight+'px'">
</textarea>
```
