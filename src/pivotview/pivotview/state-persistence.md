---
title: "State Persistence"
component: "Pivot Table"
description: "Describes about persistence in pivot table"
---

# State Persistence

State persistence allows user to maintain the current state of the component along with its report bounded in the browser local storage (cookie). Even if the browser is refreshed or if you move to the next page within the browser, components state will be persisted. State persistence stores the Pivot Table object in the local storage when [`enablePersistence`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#enablepersistence) property in pivot table is set to **true**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { IDataOptions, PivotViewComponent } from '@syncfusion/ej2-angular-pivotview';
import { ChartSettings } from '@syncfusion/ej2-pivotview/src/pivotview/model/chartsettings';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the pivot table component
  template: `<div><ejs-pivotview #pivotview id='PivotView' height='300' [dataSourceSettings]=dataSourceSettings enablePersistence='true' ></ejs-pivotview></div>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotViewComponent;

    ngOnInit(): void {

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
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

# Save and Load Pivot Layout

You can save the current layout of the pivot table by using [`getPersistData`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#getpersistdata) in string format. The saved layout can be loaded to pivot table any time by passing the saved data as a parameter to [`loadPersistData`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#loadpersistdata) method in the pivot table.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { IDataOptions, PivotViewComponent } from '@syncfusion/ej2-angular-pivotview';
import { ChartSettings } from '@syncfusion/ej2-pivotview/src/pivotview/model/chartsettings';
import { Pivot_Data } from './datasource.ts';
import { Button } from '@syncfusion/ej2-buttons';

@Component({
  selector: 'app-container',
  // specifies the template string for the pivot table component
  template: `<span><button ej-button id='save'>Save</button></span><span><button ej-button id='load'>Load</button></span><div><ejs-pivotview #pivotview id='PivotView' height='300' [dataSourceSettings]=dataSourceSettings showGroupingBar='true' ></ejs-pivotview></div>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public chartSettings: ChartSettings;
    public displayOption: DisplayOption;
    public saveButton: Button;
    public loadButton: Button;
    public layout: string;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotViewComponent;

    ngOnInit(): void {

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };

        this.saveButton = new Button({ isPrimary: true });
        this.saveButton.appendTo('#save');

        this.saveButton.element.onclick = (): void => {
            this.layout = this.pivotGridObj.getPersistData();
        };

        this.loadButton = new Button({ isPrimary: true });
        this.loadButton.appendTo('#load');

        this.loadButton.element.onclick = (): void => {
            this.pivotGridObj.loadPersistData(this.layout);
        };
    }
}

```

{% endtab %}