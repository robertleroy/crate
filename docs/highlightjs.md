## Highlight.js

#### Installation
```
npm install highlight.js 
npm install @types/highlight.js
```

#### highlight.ditective.ts

```ts 
import { Directive, ElementRef, AfterViewInit } from '@angular/core';
import * as hljs from 'highlight.js';

@Directive({
  selector: '[highlight]'
})
export class HighlightDirective implements AfterViewInit {

  constructor(private elRef: ElementRef) { }

  ngAfterViewInit() {
    hljs.configure({ useBR: false }); // change /n to <br/> | non-pre 
    hljs.highlightBlock(this.elRef.nativeElement);
  }

}
```

#### component.html 
```html
<!-- use -->
<!-- ESCAPE CODE -->

<pre highlight class='codeblock ts'><code>
@Component(&#123;
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.scss']
&#125;)
</code>
</pre>

<pre><code highlight class="html">
    &lt;html&gt;
      &lt;body&gt;

      &lt;h1&gt;My First Heading&lt;/h1&gt;
      &lt;p&gt;My first paragraph.&lt;/p&gt;

      &lt;/body&gt;
    &lt;/html&gt;
  </code>
</pre>

<pre><code highlight class="typescript">
  @import "~prismjs/plugins/toolbar/prism-toolbar.css";
  @import "~prismjs/themes/prism-okaidia";
</code>
</pre>
```


#### component.scss
```scss
// #region Styles ==================== //
// *** Import one into app/styles.scss *** //

// @import '~highlight.js/styles/agate.css';
// @import '~highlight.js/styles/github.css';
// @import '~highlight.js/styles/github-gist.css';
// @import '~highlight.js/styles/color-brewer.css';
// @import '~highlight.js/styles/vs2015.css';
// @import '~highlight.js/styles/solarized-dark.css';
// @import '~highlight.js/styles/docco.css';
// @import '~highlight.js/styles/vs.css';
// @import '~highlight.js/styles/arduino-light.css';
// @import '~highlight.js/styles/tomorrow.css';
// @import '~highlight.js/styles/tomorrow-night.css';
// @import '~highlight.js/styles/atom-one-light.css';
// @import '~highlight.js/styles/atom-one-dark.css';

// #endregion Styles ================= //
```

