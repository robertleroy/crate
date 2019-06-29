## Pipes

#### pipes.ts
```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'suffix'
})
export class SuffixPipe implements PipeTransform {
  transform(value: any, str: string): any {
    return value + str;
  }
}

@Pipe({
  name: 'degree'
})
export class DegreePipe implements PipeTransform {
  transform(value: any): any {
    return value + '°';
  }
}
```

## Date Pipe
```
| Alias        | Example                                           |
| ------------ | ------------------------------------------------: |
| 'short'      | 'M/d/yy, h:mm a' (6/15/15, 9:03 AM).              |
| 'medium'     | 'MMM d, y, h:mm:ss a' 
                  (Jun 15, 2015, 9:03:01 AM).                      |
| 'long'       | 'MMMM d, y, h:mm:ss a z' 
                  (June 15, 2015 at 9:03:01 AM GMT+1).             |
| 'full'       | 'EEEE, MMMM d, y, h:mm:ss a zzzz' 
                  (Monday, June 15, 2015 at 9:03:01 AM GMT+01:00). |
| 'shortDate'  | 'M/d/yy' (6/15/15).                               |
| 'mediumDate' | 'MMM d, y' (Jun 15, 2015).                        |
| 'longDate'   | 'MMMM d, y' (June 15, 2015).                      |
| 'fullDate'   | 'EEEE, MMMM d, y' (Monday, June 15, 2015).        |
| 'shortTime'  | 'h:mm a' (9:03 AM).                               |
| 'mediumTime' | 'h:mm:ss a' (9:03:01 AM).                         |
| 'longTime'   | 'h:mm:ss a z' (9:03:01 AM GMT+1).                 |
| 'fullTime'   | 'h:mm:ss a zzzz' (9:03:01 AM GMT+01:00).          |
```

## Currency Pipe

#### app.html
```html
<div>
    <!-- a: number = 0.259; -->
    <!-- b: number = 1.3495; -->
    
    <!--output '$0.26'-->
    <p>A: {{a | currency}}</p>
 
    <!--output 'CA$0.26'-->
    <p>A: {{a | currency:'CAD'}}</p>
 
    <!--output 'CAD0.26'-->
    <p>A: {{a | currency:'CAD':'code'}}</p>
 
    <!--output 'CA$0,001.35'-->
    <p>B: {{b | currency:'CAD':'symbol':'4.2-2'}}</p>
 
    <!--output '$0,001.35'-->
    <p>B: {{b | currency:'CAD':'symbol-narrow':'4.2-2'}}</p>
 
    <!--output '0 001,35 CA$'-->
    <p>B: {{b | currency:'CAD':'symbol':'4.2-2':'fr'}}</p>
 
    <!--output 'CLP1' because CLP has no cents-->
    <p>B: {{b | currency:'CLP'}}</p>

    <!-- output 'NZ$1.35' -->
    <p>B: {{b | currency: 'NZD'}}</p>

    <!-- output '€1.35' -->
    <p>B: {{b | currency: 'EUR'}}</p>
  </div>
  ```
