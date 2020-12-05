#### Filters
> /* Adapted for Vue 3 */

``` js
import dateFormat from './dateFormat.js'

export default {
  install: (app, options) => {
    app.config.globalProperties.$filters = {
      date(value="", filter="") {
        if (!value) return '';
        return dateFormat(value, filter);
      },
      titlecase(value) {
        if (!value) return ''
        value = value.toString().toLowerCase()  ;
        return value.replace(/(^|\s)\S/g, function(t) { return t.toUpperCase() });
      },
      sentencecase(value) {
        if (!value) return ''
        value = value.toString()  ;
         return value.toLowerCase().replace(/(^\s*\w|[.!?]\s*\w)/g,function(c){return c.toUpperCase()});
      },
      prefix(value, str) {
        if (!value) return '';
        value = value.toString(); 
        return str.concat(value);
      },
      suffix(value, str) {
        if (!value) return '';
        value = value.toString(); 
        return value.concat(str);
      },
      number(value, d=0) {
        if (!value) return '';
        value = value * 1;
        value = value.toLocaleString('en', {maximumFractionDigits:d, useGrouping:false})*1  
       return value;
      },
      decimal(value, d=0) {
        if (!value) return '';
         value = value * 1;
        return value.toFixed(d);
      }
    }

    app.provide('filters', options)
  }
}
```
