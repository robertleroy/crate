## Checkbox

#### Use
``` html
<checkbox v-model="item.completed"></checkbox>
```

#### app.js
``` js
Vue.component('checkbox', {
template: `
    <label class="checkbox btn">
      <div class="icon-outlined">
        {{checked ? 'check' : 'check_box_outline_blank'}}
      </div>
      <input ref="check" type="checkbox" 
          v-bind:checked="checked"
          v-on:change="$emit('change', $event.target.checked)">
    </label>
  `,
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    checked: Boolean
  }
})
```

#### style.scss
``` scss
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
```

