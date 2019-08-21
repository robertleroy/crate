```js

// #region Text Casing ====================== //
Vue.filter('titlecase', function (value) {
  if (!value) return '';
  value = value.toString()  ;
   return value.replace(/(^|\s)\S/g, function(t) { return t.toUpperCase() });
});


Vue.filter('sentencecase', function (value) {
  if (!value) return '';
  value = value.toString()  ;
   return value.toLowerCase().replace(/(^\s*\w|[\.\!\?]\s*\w)/g,function(c){return c.toUpperCase()});
});


Vue.filter('uppercase', function (value) {
  if (!value) return '';
  value = value.toString();
  return value.toUpperCase();
});


Vue.filter('lowercase', function (value) {
  if (!value) return '';
  value = value.toString();
  return value.toLowerCase();
});


Vue.filter('capitalize', function (value) {
  if (!value) return '';
  value = value.toString();
  return value.charAt(0).toUpperCase() + value.slice(1);
});
// #endregion Text Casing ====================== //




// #region Text Manipulation ====================== //
Vue.filter('prefix', function (value, str) {
  if (!value) return '';
  value = value.toString(); 
  return str.concat(value);
});

Vue.filter('suffix', function (value, str) {
  if (!value) return '';
  value = value.toString(); 
  return value.concat(str);
});

Vue.filter('truncate', function (value, length) {
  if (!value) return '' ;
  return value.substring(0, length) + "...";
});
// #endregion Text Manipulation ====================== //




// #region Numbers ====================== //

// Sets Decimals //
Vue.filter('decimal', function (value, d=2) {
  if (!value) return '' ;
  value = value * 1;
  return value.toFixed(d);
});

// Sets Decimal && Locale Format (thousands seperators) //
Vue.filter('number', function (value, d=0) {
  if (!value) return '' ;
  value = (value * 1).toFixed(d)*1;
  return value.toLocaleString();
});


Vue.filter('tip', function (value, num) {
  if (!value) return '' ;
  value = value*1;
  let percent = value*(num*0.01); 

  return `$${(value + percent).toFixed(2)}`;
});


Vue.filter('dollar', function (value) {
  if (!value) return '' ;
  return `$${value.toFixed(2)}`;
});
// #endregion Numbers ====================== //

```
