#### Checkbox.md
> *Vue 3*

``` vue
<!-- Vue-3 Checkbox -->

<script>
  export default {
    name: 'Checkbox',
    props: ['modelValue'],
    emits: ['update:modelValue']    
  };
</script>

<template>
  <label class="checkbox btn">
    <div class="icon-outlined">
      {{modelValue ? 'check' : 'check_box_outline_blank'}}
      <!-- {{checked ? 'check_box_outline' : 'check_box_outline_blank'}} -->
    </div>
    <input ref="check" 
        type="checkbox" 
        :checked="modelValue"
        @change="$emit('update:modelValue', $event.target.checked)">   
  </label>    
</template>

<style scoped lang='scss'>
  @import '../scss/imports';

  .checkbox {
    position: relative;
    display: inline-block;
    cursor: pointer;
    line-height: 1;
    user-select: none;
    vertical-align: middle;
    color: var(--muted-8);

    &:hover {
      opacity: 0.6;
    }
    &:active {
      opacity: 0.3;    
    }

    input {
      position: absolute;
      z-index: -1;
      opacity: 0;
      height: 0;
      width: 0;   
    }
  }
</style>

<!-- 
import Checkbox from "./components/Checkbox";
components: {"Checkbox", Checkbox},

<Checkbox v-model="item.completed" />
-->
```
