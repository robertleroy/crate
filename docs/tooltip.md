## tooltip

#### tooltip.html
```html
<!--   =====  Useage   =====   -->
<!-- tooltip: tooltip content -->
<!-- position: optional => <top, bottom, left, right> - defaults to top  -->
<!-- delay:  optional => enter number of ms to delay toolti - defaults to 0 -->

<div tooltip="tooltip content" position="top" delay="300">Tooltip Directive</div>
```
 
#### tooltip.service.ts
```ts
import { Directive, Input, ElementRef, HostListener, Renderer2 } from '@angular/core';

@Directive({
  selector: '[tooltip]'
})
export class TooltipDirective {
  @Input('tooltip') content: string;
  @Input() position?: string = 'top';
  @Input() delay?: string = '0';
  tooltip: HTMLElement;
  offset = 10;

  constructor(
    private el: ElementRef,
    private renderer: Renderer2) { }

  @HostListener('mouseenter') onMouseEnter() {
    if (!this.tooltip) { this.show(); }
  }

  @HostListener('mouseleave') onMouseLeave() {
    if (this.tooltip) { this.hide(); }
  }

  show() {
    this.create();
    this.setPosition();
    this.renderer.addClass(this.tooltip, 'tooltip-show');
  }

  hide() {
    this.renderer.removeClass(this.tooltip, 'tooltip-show');
    window.setTimeout(() => {
      this.renderer.removeChild(document.body, this.tooltip);
      this.tooltip = null;
    }, 300);
  }

  create() {
    this.tooltip = this.renderer.createElement('span');
    this.renderer.appendChild(
      this.tooltip,
      this.renderer.createText(this.content) // textNode
    );

    this.renderer.appendChild(document.body, this.tooltip);
    this.renderer.addClass(this.tooltip, 'tooltip');
    this.renderer.addClass(this.tooltip, `tooltip-${this.position}`);

    // delay 
    this.renderer.setStyle(this.tooltip, '-webkit-transition-delay', ` ${this.delay}ms`);
    this.renderer.setStyle(this.tooltip, 'transition-delay', ` ${this.delay}ms`);
  }

  setPosition() {
    const hostRect = this.el.nativeElement.getBoundingClientRect();
    const tooltipRect = this.tooltip.getBoundingClientRect();

    // window scroll top
    const scrollPos = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0;

    let top, left;

    if (this.position === 'top') {
      top = hostRect.top - tooltipRect.height - this.offset;
      left = hostRect.left + (this.offset + hostRect.width - tooltipRect.width)*0.5;
    }

    if (this.position === 'bottom') {
      top = hostRect.bottom + this.offset;
      left = hostRect.left + (this.offset + hostRect.width - tooltipRect.width)*0.5;
    }

    if (this.position === 'left') {
      top = hostRect.top + (hostRect.height - tooltipRect.height)*0.5;
      left = hostRect.left - tooltipRect.width - (this.offset * 0.5);
    }

    if (this.position === 'right') {
      top = hostRect.top + (hostRect.height - tooltipRect.height)*0.5;
      left = hostRect.right + (this.offset * 2);
    }

    this.renderer.setStyle(this.tooltip, 'top', `${top + scrollPos}px`);
    this.renderer.setStyle(this.tooltip, 'left', `${left}px`);
  }

}
```
