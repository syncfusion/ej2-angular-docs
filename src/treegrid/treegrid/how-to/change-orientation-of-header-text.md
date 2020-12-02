---
title: "Change the Orientation of Header Text"
component: "TreeGrid"
description: "Learn how to Change the Orientation of Header Text."
---

# Change the orientation of header Text

You can change the orientation of the header text by using the [`customAttributes`](../api/treegrid/column/#customattributes) property.

Ensure the following steps:

**Step 1**:

Create a CSS class with orientation style for Tree Grid header cell.

```css
.orientationcss .e-headercelldiv {
    transform: rotate(90deg);
}

```

**Step 2**:

Add the custom CSS class to particular column by using [`customAttributes`](../api/treegrid/column/#customattributes) property.

```typescript
    <e-column field='EndDate' headerText='End Date' width='90' format="yMd" textAlign='Right' [customAttributes]='customAttributes' ></e-column>

```

**Step 3**:

Resize the header cell height in [`create`](../api/treegrid/#create) event by using the following code.

```typescript
  public setHeaderHeight() {
    /** Obtain the width of the headerText content */
    const textWidth: number = (document.querySelector(".orientationcss > div") as HTMLElement).scrollWidth;
    const headerCell: NodeList = document.querySelectorAll(".e-headercell");
    for(let i: number = 0; i < headerCell.length; i++) {
      /** Assign the obtained textWidth as the height of the headerCell */
      ((headerCell as any).item(i)).style.height = textWidth + 'px';
    }
  }

```

{% tab template="treegrid/header-orientation", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild, ViewEncapsulation } from '@angular/core';
import { projectData } from './datasource';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    styleUrls: ['./app/app.component.css'],
    encapsulation: ViewEncapsulation.None,
    template: `<ejs-treegrid #treegrid [dataSource]='data' idMapping='TaskID' parentIdMapping='parentID' [height]='194' [treeColumnIndex]='1' (created)='setHeaderHeight($event)'  >
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='100' ></e-column>
            <e-column field='StartDate' headerText='Start Date' width='90' format="yMd" textAlign='Right' ></e-column>
            <e-column field='EndDate' headerText='End Date' width='90' format="yMd" textAlign='Center' [customAttributes]='customAttributes' ></e-column>
            <e-column field='Duration' headerText='Duration' width='90' textAlign='Right' ></e-column>
            <e-column field='Progress' headerText='Progress' width='90' textAlign='Right' ></e-column>
        </e-columns>
    </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[] = [];
    public customAttributes: Object;

    ngOnInit(): void {
        this.data = projectData;
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