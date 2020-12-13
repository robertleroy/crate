## Vue 3 Starter
[Vue Cli](#vue-cli) | [Vite](#vite) | [App](#app) | [Vue-Router](#vue-router) | [Vuex](#vuex)
[](#)

### Vue Cli
``` js
vue create <project-name>
```

### Vite
``` js
npm init vite-app <project-name>
cd <project-name>
npm install
npm run dev

/* React Template */
npm init vite-app --template react <project-name>

/* Utilities */
npm install -D sass
npm install vue-router@next
npm install vuex@next
```

### App
``` js
/* main.js */

import { createApp } from 'vue'
import App from './App.vue'
// import router from './router/router'
// import store from './store/store'
// import './index.css'


createApp(App)
  // .use(router)
  // .use(store)
  .mount('#app')
```

``` vue
/* App.vue */

<script>
  export default {
    name: 'App',
    data() {
      return {
        title: "Vue 3!"
      }
    }
  }
</script>

<template>
  <div id="appgrid" v-cloak>
    <header>
      <h4>{{title}}</h4>

      <!-- <div id="nav">
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
      </div> -->
    </header>

    <main>
      <!-- <router-view v-slot="{ Component }">
        <transition name='fade' mode='out-in'>
          <component :is="Component"/>
        </transition>
      </router-view> -->
    </main>
  </div> 
</template>

<style lang="scss">
  @import './scss/baseline';

  #appgrid {
    height: 100vh;
    display: grid;
    grid-template-rows: auto 1fr;
  }

  header, main {
    padding: 1rem 2rem;
  }

  header {
    display: grid;
    grid-auto-flow: column;
    justify-content: space-between;

    @include shadow(3);
  }
</style>
```

### Vue-Router

``` js
/* ./router/router.js */

import { createRouter, createWebHistory } from 'vue-router';
import Home from '../views/Home.vue';
import About from '../views/About.vue';

const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: About
  },
  { 
    path: '/:pathMatch(.*)*', 
    redirect: '/'
  }
]

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})

export default router;
```

``` html
<!-- Navigation -->
<div id="nav">
  <router-link to="/">Home</router-link> |
  <router-link to="/about">About</router-link>
</div>

<!-- Animated Router Transition -->
<router-view v-slot="{ Component }">
  <transition name='fade' mode='out-in'>
    <component :is="Component"/>
  </transition>
</router-view>
```


### Vuex

``` js
/* ./store/store */

import { createStore } from 'vuex'

export default createStore({
  state: {
    count: 0,
  },
  getters: {},
  mutations: {},
  actions: {}
})
```

``` js
/* Options.api */

<script>  
  // import { mapGetters } from "vuex";
  
  export default {
    name: 'Component',
    data() {
      return {};
    },
    computed: {
      // ...mapGetters(['count']),
      
      count() {
        return this.$store.getters.count;
      }
    },
    methods: { 
      increment() {
        this.$store.commit('increment');
      },
      decrement() {
        this.$store.commit('decrement');
      }
    },
  };
</script>


/* Composition.api */

<script>
import { computed } from "vue";
import { useStore } from "vuex";

export default {
  setup() {
    const store = useStore();
    const count = computed(() => store.getters.count);

    function increment() {
      store.commit("increment");
    }
    
    function decrement() {
      store.commit("decrement");
    }
    
    return { title, count, increment, decrement };
  }
}
</script>

```
