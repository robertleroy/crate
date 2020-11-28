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

/* Utilities */
npm install -D sass
npm install vue-router@next
```

### App
``` js
/* Main.js */

import { createApp } from 'vue'
import App from './App.vue'
import router from './router/router'
import './index.css'

createApp(App).use(router).mount('#app')
```

``` js
/* App.vue */

<template>
  <div id="App_Grid">
    <header>
      <h2>{{title}}</h2>

      <div id="nav">
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
      </div>
    </header>

    <main>
      <router-view v-slot="{ Component }">
        <transition name='fade' mode='out-in'>
          <component :is="Component"/>
        </transition>
      </router-view>
    </main>
  </div> 
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      title: "Vite!"
    }
  }
}
</script>

<style lang="scss">
@import './scss/baseline';

#App_Grid {
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
/* router/router.js */

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
