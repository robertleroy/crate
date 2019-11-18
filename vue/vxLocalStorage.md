## vxLocalStorage as Vuex Plugin

1. import into store
2. add a reference to version in state
3. add 'updateVersion' mutation

#### store.js
``` js
import Vue from 'vue';
import Vuex from 'vuex';

import { vxLocalStorage } from "./vxLocalStorage.js"

Vue.use(Vuex);

export const store = new Vuex.Store({
  plugins: [vxLocalStorage],
  state: {
    version: "",
  },
  getters: { 
      
  },
  mutations: {
    updateVersion(state, payload) {
      state.version = payload;
    },      
  },  
  actions: {
      
  }
});
```

#### vxLocalStorage.js
``` js
export const vxLocalStorage = store => {
  const store_key = "app";
  const Version = "0.0.2";

  store.subscribe((mutation, state) => {
    /* ********** */
    localStorage.setItem(
      store_key, JSON.stringify(state)
    );

  })

  let storage_obj = JSON.parse( 
    localStorage.getItem(store_key)
  );

  if ( storage_obj ) {   
    if ( storage_obj.version === Version ) { 
      // Object.assign(store.state, storage_obj);      
      store.replaceState(storage_obj);
      console.log(store_key, "version:", store.state.version);
    } else {      
      store.commit("updateVersion", Version);      
      console.log(store_key, "new version:", store.state.version);
    }
  }  
}
```
