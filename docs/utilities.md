## Utilities

#### loops.ts
```ts
  qty: number = 50;
  fillerList = Array.from({length: qty}, (_, i) => 
      `List Item ${i + 1}`);

  fillerItems = Array.from({length: qty}, () =>
      `Lorem ipsum dolor sit amet`);
```

#### widthFlag.ts
```ts
import { Component, HostListener } from '@angular/core';

... 

export class AppComponent implements OnInit {
  innerWidth: any;
  
  constructor() {}

  ngOnInit() {
    this.innerWidth = window.innerWidth;
    this.checkWidth();
  }

  @HostListener('window:resize', ['$event']) onResize(event) {
    this.innerWidth = window.innerWidth;
    this.checkWidth();
  }

  checkWidth() {
    if (this.innerWidth > 767) {
      this.offCanvas = true;
    } else {
      this.offCanvas = false;
    }
  }
}
```

#### randomHex
```ts  
  randomHex(x = 6) {
    let str = '';
    for (let i = 0; i < x; ++i) {
      str += Math.round(Math.random()*15).toString(16);
    }   
    return str;  
  }

  // id = randomHex(8);
  // returns an 8 digit hex string
```
