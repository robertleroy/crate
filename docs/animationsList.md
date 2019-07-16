import { trigger, transition, style, state, animate, query } from '@angular/animations';

const duration = '0.2s';
const delay = '0s';
const ease = 'ease-in';
let timing = duration.concat(" ",delay," ",ease);


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
    animate('0.1s', style({ opacity: 0 })),
    animate('0.2s ease-in')
  ])
]);


// rotate ======================== //
export const rotate = trigger('rotate', [
  state('up', style({
    transform: 'rotate(90deg)'
  })),

  transition('up => down', [
    animate(timing, style({
      transform: 'rotate(0deg)'
    })),
  ]),

  transition('down => up', [
    animate(timing)
  ])
]);


// routerFade ======================== //
export const routerFade = trigger('routerFade', [
  transition('* => *', [
    query(
      ':enter',
      [style({ opacity: 0 })],
      { optional: true }
    ),
    query(
      ':leave',
      [style({ opacity: 1 }), animate(timing, style({ opacity: 0 }))],
      { optional: true }
    ),
    query(
      ':enter',
      [style({ opacity: 0 }), animate(timing, style({ opacity: 1 }))],
      { optional: true }
    )
  ])
]);


// offCanvasLeft ======================== //
export const offCanvasLeft = trigger('offCanvasLeft', [
  transition(':enter', [
    style({transform: 'translateX(-100%)'}),
    animate(timing, style({transform: 'translateX(0%)'}))
  ]),
  transition(':leave', [
    animate(timing, style({transform: 'translateX(-100%)'}))
  ])
]);


// offCanvasRight ======================== //
export const offCanvasRight = trigger('offCanvasRight', [
  transition(':enter', [
    style({transform: 'translateX(100%)'}),
    animate(timing, style({transform: 'translateX(0%)'}))
  ]),
  transition(':leave', [
    animate(timing, style({transform: 'translateX(100%)'}))
  ])
]);


// slideDown ======================== //
export const slideDown = trigger('slideDown', [
  transition(':enter', [
    style({transform: 'translateY(-100%)'}),
    animate(timing, style({transform: 'translateY(0%)'}))
  ]),
  transition(':leave', [
    animate(timing, style({transform: 'translateY(-100%)'}))
  ])
]);


// fade ======================== //
export const fade = trigger('fade', [
  state('void', style({
    opacity: 0
  })),
  transition('void <=> *', animate(timing)),
]);
