## storagePlugin as Vuex Plugin

1. import into store
2. add a reference to version in state
3. add 'updateVersion' mutation

#### store.js
``` js
import Vue from 'vue';
import Vuex from 'vuex';

import { storagePlugin } from "./storagePlugin.js"

Vue.use(Vuex);

export const store = new Vuex.Store({
  plugins: [storagePlugin],
  state: {
    version: "",
  },
  getters: {},
  mutations: {
    updateVersion(state, payload) {
      state.version = payload;
    },      
  },  
  actions: {}
});
```

#### storagePlugin.js
``` js
export const storagePlugin = store => {
  const store_key = "app";
  const Version = "0.0.1";

  store.subscribe((mutation, state) => {

    let obj = {
      version: state.version,
      volume: state.volume,
      currentPanel: state.currentPanel,
      autoplay: state.autoplay,
    };
    
    localStorage.setItem(
      store_key, JSON.stringify(obj)
    );

  })

  let storage_obj = JSON.parse( 
    localStorage.getItem(store_key)
  );
  
  if ( storage_obj ) {   
    if ( storage_obj.version === Version ) { 
      Object.assign(store.state, storage_obj);      
      // store.replaceState(storage_obj);
    } else {      
      store.commit("updateVersion", Version);  
    }
  }  
}
```
