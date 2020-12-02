---
title: "Customize the icon for column menu"
component: "Grid"
description: "Learn how to Customize the icon for column menu."
---

# Customize the icon for column menu

You can customize the column menu icon by overriding the default grid class **.e-icons.e-columnmenu** with a custom property **content** as mentioned below.

```css
.e-grid .e-columnheader .e-icons.e-columnmenu::before {
              content: "\e941";
      }
```

In the below sample, grid is rendered with a customized column menu icon.

{% tab template="grid/custom-column-menu-icon", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { ColumnMenuService } from '@syncfusion/ej2-angular-grids';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315' showColumnMenu='true' >
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' format='C2' width=90></e-column>
                        <e-column field='ShipName' headerText='Ship Name' width=120></e-column>
                    </e-columns>
                </ejs-grid>`,
   providers: [ColumnMenuService]
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}


```

{% endtab %}
