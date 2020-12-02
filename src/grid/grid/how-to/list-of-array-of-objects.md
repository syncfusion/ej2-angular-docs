---
title: "Complex Data Binding with list of Array Of Objects"
component: "Grid"
description: "Learn how to set Complex data for datasource having Array Of Objects."
---

# Complex Data Binding with list of Array Of Objects

The following example shows how to set Complex field for datasource having Array Of Objects.

{% tab template="grid/complex-data", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { complexData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='Names.0.FirstName' headerText='First Name' width=120></e-column>
                        <e-column field='Names.0.LastName' headerText='Last Name' width=120></e-column>
                        <e-column field='Title' headerText='Title' width=150></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = complexData.slice(0, 5);
    }
}

```

{% endtab %}