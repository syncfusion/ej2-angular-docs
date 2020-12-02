---
title: "Customize Pager DropDown"
component: "Grid"
description: "Learn how to Customize Pager DropDown."
---

# Customize Pager DropDown

To customize default values of pager dropdown, you need to define [`pageSizes`](../../api/grid/pageSettingsModel/#pagesizes) as array of strings.

{% tab template="grid/custom-column", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' allowPaging='true' [pageSettings]='initialPage'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public initialPage: object;

    ngOnInit(): void {
        this.data = data;
        this.initialPage = { pageSizes: ['5', '10', 'All'], };
    }
}

```

{% endtab %}
