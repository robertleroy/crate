## Tabs

#### tabs.ts
```ts
  ...
  import { fade } from './animations';

  @Component({ 
    ...,
    animations: [fade]
  })
  export class SomeComponent {
    activeTab = 'tab1';
    
    constructor() { }

    ...

  }
```

#### tabs.html
```html
  <section class='tabContainer'>
    <div class="tabs">
      <div class="tab" (click)="activeTab = 'tab1'" 
          [ngClass]="{'active': activeTab=='tab1'}">Tab 1</div> 
      <div class="tab" (click)="activeTab = 'tab2'" 
          [class.active]="activeTab=='tab2'">Tab 2</div>
      <div class="tab" (click)="activeTab = 'tab3'" 
          [class.active]="activeTab=='tab3'">Tab 3</div>
    </div>
    <div class="panels" [ngSwitch]='activeTab'>
      <div *ngSwitchCase="'tab1'" [@fade]>Panel 1</div>
      <div *ngSwitchCase="'tab2'" [@fade]>Panel 2</div>
      <div *ngSwitchCase="'tab3'" [@fade]>Panel 3</div>
    </div>
  </section>
```

#### tabs.scss
```scss
  .tabs {
    display: grid;
    grid-auto-flow: column; 
    justify-content: flex-start;
    grid-gap: 1rem;
    
    .tab {    
      transition: all 0.3s;
      cursor: pointer;
    }
    
    .active {
      color: Coral;
    }
  }
```

#### animations.ts
```ts
  import { trigger, transition, style, state, animate, query } from '@angular/animations';

  export const fade = trigger('fade', [
    state('void', style({
      opacity: 0
    })),
    transition('void <=> *', animate('0.3s')), 
  ]);
```
