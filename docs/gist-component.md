## Gist Component

### Install Postscribe
`npm install --save postscribe`




## Usage
#### app.ts
```ts 
gistUrl = <Embed Code> || <Embed Code> + '?file=' + <file name> 
```

#### app.html
```html 
<my-gist [src]="gistUrl"></my-gist> 
```



## Gist Component

#### gist.component.ts
```ts
import { Component, OnChanges, Input, ViewChild } from '@angular/core';
import postscribe from 'postscribe';

@Component({
  selector: 'my-gist',
  templateUrl: './gist.component.html',
  styleUrls: ['./gist.component.scss']
})
export class GistComponent implements OnChanges {
  @Input() src;
  @ViewChild('gist') gist;

  constructor() { }

  ngOnChanges() {
    if (this.src) {
      postscribe(this.gist.nativeElement, `<script src="${this.src}"></script>`);
    }
  }
}
```

#### gist.component.html
```html
// template
<div #gist></div>
```

#### gist.component.scss
```scss
// styles
:host { 
  display: inline-block; 
}
```
