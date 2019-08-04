## Vue Routing

#### main.js
```js
// main.js

import Vue from "vue";
import VueRouter from 'vue-router'
import App from "./App.vue";

import routes from './routes';
import SvgIcon from './components/icons/SvgIcon';
Vue.component('svg-icon', SvgIcon);

Vue.config.productionTip = false;

Vue.use(VueRouter)

const router = new VueRouter({mode: 'history', routes});


new Vue({
  router,
  render: h => h(App),
}).$mount("#app");
```

#### routes.js
```js
// routes.js

import Home from "./pages/Home";
import About from "./pages/About";
import Error from './pages/404.vue';


const routes = [
  { path: '/home', component: Home, name: 'home' },
  { path: '/about', component: About, name: 'about' },
  { path: '*', redirect: '/home' },
  { path: '/404', component: Error, name: '404' },
];

export default routes;
```

#### app.vue
```html

<template>
  <div id="app">
    ~~~

    <nav>
      <router-link to='/home'>Home</router-link>
      <router-link to='/about'>About</router-link>
    </nav> 

    <main> 
      <transition name="fade"  mode="out-in">
        <router-view></router-view>
      </transition>
    </main>
    
    ~~~

  </div>  
</template>


<script>
export default {
  name: "App",
  data() {
    return {
      title: "Hello World!",
    };
  }
};
</script>


<style lang="scss">
  @import "./scss/baseline";

  ~~~

  nav {
    padding: 1rem 2rem;

    a {
      display: block;
      color: $linkColor;      
    }

    .router-link-active {
      color: complement($linkColor);

      &:hover {
        color: scale-color(complement($linkColor), $alpha: -40%);
      }
    }
  }
  
  ~~~

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

</style>
```
