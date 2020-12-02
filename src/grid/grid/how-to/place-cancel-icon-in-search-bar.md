---
title: "Place a cancel icon in search bar"
component: "Grid"
description: "Learn how to Place a cancel icon in search bar."
---

# Place a cancel icon in search bar

By default, the search bar in the grid doesn't have a **cancel** icon. If you want to add the cancel icon you can achieve it by invoking [`created`](https://ej2.syncfusion.com/javascript/documentation/api/grid/#created) event. In the event, the cancel icon is rendered on the span element and append to the search bar. If the cancel icon is pressed, the records in the search bar will be cleared using click event.

{% tab template="grid/print", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, Inject, ViewChild } from '@angular/core';
import { data } from './datasource';
import { ToolbarService, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
  selector: 'app-root',
  template: `<ejs-grid #grid [dataSource]='data' allowPaging="true" [pageSettings]='pageSettings' [toolbar]='toolbar' (created)="created($event)" height='273px'>
           <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign= 'Right' editType= 'numericedit' width=120 format= 'C2'></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' editType= 'dropdownedit' width=150></e-column>
                </e-columns>
    </ejs-grid>`

})
export class AppComponent implements OnInit {

  public data: Object[];
  public pageSettings: Object;
  public toolbar: string[];
  @ViewChild("grid", { static: true })
  public grid: GridComponent;
  public ngOnInit(): void {
    this.data = data;
    this.pageSettings = { pageCount: 5 };
    this.toolbar = ['Search'];
  }
  public created(args) {
    var gridElement = this.grid.element;
    var span = document.createElement("span");
    span.className = "e-clear-icon";
    span.id = gridElement.id + "clear";
    span.onclick = this.cancelBtnClick.bind(this);
    gridElement.querySelector(".e-toolbar-item .e-input-group").appendChild(span);
  }
  public cancelBtnClick(args) {
    this.grid.searchSettings.key = "";
    (this.grid.element.querySelector(".e-input-group.e-search .e-input") as any).value = "";
  }
}
```

{% endtab %}
