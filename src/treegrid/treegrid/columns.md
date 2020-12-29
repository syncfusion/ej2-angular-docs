---
title: "Columns"
component: "TreeGrid"
description: "Documentation on column reordering, resizing, header templates (custom header content), and column templates (custom cell content) in the Essential JS 2 TreeGrid control."
---

# Columns

The column definitions are used as the [`dataSource`](../api/treegrid#dataSource) schema in the TreeGrid. This plays a vital role in rendering column values in the required format.
The treegrid operations such as sorting, filtering and searching etc. are performed based on column definitions. The [`field`](../api/treegrid/column#field) property of the [`columns`](../api/treegrid#column)
is necessary to map the data source values in TreeGrid columns.

> 1. If the column [`field`](../api/treegrid/column#field) is not specified in the dataSource, the column values will be empty.
> 2. If the [`field`](../api/treegrid/column#field) name contains “dot” operator, it is considered as complex binding.

[`treeColumnIndex`](../api/treegrid#treecolumnindex) property denotes the column that is used to expand and collapse child rows.

## Header Template

You can customize the header element by using the [`headerTemplate`](../api/treegrid/column#headerTemplate) property.

{% tab template="treegrid/columns-header", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { headerData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' childMapping='subtasks' height='315' >
        <e-columns>
            <e-column field='taskName' width='170'><ng-template #headerTemplate>      <div>
        <div>
            <img src="__Task name.png" width="20" height="20" class="e-image" />  Task Name
        </div>
    </div></ng-template> </e-column>
            <e-column field='startDate'  width='130' format="yMd" textAlign='Right'></e-column>
            <e-column field='duration' headerText='Duration' width='80' textAlign='Right'> <ng-template #headerTemplate>    <div>
        <div>
            <img src="__Duration.png" width="20" height="20" class="e-image" />  Duration
        </div>
    </div></ng-template></e-column>
    <e-column field='progress' width='90' textAlign='Right'></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = headerData;
    }
}

```

{% endtab %}

### Header Template for Stacked Header column

By using the headerTemplate template reference for the ng template, you can customize a stacked header element in the Tree Grid column.

{% tab template="treegrid/columns-header", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { stackedData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' childMapping='subtasks' height='260'  [treeColumnIndex]='1' >
            <e-columns>
                <e-column headerText='Order Details'  [columns]='orderColumns'><ng-template #headerTemplate let-data > <div><a href="#">OrderColumns</a></div></ng-template> </e-column>
                <e-column headerText='Shipment Details' [columns]='shipColumns'></e-column>
                <e-column headerText='Price Details' [columns]='priceColumns'></e-column>
            </e-columns>
        </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[];
    public orderColumns: Object[];
    public shipColumns: Object[];
    public priceColumns: Object[];

    ngOnInit(): void {
        this.data = stackedData;
        this.orderColumns = [
            { field: 'orderID', headerText: 'Order ID', textAlign: 'Right', width: 90 },
            { field: 'orderName', headerText: 'Order Name', textAlign: 'Left', width: 180 },
            { field: 'orderDate', headerText: 'Order Date', textAlign: 'Right', width: 120, format: 'yMd'}
        ];
        this.shipColumns = [
            { field: 'shipMentCategory', headerText: 'Shipment Category', textAlign: 'Left', width: 150 },
            { field: 'shippedDate', headerText: 'Shipped Date', textAlign: 'Right', width: 120, format: 'yMd' },
            { field: 'units', headerText: 'Units', textAlign: 'Right', width: 90 }
        ];
        this.priceColumns = [
            { field: 'unitPrice', headerText: 'Price per unit', format: 'c2', type: 'number', width: 120, textAlign: 'Right' },
            { field: 'price', headerText: 'Total Price', width: 110, format: 'c2', type: 'number', textAlign: 'Right' }
        ];
    }
}

```

{% endtab %}

## Header text

By default, column header title is displayed from column [`field`](../api/treegrid/column#field) value. To override the default header title, you have to define the [`headerText`](../api/treegrid/column#headertext) value.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1'  childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
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

> * If both the [`field`](../api/treegrid/column#field) and [`headerText`](../api/treegrid/column#headertext)
are not defined in the column, the column renders with “empty” header text.

## Format

To format cell values based on specific culture, use the [`columns.format`](../api/treegrid/column#format) property. The TreeGrid uses [`Internalization`](../common/internationalization/) library to format [`number`](../common/internationalization/#number-formatting) and [`date`](../common/internationalization/#manipulating-datetime)
values.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { formatData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='orderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='orderName' headerText='Order Name' textAlign='Left' width=180></e-column>
                    <e-column field='price' headerText='Price' textAlign='Right' format='c2' type='number' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = formatData;
    }
}

```

{% endtab %}

> By default, the [`number`](../common/internationalization/#number-formatting) and [`date`](../common/internationalization/#manipulating-datetime) values are formatted in `en-US` locale.

### Number formatting

The number or integer values can be formatted using the below format strings.

Format |Description |Remarks
-----|-----
N | Denotes numeric type. | The numeric format is followed by integer value as N2, N3. etc which denotes the number of precision to be allowed.
C | Denotes currency type. | The currency format is followed by integer value as C2, C3. etc which denotes the number of precision to be allowed.
P | Denotes percentage type | The percentage format expects the input value to be in the range of 0 to 100. For example the cell value `0.2` is formatted as `20%`. The percentage format is followed by integer value as P2, P3. etc which denotes the number of precision to be allowed.

Please refer to the link to know more about [`Number formatting`](../common/internationalization/#number-formatting).

### Date formatting

You can format date values either using built-in date format string or custom format string.

For built-in date format you can specify [`columns.format`](../api/treegrid/column#format) property as string   (Example: `yMd`). Please refer to the link to know more about [`Date formatting`](../common/internationalization/#manipulating-datetime).

You can also use custom format string to format the date values. Some of the custom formats and the formatted date values are given in the below table.

Format | Formatted value
-----|-----
{ type:'date', format:'dd/MM/yyyy' } | 04/07/1996
{ type:'date', format:'dd.MM.yyyy' } | 04.07.1996
{ type:'date', skeleton:'short' } | 7/4/96
{ type: 'dateTime', format: 'dd/MM/yyyy hh:mm a' } | 04/07/1996 12:00 AM
{ type: 'dateTime', format: 'MM/dd/yyyy hh:mm:ss a' } | 07/04/1996 12:00:00 AM

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { formatData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='orderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='orderName' headerText='Order Name' textAlign='Left' width=180></e-column>
                    <e-column field='orderDate' headerText='Order Date' textAlign='Right'  width=160 [format]='formatoption'></e-column>
                    <e-column field='price' headerText='Price' textAlign='Right' format='c2' type='number' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public formatoption:Object;

    ngOnInit(): void {
        this.data = formatData;
        this.formatoption = { format: 'dd/MM/yyyy', type: 'date' };
    }
}

```

{% endtab %}

## AutoFit specific columns

The [`autoFitColumns`](../api/treegrid/#autofitcolumns) method resizes the column to fit the widest cell's content without wrapping. You can autofit a specific column at initial rendering by invoking the [`autoFitColumns`](../api/treegrid/#autofitcolumns) method in [`dataBound`](../api/treegrid/#databound) event.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { TreeGridComponent,ResizeService  } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='315' [allowResizing]='true' (dataBound)='onDataBound()' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=130></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`,
    providers: [ResizeService ]
})
export class AppComponent implements OnInit {

    public data: Object[];
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;

    }
    onDataBound() {
            this.treeGridObj.autoFitColumns(['taskName']);
    }
}

```

{% endtab %}

> You can autofit all the columns by invoking the [`autoFitColumns`](../api/treegrid/column#autofitcolumns) method without column names.

## Reorder

Reordering can be done by drag and drop of a particular column header from one index to another index within the treegrid. To enable reordering, set the [`allowReordering`](../api/treegrid/#allowreordering) to true.

To use reordering, inject the [`Reorder`](../api/treegrid/#reordermodule) module in the treegrid.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { ReorderService } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='315' [allowReordering]='true' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`,
    providers: [ReorderService]
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;

    }
}

```

{% endtab %}

> You can disable reordering a particular column by setting the [`columns.allowReordering`](../api/treegrid/column/#reordermodule) to false.

### Reorder Multiple Columns

Multiple columns can be reordered at a time by using the [`reorderColumns`](../api/treegrid/column#reordercolumns) method.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { TreeGridComponent,ReorderService } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<button ejs-button (click)="btnClick()">Reorder Task ID and Duration to Last</button>
    <ejs-treegrid #treegrid [dataSource]='data' height='285' [allowReordering]='true' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`,
    providers: [ReorderService]
})
export class AppComponent implements OnInit {

    public data: Object[];
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;

    }
     btnClick(e: any): any{
            this.treeGridObj.reorderColumns(['taskID','duration'],'progress');
}
}

```

{% endtab %}

## Lock Columns

You can lock columns by using `column.lockColumn` property. The locked columns will be moved to the first position. Also you can’t reorder its position.

In the below example, duration column is locked and its reordering functionality is disabled.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts,app/custom-column.style.css" %}

```typescript
import { Component, OnInit, ViewEncapsulation  } from '@angular/core';
import { sampleData } from './datasource';
import { ReorderService } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='285' [allowReordering]='true' [allowSelection]='false' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80 [lockColumn]= 'true' [customAttributes]='customAttributes'></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`,
                providers: [ReorderService],
                encapsulation: ViewEncapsulation.None,
                styleUrls: ['app/custom-column.style.css']
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
         this.customAttributes = {class: 'customcss'};
    }
}

```

{% endtab %}

## Column resizing

Column width can be resized by clicking and dragging the right edge of the column header. While dragging, the width of the respective column will be resized immediately. Each column can be auto resized by double-clicking the right edge of the column header to fit the width of that column based on the widest cell content. To enable column resize, set the [`allowResizing`](../api/treegrid/#allowresizing) property to true.

To use the column resize, inject `Resize` module in the treegrid.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { ResizeService  } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='315' [allowResizing]='true' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`,
    providers: [ResizeService ]
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;

    }
}

```

{% endtab %}

> * You can disable resizing for a particular column by setting the [`columns.allowResizing`](../api/treegrid/column/#allowresizing) to false.
> * In RTL mode, you can click and drag the left edge of the header cell to resize the column.

### Min and max width

Column resize can be restricted between minimum and maximum width by defining the [`columns->minWidth`](../api/treegrid/column/#minwidth) and [`columns->maxWidth`](../api/treegrid/column/#maxwidth).

In the following sample, minimum and maximum width are defined for `Duration`, and `Task Name` columns.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { ResizeService  } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='315' [allowResizing]='true' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' minWidth=170 maxWidth=250 textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' minWidth=50 maxWidth=150 textAlign='Right' width=80></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`,
    providers: [ResizeService ]
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;

    }
}

```

{% endtab %}

### Resize Stacked Column

Stacked columns can be resized by clicking and dragging the right edge of the stacked column header. While dragging, the width of the respective child columns will be resized at the same time. You can disable resize for particular stacked column by setting `allowResizing` as `false` to its columns.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { stackedData } from './datasource';
import { ResizeService  } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' childMapping='subtasks' height='260' [allowResizing]='true' [treeColumnIndex]='1' >
            <e-columns>
                <e-column headerText='Order Details' [columns]='orderColumns'></e-column>
                <e-column headerText='Shipment Details' [columns]='shipColumns'></e-column>
                <e-column headerText='Price Details' [columns]='priceColumns'></e-column>
            </e-columns>
        </ejs-treegrid>`,
    providers: [ResizeService ]
})
export class AppComponent implements OnInit {

    public data: Object[];
    public orderColumns: Object[];
    public shipColumns: Object[];
    public priceColumns: Object[];

    ngOnInit(): void {
        this.data = stackedData;
        this.orderColumns = [
            { field: 'orderID', headerText: 'Order ID', textAlign: 'Right', width: 90 },
            { field: 'orderName', headerText: 'Order Name', textAlign: 'Left', width: 180 },
            { field: 'orderDate', headerText: 'Order Date', textAlign: 'Right', width: 120, format: 'yMd'}
        ];
        this.shipColumns = [
            { field: 'shipMentCategory', headerText: 'Shipment Category', textAlign: 'Left', width: 150 },
            { field: 'shippedDate', headerText: 'Shipped Date', textAlign: 'Right', width: 120, format: 'yMd' },
            { field: 'units', headerText: 'Units', textAlign: 'Right', width: 90 }
        ];
        this.priceColumns = [
            { field: 'unitPrice', headerText: 'Price per unit', format: 'c2', type: 'number', width: 120, textAlign: 'Right' },
            { field: 'price', headerText: 'Total Price', width: 110, format: 'c2', type: 'number', textAlign: 'Right' }
        ];
    }
}

```

{% endtab %}

### Touch interaction

When the right edge of the header cell is tapped, a floating handler will be visible over the right border of the column. To resize the column, tap and drag the floating handler as needed.

The following screenshot represents the column resizing in touch device.

<!-- markdownlint-disable MD033 -->
<img src="../images/column-resizing.png" alt="Touch interaction image" style="width:320px;height: 620px">
<!-- markdownlint-enable MD033 -->

## Column template

The column [`template`](../api/treegrid/column/#template) has options to display custom element instead of a field value in the column.

{% tab template="treegrid/column-template", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild,CUSTOM_ELEMENTS_SCHEMA } from '@angular/core';
import { textdata, getSparkData } from './datasource';;
import { TreeGridComponent,ResizeService} from '@syncfusion/ej2-angular-treegrid';
import { EmitType } from '@syncfusion/ej2-base';
import { Sparkline, ISparklineLoadEventArgs, SparklineTheme } from '@syncfusion/ej2-charts';
import { RowDataBoundEventArgs, getObject } from '@syncfusion/ej2-grids';
@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='315' width='auto' childMapping='Children' [treeColumnIndex]='1' >
        <e-columns>
            <e-column field='EmpID' headerText='Employee ID' width='85' ></e-column>
            <e-column field='Name' headerText='Name' width='95'></e-column>
            <e-column field='DOB' headerText='DOB' width='85' format="yMd" textAlign='Right'></e-column>
            <e-column  headerText='Tax per annum' width='90' textAlign='Center'>
                <ng-template #template let-data>
                    <ejs-sparkline id='treegridline{{data.EmployeeID}}' [dataSource]='getSparkLine(data.EmployeeID)' height='50px' width='150px' lineWidth='2' valueType='Numeric' fill='#3C78EF' (load)="sparkload($event)"></ejs-sparkline>
                </ng-template>
            </e-column>
        </e-columns>
    </ejs-treegrid>`,
    providers: [ResizeService ],
    schemas: [CUSTOM_ELEMENTS_SCHEMA]
})
export class AppComponent implements OnInit {
    public data: Object[] = [];
    public sparkData: Object[] = [];

    @ViewChild('treegrid')
    public treegrid: TreeGridComponent;

    ngOnInit(): void {
        this.data = textdata;
        this.sparkData = getSparkData('line' + getObject('EmployeeID',textdata[0]));
    }
    getSparkLine (val: number) {
        return getSparkData('line', val);
    }

     sparkload: EmitType<ISparklineLoadEventArgs> = (args: ISparklineLoadEventArgs) => {
        let theme: string = location.hash.split('/')[1];
        theme = theme ? theme : 'Material';
        args.sparkline.theme = <SparklineTheme>(theme.charAt(0).toUpperCase() + theme.slice(1));
    }
}

```

{% endtab %}

> TreeGrid actions such as editing, filtering and sorting etc. will depend upon the column [`field`](../api/treegrid/column/#field). If the [`field`](../api/treegrid/column/#field) is not specified in the
template column, the treegrid actions cannot be performed.

### Using condition template

You can render the template elements based on condition.

In the following code, checkbox is rendered based on `Approved` field value.

```html
   <e-column headerText='Approved' width='150' textAlign='Center'>
             <ng-template #template let-data>
                  <div *ngIf="data.approved; else elseblock">
                      <input type="checkbox" checked>
                  </div>
              </ng-template>
              <ng-template #elseblock><input type="checkbox"></ng-template>
        </e-column>
```

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column headerText='Approved' width='150' textAlign='Center'>
             <ng-template #template let-data>
                  <div *ngIf="data.approved; else elseblock">
                      <input type="checkbox" checked>
                  </div>
              </ng-template>
              <ng-template #elseblock><input type="checkbox"></ng-template>
        </e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
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

## Column type

Column type can be specified using the [`columns.type`](../api/treegrid/column/#type) property. It specifies the type of data the column binds.

If the [`format`](../api/treegrid/column/#format)  is defined for a column, the column uses [`type`](../api/treegrid/column/#type) to select the appropriate format option ([number](../common/internationalization/#number-formatting)
 or [date](../common/internationalization/#manipulating-datetime)).

TreeGrid column supports the following types:
* string
* number
* boolean
* date
* datetime

> If the [`type`](../api/treegrid/column/#type) is not defined, it will be determined from the first record of the [`dataSource`](../api/treegrid/column/#datasource).

## Column menu

The column menu has options to integrate features like sorting, filtering, and autofit. It will show a menu with the integrated feature when users click on multiple icon of the column. To enable column menu, you need to define the [`showColumnMenu`](../api/treegrid/#showcolumnmenu) property as true.

To use the column menu, inject the `ColumnMenu` module in the treegrid.

The default items are displayed in following table.

| Item | Description |
|-----|-----|
| `SortAscending` | Sort the current column in ascending order. |
| `SortDescending` | Sort the current column in descending order. |
| `AutoFit` | Auto fit the current column. |
| `AutoFitAll` | Auto fit all columns. |
| `Filter` | Show the filter option as given in `filterSettings.type` |

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { ResizeService,FilterService,SortService,PageService,ColumnMenuService  } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid height='315' [dataSource]='data' [allowResizing]='true' [treeColumnIndex]='1' childMapping='subtasks'  showColumnMenu="true"  [allowFiltering]="true" [allowSorting]="true" [filterSettings]="filterSettings">
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=100></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=130></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=130></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=150></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' width=150></e-column>
        </e-columns>
                </ejs-treegrid>`,
      providers: [FilterService, PageService, SortService, ResizeService, ColumnMenuService]
})
export class AppComponent implements OnInit {

    public data: Object[];
    public filterSettings: Object;
    ngOnInit(): void {
        this.data = sampleData;
         this.filterSettings = { type: 'Menu'};
    }
}


```

{% endtab %}

> * You can disable column menu for a particular column by defining the [`columns.showColumnMenu`](../api/treegrid/column/#showcolumnmenu) as false.

## Checkbox Column

To render checkboxes in existing column, you need to set [`columns.showCheckbox`] property as `true`.

It is also possible to select the rows hierarchically using checkboxes in TreeGrid by enabling [`autoCheckHierarchy`] property. When we check on any parent record checkbox then the child record checkboxes will get checked.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks' autoCheckHierarchy='true' >
        <e-columns>
                <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180 [showCheckbox]='true'></e-column>
                <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
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

> Using [`selectCheckboxes`](../api/treegrid/#selectcheckboxes) method, we can check the checkboxes by passing the desired row Indexes. When we pass the parent record index in the [`selectCheckboxes`](../api/treegrid/#selectcheckboxes) method,
all children record checkboxes for the corresponding parent record will be selected. So, there is no need to pass the child record index along with the parent record index.

## Responsive columns

You can toggle column visibility based on media queries which are defined
at the [`hideAtMedia`](../api/treegrid/column/#hideatmedia).
The [`hideAtMedia`](../api/treegrid/column/#hideatmedia) accepts valid
[Media Queries]( http://cssmediaqueries.com/what-are-css-media-queries.html ).

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' hideAtMedia='(min-width: 700px)' textAlign='Right' width=90></e-column>// column hides when browser screen width lessthan 700px;
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' hideAtMedia='(max-width: 500px)' textAlign='Right' format='yMd' width=90></e-column>// column shows when browser screen width lessthan or equalto 500px;
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
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

## Controlling TreeGrid actions

You can enable or disable treegrid action for a particular column by setting the [`allowFiltering`](../api/treegrid/column/#allowfiltering), and [`allowSorting`](../api/treegrid/column/#allowsorting) properties.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks'  [allowFiltering]="true" [allowSorting]="true">
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [allowSorting]="false" textAlign='Right' width=120></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' [allowFiltering]="false" textAlign='Right' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=120></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`,
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}

```

{% endtab %}

## Show/hide columns by external button

You can show or hide treegrid columns dynamically using external buttons by invoking the [`showColumns`](../api/treegrid/#showcolumns) or [`hideColumns`](../api/treegrid/#hidecolumns) method.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { TreeGridComponent  } from '@syncfusion/ej2-angular-treegrid';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-container',
    template: `<button id='show' ejs-button class='e-flat' (click)='show()'> Show </button>
                <button id='hide' ejs-button class='e-flat' (click)='hide()'> Hide </button>
    <ejs-treegrid #treegrid [dataSource]='data' height='285' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;
    ngOnInit(): void {
        this.data = sampleData;
    }
 show() {
        this.treeGridObj.showColumns(['Task ID', 'Duration']); //show by HeaderText
    }

    hide() {
        this.treeGridObj.hideColumns(['Task ID', 'Duration']); //hide by HeaderText
    }
}

```

{% endtab %}

## Complex data binding

You can achieve complex data binding in the treegrid by using the dot(.) operator in the [`column.field`](../api/treegrid/column/#field).

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { complexData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='assignee.firstName' headerText='Assignee' textAlign='Right' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = complexData;
    }
}

```

{% endtab %}

## ValueAccessor

The [`valueAccessor`](../api/treegrid/column/#valueaccessor) is used to access/manipulate the value of display data. You can achieve custom value formatting by using the [`valueAccessor`](../api/treegrid/column/#valueaccessor).

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { formatData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks' >
       <e-columns>
                    <e-column field='orderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='orderName' headerText='Order Name' [valueAccessor]='orderFormatter' textAlign='Left' width=180></e-column>
                    <e-column field='orderDate' headerText='Order Date' textAlign='Right'  width=160 format='yMd'></e-column>
                    <e-column field='price' headerText='Price' textAlign='Right' [valueAccessor]='currencyFormatter'  width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = formatData;
    }

 currencyFormatter(field: string, data: Object, column: Object): string {
    return '€' + data['price'];
}

 orderFormatter(field: string, data: Object, column: Object): string {
    return data[field] + '-' + data['Category'];
}
}
```

{% endtab %}

### Display array type columns

You can bind an array of objects in a column by using the [`valueAccessor`](../api/treegrid/column/#valueaccessor) property.
In this example, the name field has an array of two objects, FirstName and LastName. These two objects are joined and bound to a column using the
[`valueAccessor`](../api/treegrid/column/#valueaccessor).

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { stringData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='name' headerText='Assignee' textAlign='Right' [valueAccessor]='orderFormatter' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = stringData;
    }
 orderFormatter(field: string, data: Object, column: Object): string {
    return data[field].map(function (s: {lastName: string, firstName: string}): string {
        return s.lastName || s.firstName }).join(' ');
}
}
```

{% endtab %}

### Expression column

You can achieve the expression column by using the [`valueAccessor`](../api/treegrid/column/#valueaccessor) property.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { formatData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks' >
      <e-columns>
                    <e-column field='orderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='orderName' headerText='Order Name' textAlign='Left' width=180></e-column>
                    <e-column field='units' headerText='Units' width=120 textAlign='Right'></e-column>
                    <e-column field='unitPrice' headerText='Unit Price' width=120 textAlign='Right'></e-column>
                    <e-column field='price' headerText='Total Price' [valueAccessor]='totalPrice' width=120 format='c2' type='number' textAlign='Right'></e-column>
      </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = formatData;
    }

totalPrice(field: string, data: { units: number, Fat: number, unitprice: number }, column: Object): number {
    return data.units * data.unitPrice;
};
}
```

{% endtab %}

## How to render boolean values as checkbox

To render boolean values as checkbox in columns, you need to set [`displayAsCheckBox`](../api/treegrid/column/#displayascheckbox) property as `true`.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' childMapping='subtasks'>
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='approved' headerText='Approved' width='150' [displayAsCheckBox]="true" textAlign='Center'> </e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
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