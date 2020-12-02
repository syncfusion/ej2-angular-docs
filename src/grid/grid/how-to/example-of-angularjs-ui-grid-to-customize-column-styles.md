---
title: "Example of AngularJS UI Grid to Customize Column Styles"
component: "Grid"
description: "Learn how to Customize Column Styles with an example of AngularJS UI Grid."
---

# Example of AngularJS UI Grid to Customize Column Styles

You can customise the appearance of header and content of the particular column using the
[`customAttributes`](../../api/grid/column/#customattributes) property.

To customize the grid column, follow the given steps:

**Step 1**:

Create a css class with custom style to override the default style for rowcell and headercell.

```css
.e-grid .e-rowcell.customcss{
    background-color: #ecedee;
    color: 'red';
    font-family: 'Bell MT';
    font-size: 20px;
}

.e-grid .e-headercell.customcss{
    background-color: #2382c3;
    color: white;
    font-family: 'Bell MT';
    font-size: 20px;
}

```

**Step 2**:

Add the custom css class to particular column by using [`customAttributes`](../../api/grid/column/#customattributes) property.

{% tab template="grid/custom-column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [height]='315'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' [customAttributes]='customAttributes' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit{

    public data: Object[];
    public customAttributes: Object;

    ngOnInit(): void{
        this.data = data;
        this.customAttributes = {class: 'customcss'};
    }
}

```

{% endtab %}
