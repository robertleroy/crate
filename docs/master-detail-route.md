## master-detail-route

#### app.module.ts
```ts
@NgModule({
  imports: [
    BrowserModule,
    ReactiveFormsModule,
    RouterModule.forRoot([
      { path: '', component: ProductListComponent },
      { path: 'products/:productId', component: ProductDetailsComponent },
    ])
  ],
  ```


  #### product-list.html
  ```html
  <div *ngFor="let product of products; index as productId">

    <h3>
      <a [title]="product.name + ' details'" [routerLink]="['/products', productId]">
        {{ product.name }}
      </a>
    </h3>
  <!-- . . . -->
  </div>
  ```


  #### product-details.ts
  ```ts
  import { Component, OnInit } from '@angular/core';
  import { ActivatedRoute } from '@angular/router';

  import { products } from '../products';

  export class ProductDetailsComponent implements OnInit {
    product;

    constructor(
      private route: ActivatedRoute,
    ) { }

    ngOnInit() {
      this.route.paramMap.subscribe(params => {
        this.product = products[+params.get('productId')];
      });
    }

  }
  ```


  #### product-details.html
  ```html
  <h2>Product Details</h2>

  <div *ngIf="product">
    <h3>{{ product.name }}</h3>
    <h4>{{ product.price | currency }}</h4>
    <p>{{ product.description }}</p>

  </div>
  ```
