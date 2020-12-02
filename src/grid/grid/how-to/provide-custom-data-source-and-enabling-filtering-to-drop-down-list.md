---
title: "Provide custom data source and enabling filtering to DropDownList"
component: "Grid"
description: "Learn how to Provide custom data source and enabling filtering to DropDownList."
---

# Provide custom data source and enabling filtering to DropDownList

You can provide data source to the DropDownList by using the [`columns.edit.params`](../../api/grid/column/#edit) property.

While setting new data source using edit params, you must specify a new [`query`](../../api/drop-down-list#query) property too for the DropDownList as follows,

```typescript
{
    this.countryParams = {
        params:   {
            allowFiltering: true,
            dataSource: this.country,
            fields: {text:'countryName',value:'countryName'},
            query: new Query(),
            actionComplete: () => false
            }
        }
}

```

You can also enable filtering for the DropDownList by passing the [`allowFiltering`](../../api/drop-down-list#allowfiltering) as **true** to the edit params.

In the below demo, DropDownList is rendered with custom Datasource for the **ShipCountry** column and enabled filtering to search DropDownList items.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { Query, DataManager } from '@syncfusion/ej2-data';
import { cascadeData } from './datasource';
import { EditSettingsModel, ToolbarItems, IEditCell } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' editType= 'dropdownedit'
                     [edit]='countryParams' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public countryParams: IEditCell;

    public country: object[] = [
        { countryName: 'United States', countryId: '1' },
        { countryName: 'Australia', countryId: '2' },
        { countryName: 'India', countryId: '3' }
    ];

    ngOnInit(): void {
        this.data = cascadeData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
        this.countryParams = {
            params: {
                allowFiltering: true,
                dataSource: new DataManager(this.country),
                fields: { text: 'countryName', value: 'countryName' },
                query: new Query(),
                actionComplete: () => false
            }
        };
    }

}

```

{% endtab %}
