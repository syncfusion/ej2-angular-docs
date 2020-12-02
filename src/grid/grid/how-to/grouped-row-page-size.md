---
title: "How to show grouped rows based on the pageSize"
component: "Grid"
description: "Learn how to show the grouped row based on the pageSize"
---

# How to show grouped rows based on the pageSize

By default, we have displayed the no of records based on the [`pageSize`](../../api/grid/pageSettings/#pagesize). If you want to show grouped column rows based on the [`pageSize`](../../api/grid/pageSettings/#pagesize) then we suggest you to use the below way.

In the below sample, we have overridden the default **generateQuery** to display the grouped rows instead of grid rows based on the [`pageSize`](../../api/grid/pageSettings/#pagesize).

{% tab template="grid/filtering1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { Data } from '@syncfusion/ej2-angular-grids';

const old = Data.prototype.generateQuery;
Data.prototype.generateQuery = function() {
    const query = old.call(this, true);
    this.pageQuery(query);
    return query;
};

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowPaging]="true" [pageSettings]='initialPage'
     [allowGrouping]="true" [groupSettings]="groupOptions" [allowPaging]='true'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='ShipCountry' headerText='ShipCountry' width=140></e-column>
                    <e-column field='CustomerID' headerText='Name' width=140></e-column>
                    <e-column field='ShipName' headerText='ShipName' width=140></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                </e-columns>
                </ejs-grid>`
})

export class AppComponent implements OnInit {

    public data: object[];
    public groupOptions: object;
    public initialPage: object;

    ngOnInit(): void {
        this.data = data;
        this.groupOptions = { showGroupedColumn: false, columns: ['ShipCountry'] };
        this.initialPage = { pageSize: 5 };
    }
}

```

{% endtab %}