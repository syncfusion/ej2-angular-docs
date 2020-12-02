---
title: "Toolbar"
component: "Pivot Table"
description: "Learn how to use the toolbar and customize toolbar items in the Essential JS 2 pivot table control."
---

# Toolbar

Toolbar option allows to access the frequently used features like switching between pivot table and pivot chart, changing chart types, conditional formatting, exporting, etc... with ease at runtime. This option can be enabled by setting the [`showToolbar`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#showtoolbar) property in pivot table to **true**. The [`toolbar`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#toolbar) property in pivot table accepts the collection of built-in toolbar options.

The following table shows built-in toolbar options and its actions.

| Built-in Toolbar Options | Actions |
|------------------------|---------|
| New | Creates a new report |
| Save | Saves the current report |
| Save As | Save as current report |
| Rename | Renames the current report |
| Delete | Deletes the current report |
| Load | Loads any report from the report list |
| Grid | Shows pivot table |
| Chart | Shows a chart in any type from the built-in list and option to enable/disable multiple axes |
| Exporting | Exports the pivot table as PDF/Excel/CSV and the pivot chart as PDF and image |
| Sub-total | Shows or hides sub totals |
| Grand Total | Shows or hides grand totals |
| Conditional Formatting | Shows the conditional formatting pop-up to apply formatting |
| Number Formatting | Shows the number formatting pop-up to apply number formatting |
| Field List | Shows the fieldlist pop-up |
| MDX | Shows the MDX query that was run to retrieve data from the OLAP data source. **NOTE: This applies only to the OLAP data source.** |

> The order of toolbar options can be changed by simply moving the position of items in the **ToolbarItems** collection. Also if end user wants to remove any toolbar option from getting displayed, it can be simply ignored from adding into the **ToolbarItems** collection.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import {
    IDataOptions, PivotView, FieldListService, CalculatedFieldService, NumberFormattingService,
    ToolbarService, ConditionalFormattingService, ToolbarItems, DisplayOption, IDataSet
} from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [CalculatedFieldService, ToolbarService, ConditionalFormattingService, FieldListService, NumberFormattingService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings allowExcelExport='true' allowNumberFormatting='true' allowConditionalFormatting='true' allowPdfExport='true' showToolbar='true' allowCalculatedField='true' showFieldList='true' width='100%' [displayOption]='displayOption' height='350' [toolbar]='toolbarOptions' (saveReport)='saveReport($event)' (loadReport)='loadReport($event)' (fetchReport)='fetchReport($event)' (renameReport)='renameReport($event)' (removeReport)='removeReport($event)' (newReport)='newReport()'></ejs-pivotview></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public toolbarOptions: ToolbarItems[];
    public displayOption: DisplayOption;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;

    saveReport(args: any) {
        let reports = [];
        let isSaved: boolean = false;
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reports = JSON.parse(localStorage.pivotviewReports);
        }
        if (args.report && args.reportName && args.reportName !== '') {
            reports.map(function (item: any): any {
                if (args.reportName === item.reportName) {
                    item.report = args.report; isSaved = true;
                }
            });
            if (!isSaved) {
                reports.push(args);
            }
            localStorage.pivotviewReports = JSON.stringify(reports);
        }
    }
    fetchReport(args: any) {
        let reportCollection: string[] = [];
        let reeportList: string[] = [];
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reportCollection = JSON.parse(localStorage.pivotviewReports);
        }
        reportCollection.map(function (item: any): void { reeportList.push(item.reportName); });
        args.reportName = reeportList;
    }
    loadReport(args: any) {
        let reportCollection: string[] = [];
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reportCollection = JSON.parse(localStorage.pivotviewReports);
        }
        reportCollection.map(function (item: any): void {
            if (args.reportName === item.reportName) {
                args.report = item.report;
            }
        });
        if (args.report) {
            this.pivotGridObj.dataSourceSettings = JSON.parse(args.report).dataSourceSettings;
        }
    }
    removeReport(args: any) {
        let reportCollection: any[] = [];
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reportCollection = JSON.parse(localStorage.pivotviewReports);
        }
        for (let i: number = 0; i < reportCollection.length; i++) {
            if (reportCollection[i].reportName === args.reportName) {
                reportCollection.splice(i, 1);
            }
        }
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            localStorage.pivotviewReports = JSON.stringify(reportCollection);
        }
    }
    renameReport(args: any) {
        let reportCollection: string[] = [];
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reportCollection = JSON.parse(localStorage.pivotviewReports);
        }
        reportCollection.map(function (item: any): any { if (args.reportName === item.reportName) { item.reportName = args.rename; } });
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            localStorage.pivotviewReports = JSON.stringify(reportCollection);
        }
    }
    newReport() {
        this.pivotGridObj.setProperties({ dataSourceSettings: { columns: [], rows: [], values: [], filters: [] } }, false);
    }
    ngOnInit(): void {
        this.displayOption = { view: 'Both' } as DisplayOption;

        this.toolbarOptions = ['New', 'Save', 'SaveAs', 'Rename', 'Remove', 'Load',
            'Grid', 'Chart', 'Export', 'SubTotal', 'GrandTotal', 'ConditionalFormatting', 'NumberFormatting', 'FieldList'] as ToolbarItems[];
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
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

## Show desired chart types in the dropdown menu

By default, all chart types are displayed in the dropdown menu included in the toolbar. However, based on the request for an application, we may need to show selective chart types on our own. This can be achieved using the [`chartTypes`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#charttypes) property. To know more about supporting chart types, [`click here`](https://ej2.syncfusion.com/angular/documentation/pivotview/pivot-chart/#chart-types).

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { IDataOptions, PivotView, ToolbarService, ToolbarItems, DisplayOption, IDataSet, ChartTypeOptions
} from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [ ToolbarService ],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings showToolbar='true' width='100%' [displayOption]='displayOption' height='350' [toolbar]='toolbarOptions' [chartTypes]= 'chartTypeOptions'></ejs-pivotview></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public toolbarOptions: ToolbarItems[];
    public displayOption: DisplayOption;
    public chartTypeOptions: ChartTypeOptions[];

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;

    ngOnInit(): void {
        this.displayOption = { view: 'Both' } as DisplayOption;
        this.chartTypeOptions = ['Column', 'Bar', 'Line', 'Area'] as ChartTypeOptions[];
        this.toolbarOptions = [ 'Grid','Chart' ] as ToolbarItems[];
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            enableSorting: true,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
        };
    }
 }
