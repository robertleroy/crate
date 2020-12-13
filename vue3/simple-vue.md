## Simple Vue 3 [non-cli]

``` html
/* index.html */

<!DOCTYPE html>
<html lang='en'>
<head>
  <meta charset='UTF-8'>
  <meta name='viewport' content='width=device-width, initial-scale=1.0'>
  <meta http-equiv='X-UA-Compatible' content='ie=edge'>
  <title>Document</title>
  <link rel="icon" href="./favicon.ico">
  <link rel='stylesheet' href='./css/style.css'>
</head>
  
<body>
  <div id='app'>
    <header>
      <h4>{{title}}</h4>
      <input v-focus type="text" 
        v-model="testStr" 
        placeholder="test string">
    </header>

    <main>
      <div>{{testStr || 'Main'}}</div>        
      <div>
        <modal-button></modal-button>
      </div>
    </main>
  </div> <!-- app -->

  <script src="./js/vue3.js"></script>
  <script src="./js/app.js"></script>
</body>
</html>
```
``` js
/* app.js */

const app = Vue.createApp({

  data() {
    return {
      title: " Vue!",
      testStr: '',
    }
  },  
})

app.directive('focus', {
  mounted(el) {
    el.focus();
  }
})

app.component('modal-button', {
  template: `
    <button @click="modalOpen = true">
      teleport to "body": {{modalOpen}}
    </button>

    <teleport to="body">
      <div v-if="modalOpen" class="modal"
          @click.self="modalOpen = false">

        <div class="panel">
          <div>
            I'm a teleported modal! 
          </div>
            
          <div> teleport to "body": {{modalOpen}}</div>
          
          <button @click="modalOpen = false">
            Close
          </button>
        </div>

      </div>
    </teleport>
  `,
  data() {
    return { 
      modalOpen: false
    }
  }
})

app.mount('#app')
```

``` css 
/* ./scss/style.scss */

@import "./baseline";

#app {
  position: relative;
  height: 100vh;
  display: grid;
  grid-template-rows: auto 1fr;
}

header, main {
  padding: 1rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  
  @include shadow(1);
}

main { }

.modal {
  position: absolute;
  top: 0; right: 0; bottom: 0; left: 0;
  background-color: rgba(0,0,0,.5);

  display: grid;
  place-items: center center;
}

.modal .panel {
  display: grid;
  justify-content: center;
  align-content: center;
  gap: 0.5rem;
  background-color: $backgroundColor;
  width: 300px;
  height: 300px;
  padding: 1rem;

  button {
    margin-top: 2rem;
  }
}
```
