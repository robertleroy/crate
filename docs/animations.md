## animations

#### Router Animations
Note that routed components need to be positioned absolute, and the parent needs to be relative.


 #### app.component.html
```html
  <nav class='navigation'
      *ngIf="offCanvas" [@offCanvasSlide]> 
    <div (click)='innerWidth < 768 ? offCanvas = false : offCanvas = true'>
      <i class="close material-icons">close</i>
      <a routerLink="/home" routerLinkActive="active">Home</a>
      <a routerLink="/about" routerLinkActive="about">Home</a>
    </div>
  </nav>

  <section class='router' [@routerFade]="o.isActivated ? o.activatedRoute : ''">
    <router-outlet #o="outlet"></router-outlet>
  </section>
```
 
 
#### app.component.ts
```ts
import { Component, OnInit, HostListener } from '@angular/core';
import { Router } from '@angular/router';
import { offCanvasSlide, fade, routerFade } from './_animations/animations';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.scss' ],
  animations: [
    offCanvasSlide, fade, routerFade
  ] 
})
export class AppComponent implements OnInit {
  currentRoute: any;
  offCanvas: boolean = false;
  innerWidth: any;

  constructor(private router: Router) {}

  ngOnInit() {
    this.currentRoute = this.router;
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

#### animations.ts
```ts
import { trigger, transition, style, state, animate, query } from '@angular/animations';

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
    animate('0.1s', style({ opacity: 0 })),
    animate('0.2s ease-in')
  ])
]);

export const rotate = trigger('rotate', [
  state('up', style({
    transform: 'rotateX(-180deg)'
  })),

  transition('up => down', [
    animate('0.2s ease-out', style({
      transform: 'rotateX(0deg)'
    })),
  ]),

  transition('down => up', [
    animate('0.2s ease-in')
  ])
]);

export const fade = trigger('fade', [
  state('void', style({
    opacity: 0
  })),
  transition('void <=> *', animate('0.3s')),
]);

export const offCanvasLeft = trigger('offCanvasLeft', [
  transition(':enter', [
    style({transform: 'translateX(-100%)'}),
    animate('200ms ease-in', style({transform: 'translateX(0%)'}))
  ]),
  transition(':leave', [
    animate('200ms ease-in', style({transform: 'translateX(-100%)'}))
  ])
]);

export const offCanvasRight = trigger('offCanvasRight', [
  transition(':enter', [
    style({transform: 'translateX(100%)'}),
    animate('200ms ease-in', style({transform: 'translateX(0%)'}))
  ]),
  transition(':leave', [
    animate('200ms ease-in', style({transform: 'translateX(100%)'}))
  ])
]);

export const routerFade = trigger('routerFade', [
  transition('* => *', [
    query(
      ':enter',
      [style({ opacity: 0 })],
      { optional: true }
    ),
    query(
      ':leave',
      [style({ opacity: 1 }), animate('0.3s', style({ opacity: 0 }))],
      { optional: true }
    ),
    query(
      ':enter',
      [style({ opacity: 0 }), animate('0.3s', style({ opacity: 1 }))],
      { optional: true }
    )
  ])
]);
```