```

{% endtab %}

## Switch the chart to multiple axes

In the chart, the user can switch from single axis to multiple axes with the help of the built-in checkbox available inside the chart type dropdown menu in the toolbar. For more information [`refer here`](https://ej2.syncfusion.com/angular/documentation/pivotview/pivot-chart/#multi-axis).

![output](images/chart-option.png)

<!-- markdownlint-disable MD009 -->

## Show or hide legend

In the chart, legend can be shown or hidden dynamically with the help of the built-in option available in the chart type drop-down menu.
> By default, the legend is not be visible for the accumulation chart types like pie, doughnut, pyramid, and funnel. Users can enable or disable using the built-in checkbox option.

![output](images/chart-legend.png)

## Adding custom option to the toolbar

In addition to the existing built-in toolbar items, new toolbar item(s) may also be included. This can be achieved by using the [`toolbarRender`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#toolbarrender) event. The action of the new toolbar item(s) can also be defined within this event. 

> The new toolbar item(s) can be added to the desired position in the toolbar using the `splice` option.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts,app/app.component.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import {
    IDataOptions, PivotView, ToolbarService, ToolbarItems, DisplayOption, IDataSet
} from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [ToolbarService],
  // specifies the template string for the pivot table component
  template: `<div><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings  showToolbar='true' width='100%' [displayOption]='displayOption' height='350' [toolbar]='toolbarOptions' (toolbarRender)='beforeToolbarRender($event)'></ejs-pivotview></div>`,
  styleUrls: ['app/app.component.css'],
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public toolbarOptions: ToolbarItems[];
    public displayOption: DisplayOption;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;

    beforeToolbarRender(args: any) {
        args.customToolbar.splice(12, 0, {
                prefixIcon: 'e-tool-expand e-icons', tooltipText: 'Expand/Collapse',
                click: this.toolbarClicked.bind(this),
        });
    }
    toolbarClicked(args: any) {
         this.pivotGridObj.dataSourceSettings.expandAll = !this.pivotGridObj.dataSourceSettings.expandAll;
    }
    ngOnInit(): void {
        this.displayOption = { view: 'Both' } as DisplayOption;

        this.toolbarOptions = ['Expand/Collapse'] as ToolbarItems[];

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
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

In the above topic, we have seen how to add an icon as one of the toolbar item in toolbar panel. In the next topic, we are going to see how to frame the entire toolbar panel and how to add a custom control in it.

### Toolbar Template

It allows to customize the toolbar panel by using template option. It allows any custom control to be used as one of the toolbar item inside the toolbar panel. It can be achieved by two ways,

Here, the entire toolbar panel can be framed in HTML elements that are appended at the top of the pivot table. The **id** of the HTML element needs to be set in the [`toolbarTemplate`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#toolbartemplate) property in-order to map it to the pivot table.

{% tab template="pivot-grid/toolbarTemplate", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    IDataOptions, PivotView, FieldListService, CalculatedFieldService,
    ToolbarService, ConditionalFormattingService, IDataSet,
    NumberFormattingService
} from '@syncfusion/ej2-angular-pivotview';
import { GridSettings } from '@syncfusion/ej2-pivotview/src/pivotview/model/gridsettings';
import { enableRipple } from '@syncfusion/ej2-base';
import { Pivot_Data } from './datasource.ts';
import { Button } from '@syncfusion/ej2-buttons';
enableRipple(false);

@Component({
  selector: 'app-container',
  providers: [ToolbarService],
  // specifies the template string for the pivot table component
  template: `<div class="control-section" id="pivot-table-section">
    <div>
        <ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings  showToolbar='true' width='100%' height='450' [gridSettings]='gridSettings' [toolbarTemplate]='toolbarOptions'> </ejs-pivotview>
    </div>
    <div id='template'>
        <div> 
            <div><button ejs-button id='expandall' class="e-flat" (click)="enablertl()">Expand All</button></div>
                <div><button ejs-button id='collapseall'  class="e-flat" (click)="disableRtl()">Collapse All</button></div>
    </div>
