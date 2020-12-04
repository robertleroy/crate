## Dropdown.vue
>  *Vue 3*

``` vue
<script>
  export default {
    name: 'Dropdown',
    props: {
      options: Array,
      placeholder: String
    },
    data: function () {
      return {
        showMenu: false,
        selectedOption: {},
      }
    },
    methods: {
      optionClick(option) {
        this.selectedOption = option;
        this.$emit('selected', option);
        this.showMenu = false;
      },
      setDefaults() {
        if (!this.options) {
          this.selectedOption = {
            value: undefined, name: "no options..."
            }
        } else if (this.placeholder) {
          this.selectedOption = {
            value: undefined, name: this.placeholder
          }
        } else {
          this.selectedOption = this.options[0];
        }
      }
    },
    mounted: function() {
      this.setDefaults();
    }
  };
</script>

<template>
  <section class='dropdown'
        @focusout="showMenu=false"
        tabindex="-1">
    <div class="button" 
          @click="showMenu = !showMenu">
      
      <div class="title">{{selectedOption.name}}</div>

      <div class="arrow"></div>
    </div>

    <div class="menu" v-if="showMenu">
      <div class="option"
            v-for="(option, index) of options"
            :key="index" :value="option.value"
            @click="optionClick(option)">
        {{option.name}}
      </div>
    </div>  
  </section>
</template>

<style scoped lang='scss'>
  @import '../scss/imports';

  .dropdown {
    position: relative;  
    display: inline-block !important;  
    min-width: 12rem;
    outline: none;

    .button {
      display: grid;
      grid-auto-flow: column;
      justify-content: space-between;
      align-items: center;
      grid-gap: 0.5rem;
      
      box-shadow: 0 1px 0 rgba(0,0,0,0.4);     
      padding: 0.25em 0; 
      padding-left: 0.375em;   

      cursor: pointer;

      &:hover {
        color: adjust-color($fontColor, $alpha: -0.3);
      }

      .arrow {
        height: 2rem;
        width: 2rem;
        background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24'%3E %3Cpath d='M7 10l5 5 5-5z' fill='rgba(0,0,0,0.8)'/%3E %3Cpath d='M0 0h24v24H0z' fill='none'/%3E %3C/svg%3E");
        background-repeat: no-repeat;
        background-size: cover;
      }    
    }

  .menu {
    position: absolute;
    left: 0;
    right: 0;
    z-index: 100;
    border-radius: 0.25rem; 
    box-shadow: 0 0 1px 1px rgba(0,0,0,0.3);
    padding: 0;
    background: $backgroundColor;
      
      .option {
        font-size: var(--h7);
        padding: 0.5rem 1rem;
        cursor: pointer;
        &:hover {        
          color: adjust-color($fontColor, $alpha: -0.3);
          background: rgba(0,0,0,0.05);
        }        
      }
    }
  }

</style>

<!--
import Dropdown from './components/Dropdown'

components: {
  'Dropdown': Dropdown'
}

items: [
  { title: 'Item One', value: 1 },
  { title: 'Item Two', value: 2 },
  { title: 'Item Three', value: 3 }
],
selectedItem: {},

methods: {
  updateSelected(obj) {
    this.selectedObject = obj;
    console.log(this.selectedItem.title);
  }
}

<Dropdown 
        :options="items"
        placeholder="choose something!"
        @selected="selectItem"/>
-->
