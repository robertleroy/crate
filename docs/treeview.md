## Treeview

#### animations.ts

```ts
import { trigger, transition, style, state, animate, query } from '@angular/animations';

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
    transform: 'rotate(-90deg)'
  })),

  transition('up => down', [
    animate('0.1s ease-out', style({
      transform: 'rotate(0deg)'
    })),
  ]),

  transition('down => up', [
    animate('0.1s ease-in')
  ])
]);
```


#### component.html

```html
<!-- #treeview Template Reference allows 
the recursive expandall function to work. -->

<h1>Treeview</h1>
<hr>

<div class="row">
  <div class="btn" (click)='treeview.toggleAll(true)'>expand all</div>
  <div class="btn" (click)='treeview.toggleAll(false)'>contract all</div>
</div>

<treeview #treeview [data]='list'></treeview>
```

#### treeview.html

```html
<!-- ==================== use ==================== -->
<!-- <treeview #treeview [data]='list'></treeview> -->
<!-- ==================== use ==================== -->

<!-- treeview works! -->

<div class="folder" *ngIf='data'>
  <div class="folderItem"  *ngFor="let item of data; let i = index">

    <div class="item" 
        (click)="item.expanded = !item.expanded"
        [class.parent]="item.children"> 
      <span>{{ item.name }}</span>

      <svg-icon  
        icon="chevron_down" 
        *ngIf="item.children" 
        [@rotate]="item.expanded ? 'down' : 'up'">
      </svg-icon>      
    </div>
    
    <div class="children"  *ngIf="item.children" [@collapse]="item.expanded ? 'expanded' : 'collapsed'" >
      <treeview 
        class="childFolder"
        *ngIf="item.expanded" 
        [data]='item.children'
        [@collapse]="item.expanded ? 'expanded' : 'collapsed'" >
      </treeview>      
    </div>
  
  </div>
</div>
```



#### treeview.scss

```scss
@import '../../../scss/imports';

:host {
  display: block;
}

.folderItem {
  // margin-top: 0.5rem;
}

.item {
  display: inline-grid;
  grid-auto-flow: column;
  align-items: center;
  grid-gap: 0 0.5rem;
  // padding: 0.125rem 0;
}

.childFolder { 
  margin-left: 1rem;
}

svg-icon {
  font-size: 1.5rem;
}

.parent {
  cursor: pointer;
}
```



#### treeview.ts
```ts
import { Component, OnInit, Input } from '@angular/core';
import { collapse, rotate } from '../../_animations/animations';

@Component({
  selector: 'treeview',
  templateUrl: './treeview.component.html',
  styleUrls: ['./treeview.component.scss'],
  animations: [ collapse, rotate ]
})
export class TreeviewComponent implements OnInit {
  @Input() data: any[];
  // expanded = {};

  constructor() { }

  ngOnInit() {
  }

  toggleAll(bool) {
    this.recursiveToggle(this.data, bool);
  }

  recursiveToggle(arr, bool) {
    arr.flatMap( item => {
      if (item.children) {
        // console.log(item.name);
        item.expanded = bool;
        this.recursiveToggle(item.children, bool);
      }      
    })
  }

}
```
