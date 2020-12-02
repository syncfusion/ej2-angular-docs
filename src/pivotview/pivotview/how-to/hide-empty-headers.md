# Hide empty headers

If the raw data for a particular field is not defined, it will be shown as 'Undefined' in the pivot table headers. You can hide those headers by setting the [`showHeaderWhenEmpty`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettingsModel/#showheaderwhenempty) property to **false** in the pivot table.

For example, if the raw data for the field 'Country' is defined as **"United Kingdom"** and **"State"** is not defined means, it will be shown as **"United Kingdom >> Undefined"** in the header section. Here, you can hide those 'Undefined' header using the [`showHeaderWhenEmpty`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettingsModel/#showheaderwhenempty) property.

> By default, this property is set as **true**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, IDataSet, PivotView, FieldListService } from '@syncfusion/ej2-angular-pivotview';
import { pivotNullData } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [FieldListService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings showFieldList='true' width=width></ejs-pivotview></div>`
})

export class AppComponent {

    public width: string;
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = '100%';

        this.dataSourceSettings = {
            dataSource: pivotNullData,
            expandAll: false,
            rows: [{ name: 'Country' }, { name: 'State'}],
            columns: [{ name: 'Product', showNoDataItems: true }, { name: 'Date' }],
            values: [{ name: 'Amount' }, { name: 'Quantity' }],
            showHeaderWhenEmpty: false
        };
    }
 }

```

{% endtab %}
