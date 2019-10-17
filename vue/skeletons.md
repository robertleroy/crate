## Vue / Vuex Skeleton

#### cdn
``` html
<script src="https://unpkg.com/vue"></script>
<script src="https://unpkg.com/vuex"></script>
```

#### vue
``` js
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

const moduleA = {
    state: { 
        
    },
    mutations: {
        
    },
    getters: {
        
    },
    actions: {
        
    }
}

const moduleB = {
    state: {
        
    },
    mutations: {
        
    },
    getters: {
        
    },
    actions: {
        
    }
}

const store = new Vuex.Store({
    state: {
        count: 2
    },
    mutations: {
        
    },
    getters: {
        
    },
    actions: {
        
    }
})


new Vue({ 
    el: '#app',
    store,
    data: {
    },
    computed: {
    }
});
```
