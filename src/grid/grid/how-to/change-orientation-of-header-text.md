---
title: "Change the Orientation of Header Text"
component: "Grid"
description: "Learn how to Change the Orientation of Header Text."
---

# Change the Orientation of Header Text

You can change the orientation of the header text by using the [`customAttributes`](../../api/grid/column/#customattributes) property.

To change the Orientation of Header Text, Ensure the following steps:

**Step 1**:

Create a css class with orientation style for grid header cell.

```css
.orientationcss .e-headercelldiv {
    transform: rotate(90deg);
}

```

**Step 2**:

Add the custom css class to particular column by using [`customAttributes`](../../api/grid/column/#customattributes) property.

```typescript
    <e-column field='Freight' headerText='Freight' textAlign='Center' format='C2' [customAttributes]='customAttributes' width=80></e-column>

```

**Step 3**:

Resize the header cell height by using the following code.

```typescript
setHeaderHeight(args) {
    let textWidth: number = document.querySelector('.orientationcss > div').scrollWidth;//Obtain the width of the headerText content.
    let headerCell: NodeList = document.querySelectorAll('.e-headercell');
    for(let i: number = 0; i < headerCell.length; i++) {
        (<HTMLElement>headerCell.item(i)).style.height = textWidth + 'px'; //Assign the obtained textWidth as the height of the headerCell.
    }
}

```

{% tab template="grid/header-orientation", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='240' (created)='setHeaderHeight($event)' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Center'
                         format='C2' [customAttributes]='customAttributes' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=100 ></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public customAttributes: object;

    ngOnInit(): void {
        this.data = data;
        this.customAttributes = { class: 'orientationcss' };
    }
    setHeaderHeight(args) {
        const textWidth = document.querySelector('.orientationcss > div').scrollWidth; // Obtain the width of the headerText content.
        const headerCell: NodeList = document.querySelectorAll('.e-headercell');
        for (let i = 0; i < headerCell.length; i++) {
            // Assign the obtained textWidth as the height of the headerCell.
            (headerCell.item(i) as HTMLElement).style.height = textWidth + 'px';
        }
    }
}

```

{% endtab %}
