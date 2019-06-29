## accordion

#### accordion.html
```html
<!-- accordion works! -->

<div (click)="toggle = !toggle"
      [class.toggled]="toggle" 
      class="header">
  <ng-content select='header'></ng-content>
  <i class="material-icons"
  [@rotate]="toggle ? 'up' : 'down'">chevron_right</i>
</div>

<div class="section" [@collapse]="toggle ? 'expanded' : 'collapsed'">
<!-- <div *ngIf="toggle"
      class="section">  -->
  <ng-content select='section'></ng-content>
</div>
```

#### accordion.scss
```scss
@import '../../../scss/imports';

:host {
  display: inline-block;
  border: 1px solid #777;
}

.header {
  padding: 1rem;
  /* background: $backgroundColor; */
  cursor: pointer;
  z-index: 1;

  display: flex;
  justify-content: space-between;
}

.toggled {
  // border-bottom: 1px solid #777;
}

.section {
  padding: 12px 12px 24px;
  border-bottom: 1px solid #ccc;
  border-top: none;
  pointer-events: none;
}
```

#### accordion.ts
```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-accordion',
  templateUrl: './accordion.component.html',
  styleUrls: ['./accordion.component.scss']
})
export class AccordionComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

}
```

#### animations.ts
```ts
import { trigger, transition, style, state, animate } from '@angular/animations';

// collapse ======================== //
export const collapse = trigger('collapse', [
  state('collapsed', style({
    height: 0,
    paddingTop: 0,
    paddingBottom: 0,
    opacity: 0,
    lineHeight: 0
  })),

  transition('collapsed => expanded', [
    animate('0.1s ease-out', style({
      height: '*',
      paddingTop: '*',
      paddingBottom: '*',
      lineHeight: '*'
    })),
    animate('0.1s', style({ opacity: 1 }))
  ]),

  transition('expanded => collapsed', [
    // animate('0.1s', style({ opacity: 0 })),
    animate('0.2s ease-in')
  ])
]);


// rotate ======================== //
export const rotate = trigger('rotate', [
  state('up', style({
    transform: 'rotate(90deg)'
  })),

  transition('up => down', [
    animate('0.2s ease-out', style({
      transform: 'rotate(0deg)'
    })),
  ]),

  transition('down => up', [
    animate('0.2s ease-in')
  ])
]);


// fade ======================== //
export const fade = trigger('fade', [
  state('void', style({
    opacity: 0
  })),
  transition('void <=> *', animate('0.3s')),
]);
```

#### app.html
```html
<!-- use -->
<accordion>
  <header>
    Accordion Header
  </header>
	
  <section>
    Lorem ipsum dolor, sit amet consectetur adipisicing elit. 
    Voluptatibus dolor cumque itaque facilis, quisquam, atque, architecto
    necessitatibus delectus voluptas repellendus voluptatem totam quis iusto at obcaecati officia placeat illo tempora.
  </section>
</accordion>
```
