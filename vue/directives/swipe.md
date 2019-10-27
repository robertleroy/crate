## `v-swipe`

Vue directive that detects swipe gestures and returns an object.

#### `use`
``` html
<div v-swipe="swiped"></div>  
```

#### `callback function`
``` js 
swiped(e, gesture) {
	this.swipe = gesture;
	// console.log(gesture);
},
```

#### `gesture object`
``` js
gesture = {
	pointerType: "mouse",
	direction: "right",
	distance.x: 205,
	distance.y: -13,
	duration: 236
}
```

Use direction `arg` to restrict event.  
currently just `right` and `left`.

``` html
<div v-swipe:left="swipedLeft"></div> 
```  

Save to file and import / register
#### `app.js` 
``` js
import Vue from 'vue';
import { swipe } from "./directives/swipe"; 
	
const app = new Vue({ 
  el: '#app',
  directives: {
    swipe: swipe,
	},
	...
```

## CSS Tips

It helps to set 
```
user-select: none;
``` 
on the element that receives the swipe. Beware that this keeps users from selecting text while and interfering with the swipe, but it also keeps users from selecting text.

When swipeing on an object like an image the app may try to move the object with your swipe.  A conflict with the swipe and an aborted move.  Set  
```
touch-action: none
```
 to disable the windows default behavior.  

```
touch-action: pan-x;
```
 can also be useful allowing a horizontal gesture only.  

Currently the only directions supported are `right` and `left`, though extending to up and down should be a simple edit.

---  
---
---

#### `./directives/swipe`

``` js
export const swipe = ('swipe', {
  bind: function (el, binding, vNode) {
    let start={}, gesture={};  
    
    const gestureStart = function(e) {
      start = {
        pointerType: e.pointerType,
        timeStamp: new Date().getTime(),
        x: e.clientX,
        y: e.clientY,
      }   
      el.setPointerCapture(e.pointerId);
    }
    
    const gestureEnd = function(e) {
      gesture = {
        pointerType: e.pointerType,
        duration: new Date().getTime() - start.timeStamp,
        direction: e.clientX > start.x ? "right" : "left",
        distance: {
          x: Math.round(e.clientX - start.x),
          y: Math.round(e.clientY - start.y)         
        }
      }  
      // console.log(gesture);
      if ( gesture.duration < 500 && 
          Math.abs(gesture.distance.x) > 100 && 
          Math.abs(gesture.distance.y) < 100 )  {

        if (binding.arg === gesture.direction || !binding.arg) {
          binding.value(e, gesture);
        }
      }     
      el.releasePointerCapture(e.pointerId);
    }
    
    el.addEventListener('pointerdown', gestureStart); 
    el.addEventListener('pointerup', gestureEnd);
    el.addEventListener('pointercancel', gestureEnd);
  },
  unbind: function (el) {
    el.removeEventListener('pointerdown', gestureStart); 
    el.removeEventListener('pointerup', gestureEnd);
    el.removeEventListener('pointercancel', gestureEnd);
  }
});


```
