## [Simple-Syntax-Highlighter](https://antoniandre.github.io/simple-syntax-highlighter/)

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
  * xml
  * html
  * html-vue
  * pug
  * js
  * json
  * css
  * php
  * sql

#### Alternate CSS
``` css
/* App.vue */
.ssh-pre {
  /* line-height: 1.5; */
  position: relative;
  margin-top: 1em;
  padding: 0.5em;
  border: 1px solid rgba(0, 0, 0, 0.06);
  background-color: #f6f8fa;
  border-radius: 4px;
  display: block;
  &--dark {
    background-color: #262626;
    color: rgba(255, 255, 255, 0.85);
  }
  &__content {
    line-height: 1.3;
    white-space: pre-wrap;
    word-break: break-word;
  }
  &__copy {
    position: absolute;
    top: 3px;
    right: 3px;
  }
  #clipboard-textarea {
    position: absolute;
    z-index: -100;
    opacity: 0;
  }
  &[data-label] {margin-top: 2.5em;}
  &[data-label]:before {
    content: attr(data-label);
    position: absolute;
    bottom: 100%;
    right: 1em;
    padding: 0.1em 0.7em 0;
    background-color: inherit;
    border: 1px solid rgba(0, 0, 0, 0.06);
    border-bottom: 1px solid #f9f9f9;
    border-radius: 3px 3px 0 0;
    font-size: 11px;
  }
  &--dark[data-label]:before {border-bottom-color: #262626;}
}


.txt {color: #24292E;}
.comment {color: #888888;}
.quote {color: #032f62;;}
.number {color: #24292E;}
.boolean {color: #005cc5;}
.keyword {color: #005cc5;}
.this {color: #22863a;}
.punctuation {color: #24292E;}
.external-var, .special {color: #02027e;}
.variable {color: #032F62;}
.obj-attr {color: #22863a;}
.vendor {color: orangered;}

[data-type="shell"] .keyword {color: #6f42c1;}
[data-type="shell"] .param {color: #22863a;}

[data-type="html"] .doctype {color: #02027e;}
[data-type="html"] .tag-name {color: #22863a;}
[data-type="html"] .attribute {color: #005cc5;}

[data-type="html-vue"] .doctype {color: #02027e;}
[data-type="html-vue"] .tag-name {color: #22863a;}
[data-type="html-vue"] .punctuation {color: #24292E;}
[data-type="html-vue"] .attribute {color: #005cc5;}

[data-type="xml"] .doctype {color: #02027e;}
[data-type="xml"] .tag-name {color: #11c;}
[data-type="xml"] .attribute {color: #02027e;}

[data-type="css"] .selector {color: #22863a;}
[data-type="css"] .class-id {color: #005cc5;}
[data-type="css"] .pseudo {color: #22863a;}
[data-type="css"] .keyword {color: #d73a49;}
[data-type="css"] .vendor {color: #6f42c1;}
[data-type="css"] .attribute {color: #005cc5;}
[data-type="css"] .value {color: #24292E;}
[data-type="css"] .color {background: #eee;}
[data-type="css"] .unit {color: #24292e;}
[data-type="css"] .number {color: #005cc5;}
[data-type="css"] .important {color: #d73a49;}

[data-type="sql"] .var-type {color: #02027e;font-weight: bold;}
```
