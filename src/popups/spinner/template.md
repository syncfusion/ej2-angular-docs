---
title: "Template"
component: "Spinner"
description: "This example demonstrates how to customize the Essential JS 2 Spinner control based on different needs."
---

# Set the template to the Spinner

You can use custom templates on the Spinner instead of the default Spinner by specifying the template in the `setSpinner` method.

The following steps explains you on how to define template for Spinner.

* Import the `setSpinner` method from `ej2-angular-popups` library into your `app.component.ts` as shown in below.

```typescript
import { setSpinner } from '@syncfusion/ej2-angular-popups';
```

* Pass your custom template to the `setSpinner` method like as below.

```typescript

// Specify the template content to be displayed in the Spinner

setSpinner({ template: '<div style="width:100%;height:100%" class="custom-rolling"><div></div></div>'});
```

> You should set the template to the Spinner before creating the respective Essential JS 2 component.
> Also,until we replace `setSpinner` template, the further Essential JS 2 component rendering is created
> with given template only.

* Now, render the Essential JS 2 component. It's render the Spinner with the template specified in the `setSpinner` method.

> In the below sample, we have rendered the Grid component with custom Spinner using `setSpinner` method.
> You have to define the styles for the template in `index.css`.

{% tab template="spinner/set-spinner", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component, ViewChild, OnInit } from '@angular/core';
import { GridComponent } from '@syncfusion/ej2-angular-grids';
import { setSpinner } from '@syncfusion/ej2-angular-popups';
import { data } from './datasource.ts';

@Component({
    selector: 'app-container',
    template: `
        <ejs-grid #grid1 [dataSource]='gridData' (created)='onFirstGridCreated()'>
            <e-columns>
                <e-column field='OrderID' headerText='Order ID' textAlign='right' width=120 type='number'></e-column>
                <e-column field='CustomerID' headerText='Customer ID' width=140 type='string'></e-column>
                <e-column field='Freight' headerText='Freight' textAlign='right' format='C' width=120></e-column>
                <e-column field='OrderDate' headerText='Order Date' width=120  format='yMd' width=140></e-column>
            </e-columns>
        </ejs-grid>
        <br/>
        <br/>
        <ejs-grid #grid2 [dataSource]='gridData' (created)='onSecondGridCreated()'>
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
    @ViewChild('grid1') grid_1: GridComponent;
    @ViewChild('grid2') grid_2: GridComponent;
    public gridData: Object[];

    constructor() {}

    public ngOnInit(): void {
        this.gridData = data.slice(0, 7);
    }

    public onFirstGridCreated(): void {
        this.grid_1.hideSpinner = () => true;
        setSpinner({ template: '<div style="width:100%;height:100%" class="custom-rolling"><div></div></div>' });
    }

    public onSecondGridCreated(): void {
        this.grid_2.hideSpinner = () => true;
    }
}

```

{% endtab %}