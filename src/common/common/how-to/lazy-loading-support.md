# Lazy Loading support with Syncfusion components in Angular

This section explains how to do Lazy Loading with Essential JS2 Angular components in Angular.  

## Lazy Loading

In the Lazy Loading technique, you can load additional payload only on demand. You can lazy load the Syncfusion components and routes in Angular by using Code splitting. The Angular will load only the needed `NgModules` for a path instead of loading everything in the application on initial start of the application. This is the main use of Code splitting. So, it reduces the initial loading time of the application.

## Getting Started

For creating the Syncfusion components in Angular, refer to the [getting started](https://ej2.syncfusion.com/angular/documentation/introduction/) documentation. Also read the Angular [lazy-loading](https://angular.io/guide/lazy-loading-ngmodules) documentation for more information.

## Angular sample with Lazy Loading Routes

Syncfusion Angular application is created with routing enabled and get the sample from the Angular [lazy-loading](https://angular.io/guide/lazy-loading-ngmodules). Now, create the Syncfusion Calendar and Grid components separately.

In the `customers.component.ts` file, Syncfusion Calendar component has been added.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-customers',
  template: `<ejs-calendar [value]='dateValue' [min]='minDate' [max]='maxDate'></ejs-calendar>`
})
export class CustomersComponent implements OnInit {
  public month: number = new Date().getMonth();
  public fullYear: number = new Date().getFullYear();
  public dateValue: Date = new Date(this.fullYear, this.month, 11);
  public minDate: Date = new Date(this.fullYear, this.month, 9);
  public maxDate: Date = new Date(this.fullYear, this.month, 15);
  constructor() { }

  ngOnInit() {
  }

}
```

In the `orders.component.ts` file, Syncfusion Grid component has been added.

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-orders',
  template: ` <ejs-grid [dataSource]='data'>
  <e-columns>
      <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
      <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
      <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
      <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
  </e-columns>
  </ejs-grid>`,
})
export class OrdersComponent implements OnInit {
  public data: DataManager;
  constructor() { }

  ngOnInit() {
    this.data = new DataManager({
      url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Orders/?$top=7',
      adaptor: new ODataV4Adaptor()
    });
  }
}
```

In the `app-routing.module.ts` file, we have implemented code splitting to dynamically import the components.

```typescript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';


const routes: Routes = [
  {
    path: 'customers',
    loadChildren: () => import('./customers/customers.module').then(m => m.CustomersModule)
  },
  {
    path: 'orders',
    loadChildren: () => import('./orders/orders.module').then(m => m.OrdersModule)
  }
];

@NgModule({
  imports: [
    RouterModule.forRoot(routes)
  ],
  exports: [RouterModule],
  providers: []
})
export class AppRoutingModule { }
```

## Run the application

Run the application using the following commands.

```bash
npm install
npm run start
```

## Sample Link

Find this sample in the [Github link](https://github.com/SyncfusionExamples/EJ2-Angular-Lazy-loading)