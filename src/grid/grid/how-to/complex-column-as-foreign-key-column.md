---
title: "Set complex column as Foreignkey column"
component: "Grid"
description: "Learn how to set complex column as Foreignkey column."
---

# Set complex column as Foreignkey column

The following example shows how to set the complex column as foreign key column.

In the following example, **Employee.EmployeeID** is a complex column and also declared as a foreign column which shows **FirstName** column from foreign data.

{% tab template="grid/foreignkey", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data, employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='Employee.EmployeeID' headerText='Employee Name'
                         width=120 foreignKeyValue='FirstName' foreignKeyField='EmployeeID' [dataSource]='employeeData'></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130  ></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public employeeData: object[];

    ngOnInit(): void {
        this.data = data.slice(0, 5);
        this.employeeData = employeeData.slice(0, 5);
    }
}

```

{% endtab %}