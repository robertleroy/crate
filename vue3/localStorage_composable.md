## localStorage_composable

``` js
/* store.js */

import { ref, computed, watch } from "vue";
const Version = "0.1.0";
const STORE_KEY = "test_state";

/* state */
const state = ref({
  version: "",
  count: 0,
});

/* getters */
const count = computed(() => state.value.count)

/* mutaions */
const setCount = function (i) {
  state.value.count += i;
}

// #region LocalStorage 
function init() {
  const storageObj = JSON.parse(localStorage.getItem(STORE_KEY));
      
  if (storageObj) {
    if ( storageObj.version === Version ) {
      console.log("setting store");
      Object.assign(state.value, storageObj);
    } else {
      console.log("resetting store");
      state.value.version = Version;
    }
  } else {
    state.value.version = Version;
  }
}

watch(state.value, () => {
  localStorage.setItem(STORE_KEY, JSON.stringify(state.value));
})
// #endregion LocalStorage 

export default { 
  count, setCount, state, init 
};
```

``` js
/* app.vue */

import { ref, onMounted } from 'vue'

    setup () {      
    const { count, setCount, init } = store;

    onMounted(() => {
      init();
    })

    return {
      count, setCount, init
    }
  }

  /* 
  <div class='number'>
    <div class="icon btn" @click="setCount(-1)">remove</div>
    <div >{{count}}</div>
    <div class="icon btn" @click="setCount(1)">add</div>    
  </div>
  */
  ```
  
  #### Narrative
1 The `store` is split into 3 parts:
  `state` is a `ref` (easier to manipulate than `responsive` here)
  `getters` use `computed` property to clone values
  `mutations` single point to set state from with its scope.
  
2 `localStorage` loads on `init()` and updates as `watch` detects changes in `state.value`

###### Loading
1 load `storageObj` and check if it is null.
2 if `storageObj` check `storageObj.version` against `Version`
3 If version match, then populate `state` with `storageObj`
4 Else update version number and leave state with default values. (effective reset)
5 If null `storageObj`, update version number, which triggers `watch` to set `localStorage` with default values.
  
