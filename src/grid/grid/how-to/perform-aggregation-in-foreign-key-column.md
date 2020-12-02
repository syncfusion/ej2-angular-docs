---
title: "Perform aggregation in Foreign Key Column"
component: "Grid"
description: "Learn how to Perform aggregation in Foreign Key Column."
---

# Perform aggregation in Foreign Key Column

Default aggregations are not supported in a foreign key column.
You can achieve aggregation for the foreign key column by using custom the aggregates.
The following example demonstrates the way to achieve aggregation in foreign key column.

In the following example, The **Employee Name** is a foreign key column and the aggregation for the foreign column was calculated in customAggregateFn.

{% tab template="grid/foreignkey", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ForeignKeyService, AggregateService, getForeignData, CustomSummaryType,
     AggregateColumnModel, GridComponent } from '@syncfusion/ej2-angular-grids';
import { data, employeeData } from './datasource';
import { getValue } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='280'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='EmployeeID' headerText='Employee Name' width=120
                         foreignKeyValue='FirstName' [dataSource]='employeeData'></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130  ></e-column>
                    </e-columns>
                    <e-aggregates>
                        <e-aggregate>
                            <e-columns>
                                <e-column field="EmployeeID" type="Custom" [customAggregate]= 'customAggregateFn'>
                                    <ng-template #footerTemplate let-data>
                                        Count of Margaret:  {{data.Custom}}
                                    </ng-template>
                                </e-column>
                            </e-columns>
                        </e-aggregate>
                    </e-aggregates>
                </ejs-grid>`,
    providers: [ForeignKeyService, AggregateService]
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public grid: GridComponent;
    public employeeData: object[];

    // Custom Aggregate function for foreign column
    public customAggregateFn: CustomSummaryType = (data1: any, column: AggregateColumnModel) => {
        return data1.result.filter((dObj: object) => {
            return getValue('FirstName', getForeignData(this.grid.getColumnByField(column.field), dObj)[0]) === 'Margaret';
        }).length;
    }

    ngOnInit(): void {
        this.data = data;
        this.employeeData = employeeData;
    }
}
  
```

{% endtab %}
