## Tooltips

``` html
/* tip on top */
<div tooltip> text
  <span tip> tooltip info </span>
</div>  

/* tip on right */
<div class="tooltip"> text
  <span tip="right"> tooltip info </span>
</div>  
```
    
- Add tooltip attribute... 
`<span tooltip>` 
or class 
`<span class="tooltip">`  
to the target element.
- Add a span with a tip attribute.
`<div tip>`
- Specify placement if needed
`<div tip="right">`
- The `textContent` of the `[tip]` is the tooltip text 


#### Adjustment object for common CSS properties:

``` css
:root {
  --fg: #fff;   // foreground 
  --bg: #555;   // background 
  --transition: 0.3s;
  --delay: 0.5s; 
  --cursor: help;
  --arrowX: 33%; 
  --borderColor: var(--bg);
}
```

#### scss
``` scss
// #region tootip ======== //
[tooltip], .tooltip {
  position: relative;
  display: inline-grid;
  border-bottom: 1px dotted var(--borderColor);
  cursor: var(--cursor);  
}

[tip] {
  position: absolute;
  top: -2rem;
  /* HORIZONTAL CENTERING for top and bottom tips*/
  /* comment out 'left: 0;' to center */
  /* uncomment out 'left: 0;' to justify left */
  left: 0; 
  justify-self: center;
  
  width: max-content;
  padding: 0 1rem;
  
  color: var(--fg);
  background: var(--bg);
  border-radius: 0.5rem;
  
  visibility: hidden;
  opacity: 0;
  z-index: 1;
  transition: opacity var(--transition);
  transition-delay: var(--delay);
  
  &::after {
    content: "";
    position: absolute;
    top: 100%;
    left: var(--arrowX);
    
    border-width: 0.5rem;
    border-style: solid;
    border-color: var(--bg) transparent transparent transparent;
    z-index: 20;
  }
}

[tooltip]:hover [tip],
.tooltip:hover [tip] {  
  visibility: visible;
  opacity: 1;
}

[tip="bottom"] {
  top: 2.5rem;
  
  &::after {
    top: -1rem;
    left: var(--arrowX);
    
    border-color: transparent transparent var(--bg) transparent;
    z-index: 10;
  }
}

[tip="right"] {
  top: 0.2rem;
  left: calc(100% + 1rem);
  display: inline-grid;
  
  &::after {
    top: calc(50% - 0.5rem);
    left: -1rem;
    border-color: transparent var(--bg) transparent transparent;
    z-index: 10;
  }
}

[tip="left"] {
  top: 0.2rem;
  left: calc(-200% + 1rem);
  
  &::after {
    top: calc(50% - 0.5rem);
    left: 100%;
    border-color: transparent transparent transparent var(--bg);
    z-index: 10;
  }
}
// #endregion tootip ======== //
```

#### or css
``` css
[tooltip], .tooltip {
  position: relative;
  display: inline-grid;
  border-bottom: 1px dotted var(--borderColor);
  cursor: var(--cursor);
}

[tip] {
  position: absolute;
  top: -2rem;
  /* HORIZONTAL CENTERING for top and bottom tips*/
  /* comment out 'left: 0;' to center */
  /* uncomment out 'left: 0;' to justify left */
  left: 0;
  justify-self: center;
  width: max-content;
  padding: 0 1rem;
  color: var(--fg);
  background: var(--bg);
  border-radius: 0.5rem;
  visibility: hidden;
  opacity: 0;
  z-index: 1;
  transition: opacity var(--transition);
  transition-delay: var(--delay);
}
[tip]::after {
  content: "";
  position: absolute;
  top: 100%;
  left: var(--arrowX);
  border-width: 0.5rem;
  border-style: solid;
  border-color: var(--bg) transparent transparent transparent;
  z-index: 20;
}

[tooltip]:hover [tip],
.tooltip:hover [tip] {
  visibility: visible;
  opacity: 1;
}

[tip=bottom] {
  top: 2.5rem;
}
[tip=bottom]::after {
  top: -1rem;
  left: var(--arrowX);
  border-color: transparent transparent var(--bg) transparent;
  z-index: 10;
}

[tip=right] {
  top: 0.2rem;
  left: calc(100% + 1rem);
  display: inline-grid;
}
[tip=right]::after {
  top: calc(50% - 0.5rem);
  left: -1rem;
  border-color: transparent var(--bg) transparent transparent;
  z-index: 10;
}

[tip=left] {
  top: 0.2rem;
  left: calc(-200% + 1rem);
}
[tip=left]::after {
  top: calc(50% - 0.5rem);
  left: 100%;
  border-color: transparent transparent transparent var(--bg);
  z-index: 10;
}
```
