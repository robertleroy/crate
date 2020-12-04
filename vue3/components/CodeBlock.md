## Simple-Syntax-Highlighter

#### install
``` js
npm i simple-syntax-highlighter /* Vue 2.x. */
npm i simple-syntax-highlighter@next /* (@^2.0.0) Vue 3. */
```

#### component
``` vue
// script
import CodeBlock from 'simple-syntax-highlighter'
import 'simple-syntax-highlighter/dist/sshpre.css'

components: { 'CodeBlock': CodeBlock },

// template
<code-block language="html-vue">{{codeSample}}</code-block>

```

#### Options
* language=''
* label=''
* reactive
* dark
* copy-button

Supported Languages:  
  * XML
  * HTML
  * HTML Vue JS Template
  * Pug
  * Javascript
  * JSON
  * CSS
  * PHP
  * MySQL
