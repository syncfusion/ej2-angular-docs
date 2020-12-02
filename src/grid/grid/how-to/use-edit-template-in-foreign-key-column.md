---
title: "Use Edit Template in Foreign Key Column"
component: "Grid"
description: "Learn how to Use Edit Template in Foreign Key Column."
---

# Use Edit Template in Foreign Key Column

By default, foreign key column uses dropdown component for editing.
You can render other than the dropdown by using the [`column.edit`](../../api/grid/column/#edit) property.
The following example demonstrates the way of using edit template in foreign column.

In the following example, The **Employee Name** is a foreign key column and while editing, AutoComplete component is rendered instead of DropDownList.

{% tab template="grid/foreignkey", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { createElement } from '@syncfusion/ej2-base';
import { ForeignKeyService, EditService, IEditCell, EditSettingsModel, ToolbarService, Column } from '@syncfusion/ej2-angular-grids';
import { DataManager, Query } from '@syncfusion/ej2-data';
import { AutoComplete } from '@syncfusion/ej2-angular-dropdowns';
import { data, employeeData } from './datasource';


@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='270' [editSettings]='editoption' [toolbar]='toolbar'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' isPrimaryKey='true' textAlign='Right' width=100></e-column>
                        <e-column field='EmployeeID' headerText='Employee Name' width=120
                        foreignKeyValue='FirstName' [dataSource]='employeeData' [edit]='edit'></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130></e-column>
                    </e-columns>
                </ejs-grid>`,
    providers: [ForeignKeyService, EditService, ToolbarService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public employeeData: object[];
    public editoption: EditSettingsModel = { allowEditing: true };
    public autoComplete: AutoComplete;
    toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    public edit: IEditCell = {
        create: () => { // to create input element
            return createElement('input');
        },
        read: () => { // return edited value to update data source
            const EmployeeID = 'EmployeeID';
            const value = new DataManager(employeeData).executeLocal(new Query().where('FirstName', 'equal', this.autoComplete.value));
            return value.length && value[0][EmployeeID]; // to convert foreign key value to local value.
        },
        destroy: () => { // to destroy the custom component.
            this.autoComplete.destroy();
        },
        write: (args: { rowData: object, column: Column, foreignKeyData: object,
             element: HTMLTableCellElement }) => { // to show the value for date picker
            this.autoComplete = new AutoComplete({
                dataSource: employeeData,
                fields: { value: args.column.foreignKeyValue },
                value: args.foreignKeyData[0][args.column.foreignKeyValue]
            });
            this.autoComplete.appendTo(args.element);
        }
    }

    ngOnInit(): void {
        this.data = data;
        this.employeeData = employeeData;
    }
}


```

{% endtab %}
