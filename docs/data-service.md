## Data Service

#### data.service.ts 
```ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable, BehaviorSubject } from 'rxjs';

@Injectable({
  providedIn: 'root',
})
export class DataService {
  dataStore = new BehaviorSubject([]);
  dataList = this.dataStore.asObservable();
  url = '../../assets/data.json';

  constructor(private http: HttpClient) { this.getData(); } 

  getData() {
    this.http.get(this.url).subscribe((data: any[]) => {
      // console.log(data);
      this.dataStore.next(data);
    }, error => console.log('Could not load todos.'));
  }

  updateData(data){
    this.dataStore.next(data);
  }

}
```

#### app.ts
```ts
import { Component, OnInit } from '@angular/core';
import { DataService } from '../_services/data.service';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.scss']
})
export class HomeComponent implements OnInit {
  data: any;

  constructor(private dataService: DataService) { }

  ngOnInit() {
    this.dataService.dataList.subscribe(res => {
      this.data = res;
    });
  }

  updateItem() {
    // console.log(this.todos);
    this.dataService.updateData(this.data);
  }

}
```
