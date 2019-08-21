```js

// Upper Case //
Vue.filter('uppercase', function (value) {
  if (!value) return '';
  value = value.toString();
  return value.toUpperCase();
})

// Lower Case //
Vue.filter('lowercase', function (value) {
  if (!value) return '';
  value = value.toString();
  return value.toLowerCase();
})

// Capitalize first letter only //
Vue.filter('capitalize', function (value) {
  if (!value) return '';
  value = value.toString();
  return value.charAt(0).toUpperCase() + value.slice(1);
})

// Capitalize first letter each sentence //
Vue.filter('sentencecase', function (value) {
  if (!value) return '';
  value = value.toString()  ;
   return value.toLowerCase().replace(/(^\s*\w|[\.\!\?]\s*\w)/g,function(c){return c.toUpperCase()});
})

Vue.filter('titlecase', function (value) {
  if (!value) return '';
  value = value.toString()  ;
   return value.replace(/(^|\s)\S/g, function(t) { return t.toUpperCase() });
})

Vue.filter('suffix', function (value, str) {
  if (!value) return '';
  value = value.toString(); 
  return value.concat(str);
})
  
Vue.filter('tip', function (value, num) {
  if (!value) return '' ;
  value = value*1;
  let percent = value*(num*0.01); 

  return `$${(value + percent).toFixed(2)}`;
})

Vue.filter('dollar', function (value) {
  if (!value) return '' ;
  return `$${value.toFixed(2)}`;
});

Vue.filter('truncate', function (value, length) {
  if (!value) return '' ;
  return value.substring(0, length) + "...";
});


Vue.filter('decimal', function (value, d=2) {
  if (!value) return '' ;
  value = value * 1;
  return value.toFixed(d);
});

Vue.filter('number', function (value, d=0) {
  if (!value) return '' ;
  value = (value * 1).toFixed(d)*1;
  return value.toLocaleString();
});
```
