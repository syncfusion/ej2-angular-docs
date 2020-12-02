---
title: "Customize Column Styles"
component: "TreeGrid"
description: "Learn how to Customize Column Styles."
---

# Customize column styles

You can customise the appearance of header and content of the particular column using the
[`customAttributes`](../../api/treegrid/column/#customattributes) property.

To customize the Tree Grid column, follow the given steps:

**Step 1**:

Create a CSS class with custom style to override the default style for rowcell and headercell.

```css

.e-treegrid .e-rowcell.customcss{
    background-color: #ecedee;
    font-family: 'Bell MT';
    color: 'red';
    font-size: '20px';
}

.e-treegrid .e-headercell.customcss{
    background-color: #2382c3;
    color: white;
    font-family: 'Bell MT';
    font-size: '20px';
}

```

**Step 2**:

Add the custom CSS class to particular column by using [`customAttributes`](../api/treegrid/column/#customattributes) property.

```typescript
<e-column field='TaskName' headerText='Task Name' width='170' [customAttributes]='customAttributes'></e-column>

```

{% tab template="treegrid/custom-column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild, ViewEncapsulation } from '@angular/core';
import { projectData } from './datasource';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    styleUrls: ['./app/app.component.css'],
    encapsulation: ViewEncapsulation.None,
    template: `<ejs-treegrid [dataSource]='data' idMapping='TaskID' parentIdMapping='parentID' [treeColumnIndex]='1' [height]='317'>
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='100' [customAttributes]='customAttributes'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='90' format="yMd" textAlign='Right'></e-column>
            <e-column field='EndDate' headerText='End Date' width='90' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='90' textAlign='Right'></e-column>
        </e-columns>
    </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[] = [];
    public customAttributes: Object;

    ngOnInit(): void {
        this.data = projectData;
        this.customAttributes = {class: 'customcss'};
    }
}

```

{% endtab %}