</div></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public gridSettings: GridSettings;
    public toolbarOptions: string;
    public btnExpand: Button;
    public btnCollapse: Button;

    @ViewChild('pivotview')
    public pivotObj: PivotView;

       enablertl() {
              this.pivotObj.dataSourceSettings.expandAll=true;
        };

         disableRtl(){
              this.pivotObj.dataSourceSettings.expandAll=false;
        };

    ngOnInit(): void {
        this.gridSettings = {
            columnWidth: 140
        } as GridSettings;

        this.toolbarOptions = '#template';

        this.dataSourceSettings = {
            enableSorting: true,
            columns: [{ name: 'Year' }, { name: 'Order_Source', caption: 'Order Source' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            dataSource: Pivot_Data,
            expandAll: false,
            values: [{ name: 'Sold', caption: 'Units Sold' },
            { name: 'Amount', caption: 'Sold Amount' }],
            filters: [{ name: 'Product_Categories', caption: 'Product Categories' }]
        };
        this.btnExpand = new Button({ isPrimary: true });
        this.btnExpand.appendTo('#expandall');
        this.btnCollapse = new Button({ isPrimary: true });
        this.btnCollapse.appendTo('#collapseall');
    }
 }
```

{% endtab %}

Another option allows to frame a custom toolbar item using HTML elements and include in the toolbar panel at the desired position. The custom toolbar items can be declared as control **instance** or element **id** in the [`toolbar`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#toolbar) property in pivot table.

{% tab template="pivot-grid/toolbarTemplate", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    IDataOptions, PivotView, 
    ToolbarService,  IDataSet } from '@syncfusion/ej2-angular-pivotview';
import { GridSettings } from '@syncfusion/ej2-pivotview/src/pivotview/model/gridsettings';
import { enableRipple } from '@syncfusion/ej2-base';
import { Pivot_Data } from './datasource.ts';
enableRipple(false);

@Component({
  selector: 'app-container',
  providers: [ToolbarService],
  // specifies the template string for the pivot table component
  template: `<div class="control-section" id="pivot-table-section">
  <div>
    <ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings  showToolbar='true' width='100%' height='450' [gridSettings]='gridSettings' [toolbar]='toolbarOptions'> </ejs-pivotview>
    </div>
    <ng-template #btnenablertl let-data>
    <button ejs-button id='enablertl' class="e-flat" isPrimary="true" (click)="enablertl()">Enable Rtl</button>
    </ng-template>
    <ng-template #btndisablertl let-data>
    <button ejs-button id='disablertl' class="e-flat" isPrimary="true" (click)="disableRtl()">Disable Rtl</button>
    </ng-template></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public gridSettings: GridSettings;
    public toolbarOptions: any;

    @ViewChild('btnenablertl', {static:true})
    public enableRtl: any;
    @ViewChild('btndisablertl', {static:true})
    public disableRTL: any;
    @ViewChild('pivotview')
    public pivotObj: PivotView;

       enablertl() {
              this.pivotObj.enableRtl=true;
        };

         disableRtl(){
              this.pivotObj.enableRtl=false;
        };

    ngOnInit(): void {
        this.gridSettings = {
            columnWidth: 140
        } as GridSettings;

        this.toolbarOptions = [{template: this.enableRtl},{template: this.disableRTL}] as any;

        this.dataSourceSettings = {
            enableSorting: true,
            columns: [{ name: 'Year' }, { name: 'Order_Source', caption: 'Order Source' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            dataSource: Pivot_Data,
            expandAll: false,
            values: [{ name: 'Sold', caption: 'Units Sold' },
            { name: 'Amount', caption: 'Sold Amount' }],
            filters: [{ name: 'Product_Categories', caption: 'Product Categories' }]
        };
    }
 }
```

{% endtab %}

>Note: For both options, the actions for the toolbar template items can be defined in the event [`toolbarClick`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#toolbarclick). Also, if the toolbar item is a custom control then its built-in events can also be accessed.

<!-- markdownlint-disable MD009 -->

## Save and load report as a JSON file 

The current pivot report can be saved as a JSON file in the desired path and loaded back to the pivot table at any time.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { IDataOptions, IDataSet, PivotView, FieldListService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';
import { Button } from '@syncfusion/ej2-buttons';

@Component({
  selector: 'app-container',
  providers: [FieldListService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [width]=width showFieldList='true' (dataBound)='ondataBound($event)'></ejs-pivotview></div><a id="save" class="btn btn-primary">Save</a><div class="fileUpload btn btn-primary"><span>Load</span><input id="files" type="file" class="upload" /></div>`,
  styleUrls: ['app/app.component.css'],
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public button: Button;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;

    ondataBound(args: any) {
       var dataSource = JSON.parse(this.pivotGridObj.getPersistData()).dataSourceSettings.dataSource;
        var a = document.getElementById('save');
        var mime_type = 'application/octet-stream'; // text/html, image/png, et c
        a.setAttribute('download', 'pivot.JSON');
        a.href = 'data:'+ mime_type +';base64,'+ btoa(JSON.stringify(dataSource) || '');
        document.getElementById('files').addEventListener('change', this.readBlob, false);
    }

    readBlob(args: any) {
        var files = document.getElementById('load').files;
        var file = files[0];
        var start = 0;
        var stop = file.size - 1;
        var reader = new FileReader();
        reader.onloadend = function(evt) {
            if (evt.target.readyState == FileReader.DONE) {
                this.pivotGridObj.dataSource = JSON.parse(evt.target.result);
            }
        };
        var blob = file.slice(start, stop + 1);
        reader.readAsBinaryString(blob);
    }

    ngOnInit(): void {
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };
        this.width = "100%";
    }
 }
