---
title: "Types"
component: "Spinner"
description: "This example demonstrates how to change the type of the Essential JS 2 Spinner control based on theme."
---

# Change the type of the Spinner

By default, the Spinner is loaded in the applicable Essential JS 2 component based on the theme imported into
the page. Based on the theme, the type is set to the Spinner.

The available types are:
* Material
* Fabric
* Bootstrap

You can change the Essential JS 2 component spinner type by passing the type of the spinner as parameter to the `setSpinner` method like as below.

```typescript

// Specify the type of the Spinner to be displayed
setSpinner({ type: 'Bootstrap'});
```

> After Essential JS 2 component creation only, you can change the Essential JS 2 component spinner type.

{% tab template="spinner/default-sample", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component, ViewChild, OnInit } from '@angular/core';
import { GridComponent } from '@syncfusion/ej2-angular-grids';
import { setSpinner } from '@syncfusion/ej2-angular-popups';
import { data } from './datasource.ts';

@Component({
    selector: 'app-container',
    template: `
        <h5> Grid is rendered with Bootstrap type Spinner </h5>
        <ejs-grid #grid [dataSource]='gridData' (created)='gridCreated()'>
            <e-columns>
                <e-column field='OrderID' headerText='Order ID' textAlign='right' width=120 type='number'></e-column>
                <e-column field='CustomerID' headerText='Customer ID' width=140 type='string'></e-column>
                <e-column field='Freight' headerText='Freight' textAlign='right' format='C' width=120></e-column>
                <e-column field='OrderDate' headerText='Order Date' width=120  format='yMd' width=140></e-column>
            </e-columns>
        </ejs-grid>
    `
})
export class AppComponent implements OnInit {
    @ViewChild('grid') grid: GridComponent;

    public gridData: Object[];

    constructor() {}

    public ngOnInit(): void {
        this.gridData = data.slice(0, 7);
    }

    public gridCreated(): void {
        this.grid.hideSpinner = () => true;
        setSpinner({ type: 'Bootstrap' });
    }
}

```

{% endtab %}