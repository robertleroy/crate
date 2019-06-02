## Boilerplate

#### app.component.html
```html
<!-- app.component.html -->
<header>
  <h1>{{title}}</h1>
</header>

<section class='router' [@routerFade]="o.isActivated ? o.activatedRoute : ''">
  <router-outlet #o="outlet"></router-outlet>
</section>

<footer class='footer'>
  <a routerLink="/home" routerLinkActive="active">Home</a>
  <a routerLink="/about" routerLinkActive="active">About</a>
</footer>
```


#### app.component.scss
```scss
@import '../scss/imports';

:host {
  height: 100vh;
  display: grid;
  grid-template-rows: auto 1fr auto;
}

.router {
  overflow-y: auto;
}

.footer {
  display: grid;
  justify-content: space-around;
  grid-auto-flow: column;

  padding: 1rem 1rem 0.5rem;
  box-shadow: 0 -5px 5px rgba(0,0,0,0.05);
}

.active {
  color: $dodgerOrange;
}
 app.component.ts
import { Component, OnInit } from '@angular/core';
import { routerFade } from './_animations/animations';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.scss' ],
  animations: [routerFade]
})
export class AppComponent implements OnInit {
  title = 'starter';  
  
  constructor() { }

  ngOnInit() {
    
  }

}
```


#### app.module.ts
```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { HttpClientModule } from '@angular/common/http';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { FormsModule } from '@angular/forms';
import { AppRoutingModule, RoutedComponents } from './app.routing.module';

import { AppComponent } from './app.component';

@NgModule({
  imports: [ 
    BrowserModule,
    AppRoutingModule,
    HttpClientModule,
    BrowserAnimationsModule,
    FormsModule
  ],
  declarations: [
    AppComponent,
    RoutedComponents
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```


#### app.routing.module.ts
```ts
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';

const routes: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' },
  { path: 'home', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', component: HomeComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

export const RoutedComponents = [
  HomeComponent,
  AboutComponent
];
```

#### style.scss
```scss
/* Add application styles & imports to this file! */

@import url("https://fonts.googleapis.com/icon?family=Material+Icons");

@import './scss/baseline';
```


 
