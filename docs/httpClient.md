## httpClient
  
#### httpService.ts
```ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable()
export class HttpService {
  constructor(private http: HttpClient) { }

  dataUrl = 'assets/data.json';

  getData() {
    return this.http.get(this.dataUrl);
  }

}
```

#### app.component.ts
```ts
import { Component, OnInit } from '@angular/core';
import { HttpService } from './_services/http.service';

export class AppComponent implements OnInit {
  title = 'code bin';  
  
  constructor(private httpService: HttpService) { }

  ngOnInit() {
    this.showConfig();
  }

  getData() {
    this.httpService.getData()
      .subscribe(
        data => {
        console.log(data);
      }, error => {
        console.log(error);
    });
  }

}
```

#### app.module.ts
```ts
import { NgModule }         from '@angular/core';
import { BrowserModule }    from '@angular/platform-browser';
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  imports: [
    BrowserModule,
    HttpClientModule,
  ],
  declarations: [
    AppComponent,
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```
 
 
