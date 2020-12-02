---
title: "Scrolling"
component: "TreeGrid"
description: "Learn how to set width and height for TreeGrid content, display a scrollbar and make the TreeGrid responsive with a parent container."
---

# Scrolling

The scrollbar will be displayed in the treegrid when content exceeds the element [`width`](../api/treegrid/#width) or [`height`](../api/treegrid/#height). The vertical and horizontal scrollbars will be displayed based on the following criteria:

* The vertical scrollbar appears when the total height of rows present in the treegrid exceeds its element height.
* The horizontal scrollbar appears when the sum of columns width exceeds the treegrid element width.
* The [`height`](../api/treegrid/#height) and [`width`](../api/treegrid/#width) are used to set the treegrid height and width, respectively.

> The default value for [`height`](../api/treegrid/#height) and [`width`](../api/treegrid/#width) is `auto`.

## Set width and height

To specify the [`width`](../api/treegrid/#width) and [`height`](../api/treegrid/#height) of the scroller in the pixel, set the pixel value to a number.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' width='400' [treeColumnIndex]='1'  childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=110></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}

```

{% endtab %}

## Responsive with parent container

Specify the [`width`](../api/treegrid/#width) and [`height`](../api/treegrid/#height) as `100%` to make the treegrid element fill its parent container.
Setting the [`height`](../api/treegrid/#height) to `100%` requires the treegrid parent element to have explicit height.

{% tab template="treegrid/responsive", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `
    <div style="height: 350px">
        <ejs-treegrid [dataSource]='data' height='100%' width='100%' [treeColumnIndex]='1'  childMapping='subtasks' >
            <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=110></e-column>
            </e-columns>
        </ejs-treegrid>
    </div>  
    `
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}

```

{% endtab %}

## Scroll to selected row

You can scroll the treegrid content to the selected row position by using the [`rowSelected`](../api/treegrid/#rowselected) event.

{% tab template="treegrid/scroll-selection", sourceFiles="app/**/*.ts" %}

```typescript
import { RowSelectEventArgs } from '@syncfusion/ej2-treegrid';
import { Component, OnInit, ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { TreeGridComponent  } from '@syncfusion/ej2-angular-treegrid';
import { NumericTextBoxComponent } from '@syncfusion/ej2-angular-inputs';

@Component({
    selector: 'app-container',
    template: `
    <ejs-numerictextbox #numerictext  min="0" max="50" width='200' [showSpinButton]='false' format= 'N' value="0" placeHolder='Enter index to select a row' (change)='onChange($event)' ></ejs-numerictextbox>

    <ejs-treegrid #treegrid [dataSource]='data' height='260' width='100%' [treeColumnIndex]='1'  childMapping='subtasks' (rowSelected)='rowSelected($event)'[selectedRowIndex]='0'>
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=110></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }

    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;
    @ViewChild('numerictext')
    public numeric: NumericTextBoxComponent;
    onChange(): void {
        this.treeGridObj.selectRow(parseInt(this.numeric.getText(), 10));
    }

    rowSelected(args: RowSelectEventArgs) {
        let rowHeight: number = this.treeGridObj.getRows()[this.treeGridObj.getSelectedRowIndexes()[0]].scrollHeight;
        this.treeGridObj.getContent().children[0].scrollTop = rowHeight * this.treeGridObj.getSelectedRowIndexes()[0];
    }
}

```

{% endtab %}

## Frozen rows and columns

Frozen rows and columns provides an option to make rows and columns always visible in the top and left side of the treegrid while scrolling.

In this demo, the [`frozenColumns`](../../api/treegrid/#frozencolumns) is set as '2' and the [`frozenRows`](../../api/treegrid/#frozenrows)
is set as '3'. Hence, the left two columns and top three rows are frozen.

{% tab template="treegrid/frozencolumns", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { FreezeService, TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' childMapping='subtasks' [treeColumnIndex]='1' height='310' [frozenColumns]='2' [frozenRows]='3' [allowSelection]='false'>
        <e-columns>
            <e-column field='taskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='taskName' headerText='Task Name' width='230'></e-column>
            <e-column field='startDate' headerText='Start Date' width='120' format='yMd' textAlign='Right'></e-column>
            <e-column field='endDate' headerText='End Date' width='120' format='yMd' textAlign='Right'></e-column>
            <e-column field='duration' headerText='Duration' width='110' textAlign='Right'></e-column>
            <e-column field='progress' headerText='Progress' width='110' textAlign='Right'></e-column>
            <e-column field='priority' headerText='Priority' width='110'></e-column>
            <e-column field='approved' headerText='Approved' textAlign='Left' width='110'></e-column>
        </e-columns>
    </ejs-treegrid>`,
providers: [FreezeService]
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}

```

{% endtab %}

### Freeze particular columns

You can use [`isFrozen`](../api/treegrid/column/#isfrozen) property to freeze selected columns in treegrid.

In this demo, the columns with field name `taskName` and `startDate` is frozen using
the `isFrozen` property.

{% tab template="treegrid/isfrozen", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { FreezeService, TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' childMapping='subtasks' height='310' [allowSelection]='false'>
        <e-columns>
            <e-column field='taskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='taskName' headerText='Task Name' width='200' isFrozen= 'true'></e-column>
            <e-column field='startDate' headerText='Start Date' isFrozen= 'true' width='150' format='yMd' textAlign='Right'></e-column>
            <e-column field='endDate' headerText='End Date' width='150' format='yMd' textAlign='Right'></e-column>
            <e-column field='duration' headerText='Duration' width='110' textAlign='Right'></e-column>
            <e-column field='progress' headerText='Progress' width='110' textAlign='Right'></e-column>
            <e-column field='priority' headerText='Priority' width='110'></e-column>
            <e-column field='approved' headerText='Approved' textAlign='Left' width='110'></e-column>
        </e-columns>
    </ejs-treegrid>`,
providers: [FreezeService]
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}

```

{% endtab %}

### Limitations

The following features are not supported in frozen rows and columns:

* Row Template
* Detail Template
* Cell Editing