## Online Indicator

#### index.js
``` js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Vue!',
    connected: false,
  },  
  methods: {
    connection() {
      // console.log("isOnline");  
      this.connected = navigator.onLine;
    }    
  },    
  mounted: function()  {  
    // console.log("mounted");
    window.addEventListener("online", this.connection);
    window.addEventListener("offline", this.connection);
    this.connection();
  }
})
```

#### index.html
``` html
<div id="app">
  
  <header>  
    <h4>
      {{ message }} 
      <small>
        &nbsp  ~ &nbsp  {{ connected ? 'online' : 'offline ' }}
      </small>      
    </h4>
  </header>
  
  <main>   
    <div class="row">
      <div class="led"
           :class="connected ? 'green' : 'red'"></div>
      <div>{{ connected ? 'online' : 'offline ' }}</div>
    </div>
    
    <div class="row">
      <div class="test"></div>
    </div>
  </main>
  
</div>  <!-- app -->
```

#### style.css
``` css
#app {
  height: 100vh;
  display: grid;
  grid-template-rows: auto 1fr;
}

header {
  padding: 1rem 2rem;
}

main {
  padding: 1rem 2rem 2rem;
}


.row {
  // height: 8rem;
  // background: black;
  
  display: grid;
  place-items: center center;
}

.led {
  height: 2rem;
  width: 2rem;
  border-radius: 1rem;
}

.red {
  background: #ff3333;
  box-shadow:
    inset 0 0 1rem #660000,
    0 0 1px 1px #000000,
    1px 2px 1rem 0.5rem #ff0000cc;
}

.green {
  background: #33ff33;  
  box-shadow: 
    inset 0 0 1rem #006600,
    0 0 1px 1px #000000cc,
    1px 2px 1rem 0.5rem #00ff00cc;
}

.test {
  height: 2rem;
  width: 2rem;
  border-radius: 1rem;
  background: #ff3333;
  box-shadow:
    inset 0 0 1rem #660000,
    0 0 1px 1px #000000,
    1px 2px 1rem 2px #ff0000cc;
}
```
