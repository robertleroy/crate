#### Basic 2-way data binding
> *Vue 3*

``` vue
<!-- Vue-3 Textbox -->

<script>
  export default {
    name: 'Textbox',
    props: ['modelValue'],
    emits: ['update:modelValue'],
    methods: { },
  };
</script>

<template>
  <input type="text" 
    :value='modelValue' 
    @input="$emit('update:modelValue', $event.target.value)"> 
</template>

<style scoped lang='scss'>
  @import '../scss/imports';

  input {
    border: 1px solid gray;
  }
</style>

<!-- 
import Textbox from "./components/Textbox";
components: {"Textbox", Textbox},

<Textbox v-model="testText" />
-->
```
