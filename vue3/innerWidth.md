## Window InnerWidth / InnerHeight

``` js
var app = new Vue({
  el: '#app',
  data: {
    innerWidth: 0,
    innerHeight: 0,
  },
  methods: {
    checkSize() {
      this.innerWidth = window.innerWidth;
      this.innerHeight = window.innerHeight;
    }
  },
  mounted() {
    this.$nextTick(function() {
      window.addEventListener('resize', this.checkSize);
    })
    
    this.checkSize();              
  },
})