```

{% endtab %}

## Events

### FetchReport

The event [`fetchReport`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#fetchreport) is triggered when dropdown list is clicked in the toolbar in-order to retrieve and populate saved reports. It has following parameter - `reportName`. This event allows user to fetch the report names from local storage and populate the dropdown list.

### LoadReport

The event [`loadReport`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#loadreport) is triggered when a report is selected from the dropdown list in the toolbar. It has following parameters - `report` and `reportName`. This event allows user to load the selected report to the pivot table.

### NewReport

The event [`newReport`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#newreport) is triggered when the new report icon is clicked in the toolbar. It has following parameter - `report`. This event allows user to create new report and add to the report list.

### RenameReport

The event [`renameReport`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#renamereport) is triggered when rename report icon is clicked in the toolbar. It has following parameters  - `rename`, `report` and `reportName`. This event allows user to rename the selected report from the report list.

### RemoveReport

The event [`removeReport`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#removereport) is triggered when remove report icon is clicked in the toolbar. It has following parameters  - `report` and `reportName`. This event allows user to remove the selected report from the report list.

### SaveReport

The event [`saveReport`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#savereport) is triggered when save report icon is clicked in the toolbar. It has following parameters  - `report` and `reportName`. This event allows user to save the altered report to the report list.

<!-- markdownlint-disable MD009 -->

### ToolbarRender 

The [`toolbarRender`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#toolbarrender) event is triggered when the toolbar is rendered. It has the `customToolbar` parameter. This event helps to customize the built-in toolbar items and to [`include new toolbar item(s)`](https://ej2.syncfusion.com/angular/documentation/pivotview/tool-bar/#adding-custom-option-to-the-toolbar).

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts,app/app.component.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import {
    IDataOptions, PivotView, ToolbarService, ToolbarItems, DisplayOption, IDataSet, FieldListService
} from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [ToolbarService, FieldListService],
  // specifies the template string for the pivot table component
  template: `<div><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings  showToolbar='true' showFieldList='true' width='100%' [displayOption]='displayOption' height='350' [toolbar]='toolbarOptions' (toolbarRender)='beforeToolbarRender($event)' (saveReport)='saveReport($event)'></ejs-pivotview></div>`,
  styleUrls: ['app/app.component.css'],
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public toolbarOptions: ToolbarItems[];
    public displayOption: DisplayOption;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;

    saveReport(args: any) {
        let reports = [];
        let isSaved: boolean = false;
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reports = JSON.parse(localStorage.pivotviewReports);
        }
        if (args.report && args.reportName && args.reportName !== '') {
            reports.map(function (item: any): any {
                if (args.reportName === item.reportName) {
                    item.report = args.report; isSaved = true;
                }
            });
            if (!isSaved) {
                reports.push(args);
            }
            localStorage.pivotviewReports = JSON.stringify(reports);
        }
    }

    beforeToolbarRender(args: any) {
        args.customToolbar.splice(2, 0, {
            prefixIcon: 'e-rename-report e-icons', tooltipText: 'Custom Button',
            click: this.customButton.bind(this),
        });
        args.customToolbar.splice(3, 0, {
            prefixIcon: 'e-tool-expand e-icons', tooltipText: 'Expand/Collapse',
            click: this.toolbarClicked.bind(this),
        });
        args.customToolbar[0].align = "Left";
        args.customToolbar[1].align = "Center";
        args.customToolbar[2].align = "Right";
    }
    customButton(args: any) {
        // Here you can customize the click event for custom button
    }
    toolbarClicked(args: any) {
         this.pivotGridObj.dataSourceSettings.expandAll = !this.pivotGridObj.dataSourceSettings.expandAll;
    }
    ngOnInit(): void {
        this.displayOption = { view: 'Both' } as DisplayOption;

        this.toolbarOptions = ['Save', 'Export', 'FieldList'] as ToolbarItems[];

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
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

### BeforeExport

The pivot table (or) pivot chart can be exported as a pdf, excel, csv etc.,  document using the toolbar options. And, you can customize the export settings for exporting document by using the [`beforeExport`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#beforeexport) event in the toolbar.

For example, you can add the header and footer for the pdf document by setting the `header` and `footer` properties for the `pdfExportProperties` in the [`beforeExport`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#beforeexport) event.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import {
    IDataOptions, PivotView, FieldListService, CalculatedFieldService,
    ToolbarService, ConditionalFormattingService, ToolbarItems, DisplayOption, IDataSet
} from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [CalculatedFieldService, ToolbarService, ConditionalFormattingService, FieldListService],
  // specifies the template string for the pivot table component
  template: `<div><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings allowExcelExport='true' allowConditionalFormatting='true' allowPdfExport='true' showToolbar='true' allowCalculatedField='true' showFieldList='true' width='100%' [displayOption]='displayOption' height='350' [toolbar]='toolbarOptions' (saveReport)='saveReport($event)' (loadReport)='loadReport($event)' (fetchReport)='fetchReport($event)' (renameReport)='renameReport($event)' (removeReport)='removeReport($event)' (newReport)='newReport()' (beforeExport)='beforeExport($event)'></ejs-pivotview></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    public toolbarOptions: ToolbarItems[];
    public displayOption: DisplayOption;

    @ViewChild('pivotview', {static: false})
    public pivotGridObj: PivotView;

    saveReport(args: any) {
        let reports = [];
        let isSaved: boolean = false;
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reports = JSON.parse(localStorage.pivotviewReports);
        }
        if (args.report && args.reportName && args.reportName !== '') {
            reports.map(function (item: any): any {
                if (args.reportName === item.reportName) {
                    item.report = args.report; isSaved = true;
                }
            });
            if (!isSaved) {
                reports.push(args);
            }
            localStorage.pivotviewReports = JSON.stringify(reports);
        }
    }
    fetchReport(args: any) {
        let reportCollection: string[] = [];
        let reeportList: string[] = [];
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reportCollection = JSON.parse(localStorage.pivotviewReports);
        }
        reportCollection.map(function (item: any): void { reeportList.push(item.reportName); });
        args.reportName = reeportList;
    }
    loadReport(args: any) {
        let reportCollection: string[] = [];
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reportCollection = JSON.parse(localStorage.pivotviewReports);
        }
        reportCollection.map(function (item: any): void {
            if (args.reportName === item.reportName) {
                args.report = item.report;
            }
        });
        if (args.report) {
            this.pivotGridObj.dataSourceSettings = JSON.parse(args.report).dataSourceSettings;
        }
    }
    removeReport(args: any) {
        let reportCollection: any[] = [];
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reportCollection = JSON.parse(localStorage.pivotviewReports);
        }
        for (let i: number = 0; i < reportCollection.length; i++) {
            if (reportCollection[i].reportName === args.reportName) {
                reportCollection.splice(i, 1);
            }
        }
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            localStorage.pivotviewReports = JSON.stringify(reportCollection);
        }
    }
    renameReport(args: any) {
        let reportCollection: string[] = [];
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            reportCollection = JSON.parse(localStorage.pivotviewReports);
        }
        reportCollection.map(function (item: any): any { if (args.reportName === item.reportName) { item.reportName = args.rename; } });
        if (localStorage.pivotviewReports && localStorage.pivotviewReports !== "") {
            localStorage.pivotviewReports = JSON.stringify(reportCollection);
        }
    }
    newReport() {
        this.pivotGridObj.setProperties({ dataSourceSettings: { columns: [], rows: [], values: [], filters: [] } }, false);
    }
    beforeExport(args: any): void {
            args.excelExportProperties = {
                header: {
                    headerRows: 2,
                    rows: [
                        { cells: [{ colSpan: 4, value: "Pivot Table", style: { fontColor: '#C67878', fontSize: 20, hAlign: 'Center', bold: true, underline: true } }] }
                    ]
                },
                footer: {
                    footerRows: 4,
                    rows: [
                        { cells: [{ colSpan: 4, value: "Thank you for your business!", style: { hAlign: 'Center', bold: true } }] },
                        { cells: [{ colSpan: 4, value: "!Visit Again!", style: { hAlign: 'Center', bold: true } }] }
                    ]
                }
            };
            args.pdfExportProperties = {
                header: {
                    fromTop: 0,
                    height: 130,
                    contents: [
                        {
                            type: 'Text',
                            value: "Pivot Table",
                            position: { x: 0, y: 50 },
                            style: { textBrushColor: '#000000', fontSize: 13, dashStyle:'Solid',hAlign:'Center' }
                        }
                    ]
                },
                footer: {
                    fromBottom: 160,
                    height: 150,
                    contents: [
                        {
                            type: 'PageNumber',
                            pageNumberType: 'Arabic',
                            format: 'Page {$current} of {$total}',
                            position: { x: 0, y: 25 },
                            style: { textBrushColor: '#02007a', fontSize: 15 }
                        }
                    ]
                }
            };
        }
    ngOnInit(): void {
        this.displayOption = { view: 'Both' } as DisplayOption;

        this.toolbarOptions = ['New', 'Save', 'SaveAs', 'Rename', 'Remove', 'Load',
            'Grid', 'Chart', 'Export', 'SubTotal', 'GrandTotal', 'ConditionalFormatting', 'FieldList'] as ToolbarItems[];
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
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

## See Also

* [Toolbar Component](../../toolbar/getting-started/)