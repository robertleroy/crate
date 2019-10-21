## Vuex / Local Storage  
  
#### `const Version = "0.0.1"`  
This allows easy resetting of storage.   
Change in Version number triggers storage reset. 

``` js
const Version = "0.0.1";

const store = new Vuex.Store({
  state: {
    version: '',
  },
  getters: {
      
  },
  mutations: {
    initializeStore(state) {
      ...
    }
  },
  actions: {
      
  }
})
```

  
#### `initializeStore`  
Check if `const Version` matches `store.version`
1. if so, merge storage into `$store.state`.
2. if not, ignore storage and update  
`$store.state.version` number.

``` js
mutations: {

  initializeStore(state) { 

    if ( localStorage.getItem('store') ) {
      let store = JSON.parse( 
        localStorage.getItem('store') 
      );

      if ( store.version === Version ) {
        this.replaceState(
          Object.assign(state, store)
        );
      } else {
        state.version = Version;
      }
    }
  }

},
```  
   
#### `beforeCreate()`  
Call `initializeStore` and  subscribe to mutations.  
When `$state.store` is changed / gets mutation  =>  
save `state` to `store`.  

``` js
beforeCreate() {
  this.$store.commit('initializeStore');
  this.$store.subscribe((mutation, state) => {

    localStorage.setItem(
      'store', JSON.stringify(state)
    );

  });
},
```   

Alternatively, save select items in an object.  
Save the object to `store`.
* note ~ `Json.stringify( store )` instead of `state`.

``` js
beforeCreate() {
  this.$store.commit('initializeStore');
  this.$store.subscribe((mutation, state) => {

    let store = {
      version: state.version,
    };
    localStorage.setItem(
      'store', JSON.stringify(store)
    );
  });
},
```   
  
---
---   
#### app.js
``` js
import './style.scss';

import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);


const Version = "0.0.1";

const store = new Vuex.Store({
  state: {
    version: '',
    favorites: ["apples", "oranges"],    
  },
  getters: {
    favorites: state => {
      return state.favorites;
    }
  },

  mutations: {
    initializeStore(state) { 
			if ( localStorage.getItem('store') ) {
        let store = JSON.parse( 
          localStorage.getItem('store') 
        );

        if ( store.version === Version ) {
          this.replaceState(
            Object.assign(state, store)
          );
        } else {
          state.version = Version;
        }
			}
		},

    addFavorite (state, payload) {
      state.favorites.push(payload);
    },

    deleteFavorite (state, payload) {
      state.favorites = state.favorites.filter(x => {
        x !== payload
      })
    }
  },

  actions: {
    addFavAsync ({commit}, payload) {
      commit("addFavorite", payload);
    },

    deleteFavAsync ({commit}, payload) {
      commit("deleteFavorite", payload);
    }
  }
})


const app = new Vue({ 
  el: '#app', 
  store, 

  data: {
    title: 'Vuex LocalStorage',
    newItem: "",
    placeholder: "add favorite..."
  },

  computed: {
    version() {
      return this.$store.state.version;
    },
    
    favorites() {
      return this.$store.getters.favorites;
    },

  },

  methods: {

    addFav(item) {
      this.$store.dispatch("addFavAsync", item);
      this.newItem = "";
    },
    
    deleteFav(item) {
      this.$store.dispatch("deleteFavAsync", item);
    }
  },

  beforeCreate() {
    this.$store.commit('initializeStore');
    this.$store.subscribe((mutation, state) => {

      /*
      let store = {
        version: state.version,
      };
      localStorage.setItem(
        'store', JSON.stringify(store)
      );
      */
    
      localStorage.setItem(
        'store', JSON.stringify(state)
      );
    });
	},
  
  mounted() {
    console.log(this.$store.state.version, " | ",Version);
  }

});
```
