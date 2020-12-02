---
title: "Customizing Filter Dialog by using additional Parameter"
component: "TreeGrid"
description: "Learn how to customize the filter dialog in Tree Grid by using an additional Parameter."
---

# Customizing Filter Dialog by using an additional Parameter

You can customize the default settings of the components which are used in Menu filter by using params of filter property in column definition.
In the below sample, TaskID and Duration Columns are numeric columns, while opening the filter dialog you can see that NumericTextBox with spin button is displayed to change/set the filter value. Now using the params option we hide the spin button in NumericTextBox for TaskID Column.

{% tab template="treegrid/refresh", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { projectData } from './datasource';
import { TreeGridComponent, FilterService, FilterSettingsModel  } from '@syncfusion/ej2-angular-treegrid';
import { IFilter } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    providers: [ FilterService ],
    template: `<ejs-treegrid #treegridObj [dataSource]='data' idMapping='TaskID' parentIdMapping='parentID' [treeColumnIndex]='1' [height]='273' [allowFiltering]='true' [filterSettings]='filterOption'>
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='70' textAlign='Right' [filter]='filterParams'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='100' ></e-column>
            <e-column field='StartDate' headerText='Start Date' textAlign='Right' [format]='formatOptions'  width='100' ></e-column>
            <e-column field='EndDate' headerText='End Date' textAlign='Right' [format]='formatOptions' width='100'></e-column>
            <e-column field='Duration' headerText='Duration' width='90' textAlign='Right'></e-column>
            <e-column field='Priority' headerText='Priority' width='90'></e-column>
        </e-columns>
    </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[] = [];
    public formatOptions: Object;
    public filterParams: IFilter;
    public filterOption: FilterSettingsModel;

    ngOnInit(): void {
        this.data = projectData;
        this.formatOptions = { format: 'y/M/d', type: 'date' };
        this.filterOption = { type: 'Menu'};
        this.filterParams = { params: { showSpinButton: false } };
    }

```

{% endtab %}