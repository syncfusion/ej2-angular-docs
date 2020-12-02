---
title: "Tooltip"
component: "Pivot Table"
description: "Describes about enabling and disabling tooltip in pivot table"
---

# Tooltip

The tooltip can be enabled or disabled by setting the [`showTooltip`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#showtooltip) property to **true** or **false**. By default, tooltip is enabled in the pivot table.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width [showTooltip]='false'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;

    ngOnInit(): void {
        this.width = '100%';

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            formatSettings: [{ name: 'Amount', format: 'C2', useGrouping: false,
                    minimumSignificantDigits: 1, maximumSignificantDigits: 3 }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            filters: []
        };
    }
}

```

{% endtab %}

## Tooltip Template

User can design their own tooltip by setting the property [`tooltipTemplate`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#tooltiptemplate) with own HTML elements. The property accepts both HTML string and ID attribute. The following place holders are available to display its dynamic values inside the HTML elements.

`${rowHeaders}` – Row headers of the selected value cell.

`${columnHeaders}`  – Column headers of the selected value cell.

`${rowFields}` – Row fields of the selected value cell.

`${columnFields}` – Column fields of the selected value cell.

`${valueField}` – Field name of the selected value cell.

`${aggregateType}` – Aggregate type of the selected value cell.

`${value}` – Formatted value of the selected value cell.

The tooltip customization is common for both pivot table and pivot chart or it can be done individually as well. To customize the pivot table tooltip, the above procedure needs to be followed. To customize the pivot chart tooltip alone use `template` property of tooltip under [`chartSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/chartSettings).

In the below sample, the pivot table and pivot chart shows customized tooltip layouts.

{% tab template="pivot-grid/tooltipTemplate", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import {
    IDataOptions, PivotView, ToolbarService, ToolbarItems, DisplayOption, IDataSet, PivotChartService
} from '@syncfusion/ej2-angular-pivotview';
import { ChartSettings } from '@syncfusion/ej2-pivotview/src/pivotview/model/chartsettings';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [ToolbarService, PivotChartService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings showToolbar='true' width='100%' [displayOption]='displayOption' height='350' tooltipTemplate='#Template' [toolbar]='toolbarOptions' [chartSettings]='chartSettings'></ejs-pivotview></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public toolbarOptions: ToolbarItems[];
    public displayOption: DisplayOption;
    public chartSettings: ChartSettings;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;
    ngOnInit(): void {
        this.displayOption = { view: 'Both' } as DisplayOption;

        this.chartSettings = { chartSeries: { type: 'Column', animation: { enable: false } },
                               tooltip:{ template:'<span class="wrap">${aggregateType} of ${valueField}: ${value}</span>' }
      } as ChartSettings;

        this.toolbarOptions = ['Grid', 'Chart'] as ToolbarItems[];
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };
    }
 }
```

{% endtab %}