## BehaviorSubject

#### app.ts
```ts
import { Component, OnInit } from '@angular/core';
import { DataService } from './_services/data.service';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.scss' ]
})
export class AppComponent implements OnInit {
  data: any; 
  
  constructor(private dataService: DataService) { }

  ngOnInit() {
    this.dataService.dataSource.subscribe( res => {
      this.data = res;
    });
  }

  updateData() {
    this.dataService.updateData(this.data);
  }
}
```


#### data.service.ts
```ts
import { Injectable } from '@angular/core';
import { BehaviorSubject } from 'rxjs';

import { Data } from '../entities/data';

@Injectable()
export class DataService {

  private dataSource = new BehaviorSubject({});

  constructor() { }

  updateData(data){
    this.dataSource.next(data);
  }
  
}
```
