## Utilities

#### innerWidth
```js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Vue!',
    innerWidth: 0,
  },
  methods: {
    checkWidth() {
      this.innerWidth = window.innerWidth;
    }
  },
  mounted() {
    this.$nextTick(function() {
      window.addEventListener('resize', this.checkWidth);
    })
    
    this.checkWidth();              
  },
})
```
