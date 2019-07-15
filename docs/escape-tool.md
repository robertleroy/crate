## escape-tool element

*Use to make your own code escape tool.*

###### escape.html
```html
<p>
escape code!
</p>

<textarea class="textIn" 
    placeholder="escape( )"
    (input)="escape()"
    [(ngModel)]="textIn"></textarea>

<div class="output">
  <p *ngIf="textIn">output</p>

  <pre class="textOut" *ngIf="textIn">{{textOut}}</pre>
</div>
```

###### escape.scss
```scss
@import '../../../scss/imports';

:host {
  display: block;
  padding: 1rem 2rem;
  background: #eee;
  min-height: 250px;
  
}

.textIn, .textOut {
  background: #fff;
  font-family: $monospace, $monospace;
  padding: 2rem;
  border-radius: 0.53rem;
  tab-size: 8;

  @include shadow(2);
  transition: all 0.2s ease-out;

  &:hover {
    @include shadow(4);  
  }
}

.textIn {
  min-height: 150px;
  width: 100%;
  border-radius: 0.3rem;  

  overflow-y: auto;
}

.output {
  margin-top: 2rem;
  .textOut {
    white-space: pre-wrap;
  }
}
```

###### escape.ts
```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'escape-tool',
  templateUrl: './escape-tool.component.html',
  styleUrls: ['./escape-tool.component.scss']
})

export class EscapeToolComponent implements OnInit {
  textIn;
  textOut;

  constructor() { }

  ngOnInit() {
  }

  escape() {
    this.textOut = this.replaceAll(this.textIn);
  }

  replaceAll(str) {
    var replaceChars={ 
      "{":"&#123;",
      "}":"&#125;",
      "<":"&lt;",
      ">":"&gt;",
      "\"":"&quot;",
      "&":"&amp;",
    };

    return str.replace(/{|}|<|>|"|&/g,function(match) {return replaceChars[match];})  
  }   

}

```

###### use
```html
<!-- component.html -->

<-tool class="escapeTool" *ngIf='toggleEscape' [@slideDown]></-tool>
```
