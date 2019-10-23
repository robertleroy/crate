## Menu Button

#### app.html
``` html
<menu-btn></menu-btn>
```

#### app.js
```js
const MenuBtn = {
  template: `
    <div class="menuBtn">
      <div class="bar"></div>
      <div class="bar"></div>
      <div class="bar"></div>
    </div>`
}

~~~

components: {
  "menuBtn": MenuBtn
},
```

#### app.scss
``` scss
  .menuBtn {
    padding: 6px 3px;
    display: inline-block;
    height: 24px;
    width: 24px;
    @extend .btn;    
    
    .bar {
      height: 2px;
      margin-bottom: 3px;
      background: currentColor;
      
      &:last-child {
        margin: 0;
      }
    }
  }
  ```
  
