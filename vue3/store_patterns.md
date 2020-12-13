## Store Patterns

[Pattern One](#pattern-one)    
[Pattern Two](#pattern-two)   
[Pattern Three](#pattern-three)   
[Pattern Four](#pattern-four)  

### Pattern One
``` js
/* readonly */

import { reactive, readonly } from "vue";

const state = reactive({
  count: 5
});

const increment = function () {
  state.count++;
}

export default { state: readonly(state), increment };
```
``` js
import store from '../store.js'

setup () {      
  const { state, increment } = store;

  return {
    state, increment
  }
}

/* <div>Count: {{state.count}}</div>  */

```

<br>

### Pattern Two
``` js
/* toRefs */

import { reactive, toRefs } from "vue";

const state = reactive({
  count: 5,
  isTrue: false,
});

const increment = function () {
  state.count++;
}

function toggleTruth() {
  state.isTrue = !state.isTrue
}

export default { ...toRefs(state), increment, toggleTruth };
```
``` js
import store from '../store.js'

setup () {      
  const { count, isTrue, increment, toggleTruth } = store;

  return {
    count, isTrue, increment, toggleTruth
  }
}

/* 
  <div>Count: {{count}}</div>
  <div class="icon btn" @click="increment">add</div>
  <div>
    <button @click="toggleTruth">Truth: {{isTrue}}</button>
  </div>
*/

```

<br>

### Pattern Three
``` js
/* Getters instead of state */

import { reactive, computed } from "vue";

/* state */
const state = reactive({
  count: 5,
  truth: false,
  list: [
    { id: 1, name: "One" },
    { id: 2, name: "Two" },
    { id: 3, name: "Three" },
  ]
});

/* getters */
const count = computed(() => state.count)
const truth = computed(() => state.truth)
const list = computed(() => state.list)

/* mutaions */
const setCount = function (i) {
  state.count += i;
}
function toggleTruth() {
  state.truth = !state.truth
}
function addListItem(str) {
  state.list.push({
    id: Date.now().toString(16).slice(-6),
    name: str
  })
}
function removeListItem(item) {
  state.list = state.list.filter(d => d.id !== item.id)
}

export default { 
  count, truth, list, setCount, toggleTruth, addListItem, removeListItem 
};
```
``` js
import store from '../store.js'

setup () {      
  const { count, truth, list, setCount, toggleTruth, addListItem, removeListItem } = store;

  return {
    count, truth, list, setCount, toggleTruth, addListItem, removeListItem
  }
}

/* 

*/

```

<br>

### Pattern Four
``` js
/* Getters instead of state */

import { reactive, computed } from "vue";

/* state */
const state = reactive({
  count: 5,
  truth: false,
  list: [
    { id: 1, name: "One" },
    { id: 2, name: "Two" },
    { id: 3, name: "Three" },
  ]
});

/* getters */
const count = computed(() => state.count)
const truth = computed(() => state.truth)
const list = computed(() => state.list)

/* mutaions */
const setCount = function (i) {
  state.count += i;
}
function toggleTruth() {
  state.truth = !state.truth
}
function addListItem(str) {
  state.list.push({
    id: Date.now().toString(16).slice(-6),
    name: str
  })
}
function removeListItem(item) {
  state.list = state.list.filter(d => d.id !== item.id)
}

export default { 
  count, truth, list, setCount, toggleTruth, addListItem, removeListItem 
};
```
``` js
import store from '../store.js'

setup () {      
  const { count, truth, list, setCount, toggleTruth, addListItem, removeListItem } = store;

  return {
    count, truth, list, setCount, toggleTruth, addListItem, removeListItem
  }
}

/* 

*/

```
