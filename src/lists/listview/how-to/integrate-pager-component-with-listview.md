# How to integrate pager component with listview

The first and foremost step is to obtain the `Pager` component from `Grid`. Install the ej2-angular-grids package using the following command.

```shell
npm install @syncfusion/ej2-angular-grids --save
```

Import the Pager to the ListView sample which has been created.

```shell
import { Pager } from "@syncfusion/ej2-angular-grids";
```

The [`totalRecordsCount`](https://ej2.syncfusion.com/documentation/api/pager/#totalrecordscount) property of Pager must be specified whenever using this particular component. By using [`pageSize`](https://ej2.syncfusion.com/documentation/api/pager/#pagesize) property, the number of list items to be displayed is made available. The [`pageCount`](https://ej2.syncfusion.com/documentation/api/pager/#pagecount) property allows the user to specify the visibility of the page numbers accordingly. Since the paging sample in the upcoming code snippet uses these three properties, the explanation provided here were minimal and to the point. For further API concerns in Pager component, [click here](https://ej2.syncfusion.com/documentation/api/pager/).

With the help of the [`query`](../../api/list-view#query) property of ListView, the user can specify the number of records to be displayed in the current page.

The `query` property helps in splitting the entire datasource based on our convenience. In the sample provided below, when clicking the next button in pager, it fetches the datasource based on page size and current page of Pager component.

The [`headerTemplate`](../../api/list-view#headertemplate) and the [`template`](../../api/list-view#template) property of ListView is defined within ng-template. The required styles can be changed here accordingly.

```typescript
public clickevent(args) {
  this.query = new Query().range((args.currentPage - 1) * this.pagesize, (args.currentPage * this.pagesize));
}
```

In the above code snippet, the event stores the [`currentPage`](https://ej2.syncfusion.com/documentation/api/pager/#currentpage) value, and the datasource which is to be displayed in the next page is obtained.

Note: When `pageize` isn't mentioned, it defaults to 12 records per page.

{% tab template="listview/paging", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript

import { Component} from '@angular/core';
import { Browser } from '@syncfusion/ej2-base';
import { datasource } from './dataSource';
import { DataManager, Query, JsonAdaptor } from '@syncfusion/ej2-data';
import { Pager } from "@syncfusion/ej2-angular-grids";
@Component({
    selector: 'my-app',
    template: `<div class="control-section">
  <ejs-listview id='listview' [dataSource]='data' [query]='query' showHeader='true' >
    <ng-template #headerTemplate let-data="">
      <table class="w-100"> <tr><td class="w-25">Order ID</td><td class="w-45">Ship       Name</td><td class="w-25">Ship City</td></tr></table>
    </ng-template>
    <ng-template #template let-data="">
      <table class="w-100"> <tr><td class="w-25">{{data.OrderID}}</td><td class="w-45">{{data.ShipName}}</td><td class="w-25" >{{data.ShipCity}}</td></tr></table>
    </ng-template>
  </ejs-listview>
  <ejs-pager [pageSize]= 'pagesize' [totalRecordsCount]='totalrec' [pageCount]='pageCount' (click)='clickevent($event)'>
  </ejs-pager>
</div>`
})

export class AppComponent {
public totalrec: number = datasource.length;
public pagesize: number = 10;
public pageCount: number = 2;
//Define an array of JSON data
public data: Object = new DataManager({
    json: datasource,
    adaptor: new JsonAdaptor
});
public query = new Query().range(0,this.pagesize);
public clickevent(args) {
  this.query = new Query().range((args.currentPage - 1) * this.pagesize, (args.currentPage * this.pagesize));
}
constructor(){
    this.templatecheck = Browser.isDevice;
}
}

```

{% endtab %}
