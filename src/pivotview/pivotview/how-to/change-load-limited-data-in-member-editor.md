# Improve filter dialog performance when handling large data

In the filter dialog, you can set the limit to display the field values while loading large data. Based on this limit, the initial loading will complete quickly without any performance constraint. You can use the search option to refine the field values from the exceeded limit and refine the data further. A message with the remaining data count will be displayed in the member editor. The data limit can be set in the `maxNodeLimitInMemberEditor` property.

By default, the property holds the value 1000.

> The property is available in both pivot table and field list components.

In the following example, the limit of data in the member editor is set to 100. So, the member editor of the `ProductID` field shows only its first 100 members from its 1000 members.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, PivotView, GroupingBarService, FieldListService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [GroupingBarService, FieldListService],
  // specifies the template string for the pivot table component
  template: `<div><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings showGroupingBar='true' width=width maxNodeLimitInMemberEditor=maxNodeLimitInMemberEditor showFieldList='true'></ejs-pivotview></div>`
})

export class AppComponent {

    public width: string;
    public dataSourceSettings: IDataOptions;
    public maxNodeLimitInMemberEditor: number;
    public date1: number;
    public date2: number;
    data(count: number) {
        let result: Object[] = [];
        let dt: number = 0;
        for (let i: number = 1; i < count + 1; i++) {
            dt++;
            let round: string;
            let toString: string = i.toString();
            if (toString.length === 1) {
                round = "0000" + i;
            } else if (toString.length === 2) {
                round = "000" + i;
            } else if (toString.length === 3) {
                round = "00" + i;
            } else if (toString.length === 4) {
                round = "0" + i;
            } else {
                round = toString;
            }
            result.push({
                ProductID: "PRO-" + round,
                Year: "FY " + (dt + 2013),
                Price: Math.round(Math.random() * 5000) + 5000,
                Sold: Math.round(Math.random() * 80) + 10
            });
            if (dt / 4 == 1) {
                dt = 0;
            }
        }
        return result;
    }
    ngOnInit(): void {

        this.width = "100%";
        this.maxNodeLimitInMemberEditor= 100;

        this.dataSourceSettings = {
            dataSource: this.data(1000) as IDataSet[],
            enableSorting: false,
            expandAll: true,
            formatSettings: [{ name: 'Price', format: 'C0' }],
            rows: [{ name: 'ProductID' }],
            columns: [{ name: 'Year' }],
            values: [{ name: 'Price', caption: 'Unit Price' }, { name: 'Sold', caption: 'Unit Sold' }]
        };
    }
 }

```

{% endtab %}
