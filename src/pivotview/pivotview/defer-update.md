---
title: "Defer Layout Update"
component: "Pivot Table"
description: "Defer update allows users to update the pivot table only on demand."
---

# Defer Layout Update

Defer layout update support allows to update the pivot table component only on demand. On enabling this feature, end user can drag-and-drop fields between row, column, value and filter axes, apply sorting and filtering inside the Field List, resulting in change of pivot report alone but not the pivot table values. Once all operations are performed and on clicking the "Apply" button in the Field List, pivot table will start to update with the last modified report. This also helps in bringing better performance in pivot table component rendering.

The field list can be displayed in two different formats to interact with pivot table. They are:

* **In-built Field List (Popup)**: To display the field list icon in pivot table UI to invoke the built-in dialog.
* **Stand-alone Field List (Fixed)**: To display the field list in a static position within a web page.

## In-built Field List (Popup)

To enable deferred updates in the pivot table, set the property [`allowDeferLayoutUpdate`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#allowdeferlayoutupdate) in pivot table as **true**. To make a note, the defer update option can be controlled only via Field List during runtime.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, IDataSet, PivotView, FieldListService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [FieldListService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings showFieldList='true' width=width allowDeferLayoutUpdate='true'></ejs-pivotview></div>`
})

export class AppComponent {

    public width: string;
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = '100%';

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            allowLabelFilter: true,
            allowValueFilter: true,
            enableSorting: true,
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

## Stand-alone Field List (Fixed)

The field list can be rendered in a static position, anywhere in web page layout, like a separate component. To do so, you need to set [`renderMode`](https://ej2.syncfusion.com/angular/documentation/api/pivotfieldlist#rendermode) property to **Fixed** in pivot fieldlist.

To enable deferred updates in the static fieldlist, set the property [`allowDeferLayoutUpdate`](https://ej2.syncfusion.com/angular/documentation/api/pivotfieldlist#allowdeferlayoutupdate) in fieldlist as **true**. To make a note, the defer update option can be controlled only via Field List during runtime.

> To make field list interact with pivot table, you need to use the **UpdateView** and **Update** methods for data source update in both field list and pivot table simultaneously.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { PivotFieldListComponent, PivotViewComponent, FieldListService, IDataOptions, IDataSet,
    EnginePopulatedEventArgs } from '@syncfusion/ej2-angular-pivotview';
import { Browser, setStyleAttribute, prepend } from '@syncfusion/ej2-base';
import { GridSettings } from '@syncfusion/ej2-pivotview/src/pivotview/model/gridsettings';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [FieldListService],
  styleUrls: ['app/app.component.css'],
  // specifies the template string for the pivot table component
  template: `<ejs-pivotfieldlist #pivotfieldlist id='PivotFieldList' [dataSourceSettings]=dataSourceSettings renderMode="Fixed" (enginePopulated)='afterPopulate($event)' allowDeferLayoutUpdate='true' allowCalculatedField='true' (load)='onLoad()' (dataBound)='ondataBound()'></ejs-pivotfieldlist><ejs-pivotview #pivotview id='PivotViewFieldList' allowDeferLayoutUpdate='true' width='99%' height='530' (enginePopulated)='afterEnginePopulate($event)' [gridSettings]='gridSettings'></ejs-pivotview>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public gridSettings: GridSettings;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotViewComponent;

    @ViewChild('pivotfieldlist')
    public fieldlistObj: PivotFieldListComponent;

    afterPopulate(arge: EnginePopulatedEventArgs): void {
        if (this.fieldlistObj.isRequiredUpdate) {
            this.fieldlistObj.updateView(this.pivotGridObj);
        }
        this.pivotGridObj.notify('ui-update', this.pivotGridObj);
        this.fieldlistObj.notify('tree-view-update', this.fieldlistObj);
    }
    afterEnginePopulate(args: EnginePopulatedEventArgs): void {
        if (this.fieldlistObj && this.pivotGridObj) {
            this.fieldlistObj.update(this.pivotGridObj);
        }
    }
    onLoad(): void {
        if (Browser.isDevice) {
            this.fieldlistObj.renderMode = 'Popup';
            this.fieldlistObj.target = '.control-section';
            document.getElementById('PivotFieldList').removeAttribute('style');
            setStyleAttribute(document.getElementById('PivotFieldList'), {
                'height': 0,
                'float': 'left'
            });
        }
    }

    ondataBound(): void {
        if (Browser.isDevice) {
            prepend([document.getElementById('PivotFieldList')], document.getElementById('PivotView'));
        }
    }

    ngOnInit(): void {

        this.gridSettings = {
            columnWidth: 140
        } as GridSettings;

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
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