## code-block

Code-block transcludes `pre` and `code` elements into a single component.
- Highlighting is automatic
  - use the `lang` attribute to get it right  ~  `lang='html'`. 
- `title` attribute assigns a header/title
- if you need to escape double curly braces add a `ngNonBindable` attribute
    - keeps angular from *binding* or *interpolating* them

```html
<codeblock lang="ts" title="component.ts" ngNonBindable>
  ...
</codeblock>
```

### preserveWhitespaces: true
Prepare the app to allow `code-block` to mimic `pre` tag.  
- Add `preserveWhitespaces: true` to `main.ts` bootstrap call.
- Add `preserveWhitespaces: true` to `code-block.ts` @component decorator.
###### main.ts ~ *available to app*
```ts
platformBrowserDynamic().bootstrapModule(AppModule, {
  
  preserveWhitespaces: true

}).then(ref => {
  
 ...
 
}).catch(err => console.error(err));
```
###### component.ts ~ *available to component*
```ts
@Component({
  selector: 'codeblock',
  templateUrl: './code-block.component.html',
  styleUrls: ['./code-block.component.scss'], 
  
  preserveWhitespaces: true

})
```

#### code-block.ts
```ts
import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'codeblock',
  templateUrl: './code-block.component.html',
  styleUrls: ['./code-block.component.scss'], 
  preserveWhitespaces: true
})
export class CodeBlockComponent implements OnInit {

  @Input() title;
  @Input() lang;

  constructor() {}

  ngOnInit() {
    console.log(this.lang);
  }

}
```

#### code-block.html
###### *to preserveWhitespaces do not make extra line breaks here*
```html
<pre><div class="title" *ngIf="title">{{title}}</div><code highlight [class]="lang"><ng-content></ng-content></code></pre>
```


#### code-block.scss 
###### *builds off of my default `pre` styles*
```scss
@import '../../../scss/imports';

$buffer: 1rem;

:host {  
  position: relative;
  display: block;
  margin-bottom: 2rem;
  border-radius: 0.3rem;
  @include shadow(2);
}

pre {
  padding: 0 $buffer 2rem !important;
  margin-bottom: 0;
  overflow-x: auto;

  .title {
    position: relative;
    font-size: var(--h9);
    padding: 0.5rem 0;

    &:after {
      position: absolute;
      content: '';
      height: 2.5rem;
      left: -1rem;
      right: -1rem;
      border-bottom: 1px solid rgba(0,0,0,0.08);
    }
  } 
}
```

#### Use
Escape code before adding to element.  These characters need to be addressed:

`<`, `>`, `{`, `}`, `"`, `$`

###### *app.html*
```
<!-- app.html -->

<codeblock lang="html" title="codeblock component html" ngNonBindable>
&lt;header&gt;
  &lt;h2&gt;&#123;&#123;title&#125;&#125; &lt;sup&gt;&#123;&#123;version&#125;&#125;&lt;/sup&gt;&lt;/h2&gt;
&lt;/header&gt;
</codeblock>
```
