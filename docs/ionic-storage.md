## Ionic Storage

#### instalation
```
npm install --save @ionic/Storage
```

#### app.module.ts
```ts
import { IonicStorageModule } from '@ionic/storage';

@NgModule({
  declarations: [
    // ...
  ],
  imports: [
    // ...
    IonicStorageModule.forRoot()
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    // ...
  ],
  providers: [
    // ...
  ]
})
export class AppModule {}
```

#### configuration ( optional )
```ts
@NgModule({
  declarations: [...],
  imports: [
    IonicStorageModule.forRoot({
      name: '__mydb',
driverOrder: ['indexeddb', 'sqlite', 'websql']
    })
  ],
  bootstrap: [...],
  entryComponents: [...],
   providers: [...]
})
```

#### app.ts
```ts
import { Storage } from '@ionic/storage';

export class MyApp {
  constructor(private storage: Storage) { }

  ...

  // set a key/value
  storage.set('name', 'Max');

  // Or to get a key/value pair
  storage.get('age').then((val) => {
    console.log('Your age is', val);
  });
}
```
