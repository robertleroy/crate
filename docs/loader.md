```
<svg  class="loader" [@delayedFade] width="150" height="76px" viewBox="0 0 70 48" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1">
  <path id="text">
    <animate attributeName="d" from="m0,18 h0" to="m0,18 h150" dur="2s" begin="1s" repeatCount="indefinite"/>
  </path>
  <text font-size="16" font-family="arial" fill='currentColor'>
    <textPath xlink:href="#text">loading...</textPath>
  </text>
</svg>
```
  
// delayedFadefade ======================== //
// export const delayedFade = trigger('delayedFade', [
//   state('void', style({
//     opacity: 0
//   })),
//   transition('void => *', animate('0.3s 1s')),
// ]);
