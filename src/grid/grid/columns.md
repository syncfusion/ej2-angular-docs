---
title: "Columns"
component: "Grid"
description: "Documentation on column reordering, resizing, header templates (custom header content), and column templates (custom cell content) in the Essential JS 2 DataGrid control."
---

# Columns

The column definitions are used as the **dataSource** schema in the Grid.
This plays a vital role in rendering column values in the required format.
The grid operations such as sorting, filtering and grouping etc. are performed based on column definitions.
The [`field`](../api/grid/column/#field) property of the [`columns`](../api/grid/column)
is necessary to map the data source values in Grid columns.

> 1. If the column with [`field`](../api/grid/column/#field) is not in the dataSource, then the column values will be displayed as empty.
> 2. If the [`field`](../api/grid/column/#field) name contains “dot” operator then it is considered as complex binding.

## Auto generation

The [`columns`](../api/grid/column) are automatically generated when
[`columns`](../api/grid/column)
declaration is empty or undefined while initializing the grid. All the columns in the **dataSource** are bound as grid columns.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data'>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = [
            { OrderID: 10248, CustomerID: 'VINET', EmployeeID: 5 },
            { OrderID: 10249, CustomerID: 'TOMSP', EmployeeID: 6 },
            { OrderID: 10250, CustomerID: 'HANAR', EmployeeID: 4 }];
    }
}

```

{% endtab %}

> When the columns are auto-generated then the column [`type`](../api/grid/column/#type)
will be determined from the first record of the
[`dataSource`](../api/grid/#datasource).

### Set Primary key column for auto generated columns when editing is enabled

Primary key can be defined in the declaration of column object of the grid. When we didn't declare the columns, the grid will generate the columns automatically. For these auto generated columns, you can set [`isPrimaryKey`](../api/grid/column/#isprimarykey) column property as true by using the following ways,

If Primary key "column index" is known then refer the following code example

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { GridComponent, EditSettingsModel, EditService } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [editSettings]='editSettings' (dataBound)="dataBound($event)">
               </ejs-grid>`,
    providers: [EditService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = [
            { OrderID: 10248, CustomerID: 'VINET', EmployeeID: 5 },
            { OrderID: 10249, CustomerID: 'TOMSP', EmployeeID: 6 },
            { OrderID: 10250, CustomerID: 'HANAR', EmployeeID: 4 }];
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
    }

    dataBound(args: any) {
        (this.grid.columns[0] as any).isPrimaryKey = 'true';
    }
}

```

{% endtab %}

If Primary key **column** and its **field** is known then primary key for the respective [`column`](https://ej2.syncfusion.com/documentation/api/grid/column/) can be defined as follows.

```typescript

  const column: ColumnModel = this.grid.getColumnByField('OrderID');
  column.isPrimaryKey = true;

```

### Set column options to auto generated columns

You can set column options such as [`format`](../api/grid/column/#format), [`width`](../api/grid/column/#width) to the auto generated columns by using [`dataBound`](../api/grid/#databound) event of the grid.

In the below example, [`width`](../api/grid/column/#width) is set for **OrderID** column, **date** type is set for **OrderDate** column and [`format`](../api/grid/column/#format) is set for **Freight** and **OrderDate** column.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' (dataBound)="dataBound($event)">
               </ejs-grid>`
})
export class AppComponent implements OnInit {
    public data: object[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = [
            { OrderID: 10248, CustomerID: 'VINET', Freight: 32.3800, OrderDate: '1996-07-02T00:00:00.000Z' },
            { OrderID: 10249, CustomerID: 'TOMSP', Freight: 32.3800, OrderDate: '1996-07-19T00:00:00.000Z' },
            { OrderID: 10250, CustomerID: 'HANAR', Freight: 32.3800, OrderDate: '1996-07-22T00:00:00.000Z' }];
    }

    dataBound(args: any) {
        for (const cols of this.grid.columns) {
            if ((cols as any).field === 'OrderID') {
                (cols as any).width = 120;
            }
            if ((cols as any).field === 'OrderDate') {
                (cols as any).type = 'date';
                (cols as any).format = 'yMd';
            }
            if ((cols as any).field === 'Freight') {
                (cols as any).format = 'P2';
            }
        }
        this.grid.refreshColumns();
    }
}

```

{% endtab %}

## Complex Data Binding

You can achieve complex data binding in the grid by using the dot(.) operator in the [`column.field`](../api/grid/column/#field).

{% tab template="grid/grid", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { complexData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='Name.FirstName' headerText='First Name' width=120></e-column>
                        <e-column field='Name.LastName' headerText='Last Name' width=120></e-column>
                        <e-column field='Title' headerText='Title' width=150></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = complexData;
    }
}

```

{% endtab %}

 For OData and ODataV4 adaptors, you need to add [`expand`](https://ej2.syncfusion.com/documentation/api/data/query/#expand) query to the [`query`](../api/grid/#query) property (of Grid), to eager load the complex data.

 ```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, ODataAdaptor, Query } from '@syncfusion/ej2-data';
import { employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' allowPaging='true' [query]='query' [height]='315'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130 ></e-column>
                        <e-column field='Employee.City' headerText='City' width=130  ></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {
    public employeeData: object[];
    public data: DataManager = new DataManager({
        adaptor: new ODataAdaptor(),
        crossDomain: true,
        url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders'
      });
      public query = new Query().expand('Employee');

    ngOnInit(): void {
        this.employeeData = employeeData;
    }
}

```

## Foreign Key Column

Foreign key column can be enabled by using [`column.dataSource`](../api/grid/column/#datasource),
[`column.foreignKeyField`](../api/grid/column/#foreignkeyfield) and
[`column.foreignKeyValue`](../api/grid/column/#foreignkeyvalue) properties.

* [`column.dataSource`](../api/grid/column/#datasource) - Defines the foreign data.
* [`column.foreignKeyField`](../api/grid/column/#foreignkeyfield) - Defines the mapping column name to the foreign data.
* [`column.foreignKeyValue`](../api/grid/column/#foreignkeyvalue) - Defines the display field from the foreign data.

In the following example, **Employee Name** is a foreign column which shows **FirstName** column from foreign data.

To use ForeignKeyColumn, you need to inject **ForeignKeyService** in the provider section of **AppModule**.

{% tab template="grid/grid", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { ForeignKeyService } from '@syncfusion/ej2-angular-grids';
import { data, employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='EmployeeID' headerText='Employee Name' width=120
                        foreignKeyValue='FirstName' [dataSource]='employeeData'></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130  ></e-column>
                    </e-columns>
                </ejs-grid>`,
    providers: [ForeignKeyService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public employeeData: object[];

    ngOnInit(): void {
        this.data = data;
        this.employeeData = employeeData;
    }
}

```

{% endtab %}

> * For remote data, the sorting and grouping is done based on [`column.foreignKeyField`](../api/grid/column/#foreignkeyfield) instead of
[`column.foreignKeyValue`](../api/grid/column/#foreignkeyvalue).
> * If [`column.foreignKeyField`](../api/grid/column/#foreignkeyfield) is not defined, then the column uses [`column.field`](../api/grid/column/#field).

## Header Template

You can customize the header element by using the [`headerTemplate`](../api/grid/column/#headertemplate) property. In this demo, the custom element is rendered for both CustomerID and OrderDate column headers.

{% tab template="grid/header-template", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=140>
                        <ng-template #headerTemplate let-data>
                            <div>
                            <span class="e-icon-userlogin e-icons employee"></span> Customer ID
                            </div>
                        </ng-template>
                    </e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C' width=120></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=140>
                        <ng-template #headerTemplate let-data>
                            <div>
                                <span class="e-icon-calender e-icons headericon"></span> Order Date
                            </div>
                        </ng-template>
                    </e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

## Header Text

By default, column header title is displayed from column [`field`](../api/grid/column/#field) value.
To override the default header title by defining [`headerText`](../api/grid/column/#headertext) value.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=140></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C' width=120></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=140></e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

> If both the [`field`](../api/grid/column/#field) and [`headerText`](../api/grid/column/#headertext)
are not defined in the column, the column renders with “empty” header text.

## Format

To format cell values based on specific culture, use the [`columns.format`](../api/grid/column/#format)
property. The grid uses [`Internalization`](../common/internationalization/) library to format [`number`](../common/internationalization/#number-formatting) and
[`date`](../common/internationalization/#manipulating-datetime)
values.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height="315px">
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}
```

{% endtab %}

> By default, the [`number`](../common/internationalization/#number-formatting) and [`date`](../common/internationalization/#manipulating-datetime) values are formatted in **en-US** locale. You can localize the currency and date in different locale as explained ['here'](../common/internationalization/)

### Number formatting

The number or integer values can be formatted using the below format strings.

Format |Description |Remarks
-----|-----|-----
N | Denotes numeric type. | The numeric format is followed by integer value as N2, N3. etc which denotes the number of precision to be allowed.
C | Denotes currency type. | The currency format is followed by integer value as C2, C3. etc which denotes the number of precision to be allowed.
P | Denotes percentage type | The percentage format expects the input value to be in the range of 0 to 1. For example the cell value **0.2** is formatted as **20%**. The percentage format is followed by integer value as P2, P3. etc which denotes the number of precision to be allowed.

Please refer to the link to know more about [`number`](../common/internationalization/#number-formatting) format.

### Date formatting

You can format date values either using built-in date format string or custom format string.

For built-in date format you can specify [`columns.format`](../api/grid/column/#format) as string   (Example: **yMd**). Please refer to the link to know more about [`Date formatting`](../common/internationalization/#manipulating-datetime)

You can also use custom format string to format the date values. Some of the custom formats and the formatted date values are given in the below table.

Format | Formatted value
-----|-----
{ type:'date', format:'dd/MM/yyyy' } | 04/07/1996
{ type:'date', format:'dd.MM.yyyy' } | 04.07.1996
{ type:'date', skeleton:'short' } | 7/4/96
{ type: 'dateTime', format: 'dd/MM/yyyy hh:mm a' } | 04/07/1996 12:00 AM
{ type: 'dateTime', format: 'MM/dd/yyyy hh:mm:ss a' } | 07/04/1996 12:00:00 AM

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height="315px">
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                    <e-column field='OrderDate' [format]='formatOptions' headerText='Order Date' textAlign='Right' width=120></e-column>
                    <e-column field='OrderDate' [format]='shipFormat' headerText='Ship Date' textAlign='Right' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public formatOptions: object;
    public shipFormat: object;

    ngOnInit(): void {
        this.data = data;
        this.formatOptions = {type: 'date', format: 'dd/MM/yyyy'};
        this.shipFormat = { type: 'dateTime', format: 'dd/MM/yyyy hh:mm a' };
    }
}

```

{% endtab %}

## Visibility

You can hide any particular column in Grid before rendering by defining [`visible`](../api/grid/column/#visible) property as false. In the below sample **ShipCity** column is defined as visible false.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=140></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C' width=120></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=140></e-column>
                    <e-column field='ShipCity' headerText='Ship City' [visible]='false' width=100></e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {
    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

## AutoFit specific columns

The [`autoFitColumns`](../api/grid/#autofitcolumns) method resizes the column to fit the widest
cell's content without wrapping. You can autofit specific columns at initial rendering by invoking
the [`autoFitColumns`](../api/grid/#autofitcolumns) method in [`dataBound`](../api/grid/#databound) event.

To use autofit feature, you need to inject **ResizeService** in the provider section of **AppModule**.

{% tab template="grid/resize", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
selector: 'app-root',
template: `<ejs-grid #grid [dataSource]='data' height='315px' (dataBound)='dataBound()' >
<e-columns>
<e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
<e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
<e-column field='ShipName' headerText='Ship Name' width=80></e-column>
<e-column field='ShipAddress' headerText='Ship Address' width=120></e-column>
<e-column field='ShipCity' headerText='Ship City' width=100></e-column>
</e-columns>
</ejs-grid>`
})
export class AppComponent implements OnInit {

public data: object[];
@ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }
    dataBound() {
        this.grid.autoFitColumns(['ShipAddress', 'ShipName']);
    }
}

```

{% endtab %}

> You can autofit all columns, by invoking the [`autoFitColumns`](../api/grid/#autofitcolumns)
method without column name.

## Reorder

Reordering can be done by drag and drop of a particular column header from one index to another index within the grid.
To enable reordering, set the [`allowReordering`](../api/grid/#allowreordering) to true.

To use Reordering, you need to inject **ReorderService** in the provider section of **AppModule**.

{% tab template="grid/reorder", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowReordering]='true' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=100></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=80></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

> You can disable reordering a particular column by setting the [`columns.allowReordering`](../api/grid/column/#allowreordering) to false.

### Reorder Single Columns

Grid have option to reorder Columns either by Interaction or by using the [`reorderColumns`](../api/grid/#reordercolumns) method. In the below sample, **ShipCity** column is reordered to last column position by using the method.

{% tab template="grid/reorder", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-root',
    template:
    `<button ej-button id='reorderSingleCol' (click)='reorderSingleCol()'>Reorder Ship City to Last</button>
    <ejs-grid #grid='' [dataSource]='data' [allowReordering]='true' height='280px'>
        <e-columns>
            <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
            <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
            <e-column field='ShipCity' headerText='Ship City' width=100></e-column>
            <e-column field='ShipRegion' headerText='Ship Region' width=100></e-column>
            <e-column field='ShipName' headerText='Ship Name' width=120></e-column>
        </e-columns>
    </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    @ViewChild('grid')
    public gridObj: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }

    reorderSingleCol(): void {
        this.gridObj.reorderColumns('ShipCity','ShipName');
    }
}
```

{% endtab %}

### Reorder Multiple Columns

User can reorder a single column at a time by Interaction. Sometimes we need to have reorder multiple columns at the same time, It can be achieved through programmatically by using [`reorderColumns`](../api/grid/#reordercolumns) method.

In the below sample, **Ship City** and **Ship Region** column is reordered to last column position.

{% tab template="grid/reorder", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template:
    `<button ej-button id='reorderMultipleCols' (click)='reorderMultipleCols()'>Reorder Ship City and Ship Region to Last</button>
    <ejs-grid #grid='' [dataSource]='data' [allowReordering]='true' height='280px'>
        <e-columns>
            <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
            <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
            <e-column field='ShipCity' headerText='Ship City' width=100></e-column>
            <e-column field='ShipRegion' headerText='Ship Region' width=100></e-column>
            <e-column field='ShipName' headerText='Ship Name' width=120></e-column>
        </e-columns>
    </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public gridObj: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }

    reorderMultipleCols(): void {
        this.gridObj.reorderColumns(['ShipCity', 'ShipRegion'], 'ShipName');
    }
}

```

{% endtab %}

### Reorder Events

During the reorder action, the grid component triggers the below three events.

1. The [`columnDragStart`](../api/grid/#columndragstart) event triggers when column header element drag (move) starts.
2. The [`columnDrag`](../api/grid/#columndrag) event triggers when column header element is dragged (moved) continuously.
3. The [`columnDrop`](../api/grid/#columndrop) event triggers when a column header element is dropped on the target column.

{% tab template="grid/reorder", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template:
        `<ejs-grid #grid [dataSource]='data' [allowReordering]='true' height='280px'
         (columnDragStart)="columnDragStart()" (columnDrag)="columnDrag()" (columnDrop)="columnDrop()">
        <e-columns>
            <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
            <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
            <e-column field='ShipCity' headerText='Ship City' width=100></e-column>
            <e-column field='ShipRegion' headerText='Ship Region' width=100></e-column>
            <e-column field='ShipName' headerText='Ship Name' width=120></e-column>
        </e-columns>
    </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public gridObj: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }

    columnDrop() {
        alert('columnDrop event is Triggered');
    }
    columnDragStart() {
        alert('columnDragStart event is Triggered');
    }
    columnDrag() {
        alert('columnDrag event is Triggered');
    }
}

```

{% endtab %}

## Lock Columns

You can lock columns by using [`column.lockColumn`](../api/grid/column/#lockcolumn) property. The locked columns will be moved to the first position. Also you can’t reorder its position.

In the below example, Ship City column is locked and its reordering functionality is disabled.

{% tab template="grid/reorder", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowReordering]='true' [allowSelection]='false' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCity' width=100 [lockColumn]='true' [customAttributes]='customAttributes'></e-column>
                    <e-column field='ShipName'width=100></e-column>
                    <e-column field='ShipPostalCode'width=80></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public customAttributes: object;

    ngOnInit(): void {
        this.data = data;
        this.customAttributes = {class: 'customcss'};
    }
}

```

{% endtab %}

## Column Resizing

Columns width can be resized by clicking and dragging at the right edge of the column header.
While dragging, the width of a respective column will be resized immediately.
Each column can be auto resized by double-clicking at the right edge of the column header.
It will fit the width of that column based on widest cell content.
To enable the column resize, set the [`allowResizing`](../api/grid/#allowresizing) property to true.

To use the column resize, inject **ResizeService** in the provider section of **AppModule**.

{% tab template="grid/resize", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowResizing]='true' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=100></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=80></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' textAlign='Right' width=100></e-column>
                    <e-column field='ShipAddress' headerText='Ship Address' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' width=80></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

> You can disable Resizing for a particular column,
by specifying [`columns.allowResizing`](../api/grid/columnDirective/#allowresizing) to false.
> In RTL mode, you can click and drag the left edge of header cell to resize the column.

### Min and Max width

Columns can be restricted to resize in between minimum and maximum width by defining the
[`columns.minWidth`](../api/grid/columnDirective/#minwidth) and [`columns.maxWidth`](../api/grid/columnDirective/#maxwidth).

In the below sample, **OrderID**, **Ship Name** and **Ship Country** columns are defined with minimum and maximum width.

{% tab template="grid/resize", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowResizing]='true' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' minWidth= 100 width=150 maxWidth=250 ></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=100></e-column>
                    <e-column field='ShipName' headerText='Ship Name'  minWidth= 150 width=200 maxWidth=300></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' textAlign='Right'  minWidth= 120 width=150 maxWidth=280></e-column>
                    <e-column field='ShipAddress' headerText='Ship Address' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' width=80></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

### Resize Stacked Column

Stacked columns can be resized by clicking and dragging the right edge of the stacked column header. While dragging, the width of the respective child columns will be resized at the same time. You can disable resize for any particular stacked column by setting [`allowResizing`](../api/grid/columnDirective/#allowresizing) as **false** to its columns.

In this example, we have disabled resize for **Ship City** column.

{% tab template="grid/resize", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { ColumnModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowResizing]='true' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' width='100' textAlign="Center" minWidth=10></e-column>
                    <e-column headerText='Order Details' [columns]='orderColumns'></e-column>
                    <e-column headerText='Ship Details' [columns]='shipColumns'></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public orderColumns: ColumnModel[];
    public shipColumns: ColumnModel[];


    ngOnInit(): void {
        this.data = data;
        this.orderColumns = [
            {
                field: 'OrderDate',
                headerText: 'Order Date',
                format: 'yMd',
                width: 120,
                textAlign: 'Right',
                minWidth: 10
            },
            {
                field: 'Freight',
                headerText: 'Freight ($)',
                width: 100,
                format: 'C1',
                textAlign: 'Right',
                minWidth: 10
            }
        ];

        this.shipColumns = [
            {
                field: 'ShipCity',
                headerText: 'Ship City',
                width: 100,
                minWidth: 10
            },
            {
                field: 'ShipCountry',
                headerText: 'Ship Country',
                width: 120,
                minWidth: 10
            }
        ];
    }
}

```

{% endtab %}

### Touch Interaction

When you tap at the right edge of header cell, a floating handler will be visible over the right border of the column.
To resize the column, tap and drag the floating handler as much you need. You can also autoFit a column by using the Column menu of the grid.

The following screenshot represents the column resizing on the touch device.

![Touch Interaction](images/column-resizing.jpg)

### Resizing Events

During the resizing action, the grid component triggers the below three events.

1. The [`resizeStart`](../api/grid/#resizestart) event triggers when column resize starts.
2. The [`resizing`](../api/grid/#resizing) event triggers when column header element is dragged (moved) continuously..
3. The [`resizeStop`](../api/grid/#resizestop) event triggers when column resize ends.

{% tab template="grid/resize", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowResizing]='true' height='315px' (resizeStart)="resizeStart()"
               (resizing)="resizing()" (resizeStop)="resizeStop()">
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=100></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=80></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' textAlign='Right' width=100></e-column>
                    <e-column field='ShipAddress' headerText='Ship Address' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' width=80></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }

    resizing() {
        alert('resizing event is Triggered');
    }
    resizeStop() {
        alert('resizeStop event is Triggered');
    }
    resizeStart() {
        alert('resizeStart event is Triggered');
    }
}

```

{% endtab %}

## Column Type

Column type can be specified using the [`columns.type`](../api/grid/column/#type) property. It specifies the type of data the column binds.

If the [`format`](../api/grid/column/#format)  is defined for a column,
the column uses [`type`](../api/grid/column/#type) to select the appropriate format option ([number](../common/internationalization/#number-formatting)
 or [date](../common/internationalization/#manipulating-datetime)).

Grid column supports the following types:
* string
* number
* boolean
* date
* datetime

> If the [`type`](../api/grid/column/#type) is not defined, then it will be determined from the first record of the [`dataSource`](../api/grid/#datasource).
> Incase if the first record of the [`dataSource`](../api/grid/#datasource) is null/blank value for a column then it is necessary to define the [`type`](../api/grid/column/#type) for that column.

## Column template

The column [`template`](../api/grid/column/#template) has options to display custom element instead of a field value in the column.

{% tab template="grid/template", sourceFiles="app/app.component.ts,app/app.module.ts, app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height='315px'>
                    <e-columns>
                        <e-column headerText='Employee Image' width='150' textAlign='Center'>
                            <ng-template #template let-data>
                                <div class="image">
                             <img src="https://ej2.syncfusion.com/angular/demos/src/grid/images/{{data.EmployeeID}}.png" alt="{{data.EmployeeID}}"/>
                                </div>
                            </ng-template>
                        </e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>`,
    styleUrls: ['./app/app.style.css']
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = employeeData;
    }
}


```

{% endtab %}

### Using condition template

You can render the template elements based on condition.

In the following code, checkbox is rendered based on **Discontinued** field value.

```html
  <e-column headerText='Discontinued' width='150' textAlign='Center'>
             <ng-template #template let-data>
                  <div *ngIf="data.Discontinued; else elseblock">
                      <input type="checkbox" checked>
                  </div>
              </ng-template>
              <ng-template #elseblock><input type="checkbox"></ng-template>
        </e-column>
```

{% tab template="grid/condition-template", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { categoryData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height='315px'>
                    <e-columns>
                        <e-column headerText='Discontinued' width='150' textAlign='Center'>
                          <ng-template #template let-data>
                            <div *ngIf="data.Discontinued; else elseblock">
                                 <input type="checkbox" checked>
                            </div>
                          </ng-template>
                          <ng-template #elseblock><input type="checkbox"></ng-template>
                       </e-column>
                        <e-column field='ProductID' headerText='Product ID' width=150></e-column>
                        <e-column field='CategoryName' headerText='Category Name' width=150></e-column>
                        <e-column field='ProductName' headerText='Product Name' width=150></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = categoryData;
    }
}

```

{% endtab %}

## Column chooser

The column chooser has options to show or hide columns dynamically. It can be enabled by defining the
[`showColumnChooser`](../api/grid/#showcolumnchooser) as true.

To use column chooser, inject **ColumnChooserService** in the provider section of **AppModule**.

{% tab template="grid/columnchooser", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { ToolbarItems } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [toolbar]='toolbarOptions' height='272px' [showColumnChooser]= 'true'>
               <e-columns>
                    <e-column field='OrderID' headerText='Order ID' width='120' textAlign="Right"></e-column>
                    <e-column field='CustomerName' headerText='Customer Name' width='150' [showInColumnChooser]='false'></e-column>
                    <e-column field='OrderDate' headerText='Order Date' width='130' format="yMd" textAlign="Right"></e-column>
                    <e-column field='Freight' headerText='Freight' width='120' format='C2' textAlign="Right"></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' [visible]='false' width='150'></e-column>
                    <e-column field='ShipCity' headerText='Ship City' [visible]='false' width='150'></e-column>
               </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbarOptions: ToolbarItems[];

    ngOnInit(): void {
        this.data = data;
        this.toolbarOptions = ['ColumnChooser'];
    }
}


```

{% endtab %}

> You can hide the column names in column chooser by defining the
[`columns.showInColumnChooser`](../api/grid/column/#showincolumnchooser) as false.

### Open column chooser by external button

The Column chooser can be displayed on a page through external button by invoking
the [`openColumnChooser`](../api/grid/columnChooser/#opencolumnchooser) method with **X** and **Y** axis positions.

{% tab template="grid/columnschooser-method", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: ` <button id='show' ej-button class='e-flat' (click)='show()'> open Column Chooser </button>
                <ejs-grid #grid [dataSource]='data' [height]='280' [showColumnChooser]= 'true'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' width='120' textAlign="Right"></e-column>
                        <e-column field='CustomerName' headerText='Customer Name' width='150' [showInColumnChooser]='false'></e-column>
                        <e-column field='OrderDate' headerText='Order Date' width='130' format="yMd" textAlign="right"></e-column>
                        <e-column field='Freight' headerText='Freight' width='120' format='C2' textAlign="Right"></e-column>
                        <e-column field='ShipCountry' headerText='Ship Country' [visible]='false' width='150'></e-column>
                        <e-column field='ShipCity' headerText='Ship City' [visible]='false' width='150'></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }

    show() {
        this.grid.columnChooserModule.openColumnChooser(200, 50); // give X and Y axis
    }
}

```

{% endtab %}

## Column menu

The column menu has options to integrate features like sorting, grouping, filtering, column chooser, and autofit.
It will show a menu with the integrated feature when users click on multiple icon of the column.
To enable column menu, you need to define the [`showColumnMenu`](../api/grid/#showcolumnmenu) property as true.

To use the column menu, inject the **ColumnMenuService** in the provider section of **AppModule**.

The default items are displayed in following table.

| Item | Description |
|-----|-----|
| **SortAscending** | Sort the current column in ascending order. |
| **SortDescending** | Sort the current column in descending order. |
| **Group** | Group the current column. |
| **Ungroup** | Ungroup the current column. |
| **AutoFit** | Auto fit the current column. |
| **AutoFitAll** | Auto fit all columns. |
| **ColumnChooser** | Choose the column visibility. |
| **Filter** | Show the filter option as given in [`filterSettings.type`](../api/grid/filterSettings/#type) |

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript


import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SortService, GroupService, ColumnMenuService, PageService, FilterService } from '@syncfusion/ej2-angular-grids';
import {  GroupSettingsModel, FilterSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' id="gridcomp" allowPaging='true' allowGrouping='true' allowSorting='true' showColumnMenu='true'
        [groupSettings]='groupOptions' allowFiltering='true' [filterSettings]='filterSettings'>
        <e-columns>
            <e-column field='OrderID' headerText='Order ID' width='140' textAlign="Right"></e-column>
            <e-column field='CustomerID' headerText='Customer Name'></e-column>
            <e-column field='Freight' headerText='Freight' format='C2' textAlign="Right"></e-column>
            <e-column field='ShipCountry' headerText='Ship Country' [visible]='false' width='150'></e-column>
            <e-column field='ShipCity' headerText='Ship City' width='150'></e-column>
        </e-columns>
    </ejs-grid>
                `,
    providers: [SortService, GroupService, ColumnMenuService, PageService, FilterService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public groupOptions: GroupSettingsModel;
    public filterSettings: FilterSettingsModel;
    ngOnInit(): void {
        this.data = data;
        this.groupOptions = { showGroupedColumn: true };
        this.filterSettings = { type: 'CheckBox' };
    }
}

```

{% endtab %}

> You can disable column menu for a particular column by defining the
[`columns.showColumnMenu`](../api/grid/column/#showcolumnmenu) as false.
> You can customize the default items by defining the
[`columnMenuItems`](../api/grid/#columnmenuitems) with required items.

### Column menu events

During the resizing action, the grid component triggers the below two events.

1. The [`columnMenuOpen`](../api/grid/#columnmenuopen) event triggers before the column menu opens.
2. The [`columnMenuClick`](../api/grid/#columnmenuclick) event triggers when the user clicks the column menu of the grid.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { SortService, GroupService, ColumnMenuService, PageService, FilterService } from '@syncfusion/ej2-angular-grids';
import { GroupSettingsModel, FilterSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' id="gridcomp" allowPaging='true' allowGrouping='true' allowSorting='true' showColumnMenu='true'
               [groupSettings]='groupOptions' allowFiltering='true' [filterSettings]='filterSettings'
         (columnMenuOpen)="columnMenuOpen()" (columnMenuClick)="columnMenuClick()">
        <e-columns>
            <e-column field='OrderID' headerText='Order ID' width='140' textAlign="Right"></e-column>
            <e-column field='CustomerID' headerText='Customer Name'></e-column>
            <e-column field='Freight' headerText='Freight' format='C2' textAlign="Right"></e-column>
            <e-column field='ShipCountry' headerText='Ship Country' [visible]='false' width='150'></e-column>
            <e-column field='ShipCity' headerText='Ship City' width='150'></e-column>
        </e-columns>
    </ejs-grid>
                `,
    providers: [SortService, GroupService, ColumnMenuService, PageService, FilterService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public groupOptions: GroupSettingsModel;
    public filterSettings: FilterSettingsModel;
    ngOnInit(): void {
        this.data = data;
        this.groupOptions = { showGroupedColumn: true };
        this.filterSettings = { type: 'CheckBox' };
    }
    columnMenuOpen() {
        alert('columnMenuOpen event is Triggered');
    }
    columnMenuClick() {
        alert('columnMenuClick event is Triggered');
    }
}

```

{% endtab %}

### Custom Column Menu Item

Custom column menu items can be added by defining the
[`columnMenuItems`](../api/grid/#columnmenuitems) as collection of
the [`columnMenuItemModel`](../api/grid/columnMenuItemModel/).
Actions for this customized items can be defined in the
[`columnMenuClick`](../api/grid/#columnmenuclick) event.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, SortService, ColumnMenuService, PageService } from '@syncfusion/ej2-angular-grids';
import { MenuEventArgs } from '@syncfusion/ej2-navigations';
import { SortSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' id="gridcomp" allowPaging='true' allowSorting='true'
     showColumnMenu='true' [sortSettings]='sortSettings' [columnMenuItems]='columnMenuItems' (columnMenuClick)='columnMenuClick($event)'>
        <e-columns>
            <e-column field='OrderID' headerText='Order ID' width='140' textAlign="Right"></e-column>
            <e-column field='CustomerID' headerText='Customer Name' showInColumnChooser='false'></e-column>
            <e-column field='Freight' headerText='Freight' format='C2' textAlign="Right"></e-column>
            <e-column field='ShipCountry' headerText='Ship Country' [visible]='false' width='150'></e-column>
            <e-column field='ShipCity' headerText='Ship City' width='150'></e-column>
        </e-columns>
    </ejs-grid>
                `,
    providers: [SortService, ColumnMenuService, PageService]
})
export class AppComponent implements OnInit {

    @ViewChild('grid')
    public grid: GridComponent;
    public data: object[];
    public columnMenuItems: any = [{ text: 'Clear Sorting', id: 'gridclearsorting' }];
    public sortSettings: SortSettingsModel =  {columns: [{direction: 'Ascending', field: 'OrderID'}]};
    public columnMenuClick(args: MenuEventArgs) {
        if (args.item.id === 'gridclearsorting') {
            this.grid.clearSorting();
        }
    }
    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

### Customize menu items for particular columns

Sometimes, you have a scenario that to hide an item from column menu for particular columns. In that case, you need to define the
[`columnMenuOpenEventArgs.hide`](../api/grid/columnMenuOpenEventArgs) as true in the
[`columnMenuOpen`](../api/grid/#columnmenuopen) event.

The following sample, **Filter** item was hidden in column menu when opens for the **OrderID** column.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent, SortService, GroupService, ColumnMenuService, PageService, FilterService } from '@syncfusion/ej2-angular-grids';
import { ColumnMenuItemModel, ColumnMenuOpenEventArgs, FilterSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' id="gridcomp" allowPaging='true' allowSorting='true' showColumnMenu='true'
     [filterSettings]='filterSettings' (columnMenuOpen)='columnMenuOpen($event)' [allowFiltering]='true' [allowGrouping]='true'>
        <e-columns>
            <e-column field='OrderID' headerText='Order ID' width='140' textAlign="Right"></e-column>
            <e-column field='CustomerID' headerText='Customer Name' showInColumnChooser='false'></e-column>
            <e-column field='Freight' headerText='Freight' format='C2' textAlign="Right"></e-column>
            <e-column field='ShipCountry' headerText='Ship Country' [visible]='false' width='150'></e-column>
            <e-column field='ShipCity' headerText='Ship City' width='150'></e-column>
        </e-columns>
    </ejs-grid>
                `,
    providers: [SortService, ColumnMenuService, PageService, GroupService, ColumnMenuService, FilterService]
})
export class AppComponent implements OnInit {

    @ViewChild('grid')
    public grid: GridComponent;
    public data: object[];
    public filterSettings: FilterSettingsModel = { type: 'Menu' };
    public columnMenuOpen(args: ColumnMenuOpenEventArgs) {
        for (const item of args.items) {
            if (item.text === 'Filter' && args.column.field === 'OrderID') {
                (item as ColumnMenuItemModel).hide = true;
            } else {
                (item as ColumnMenuItemModel).hide = false;
            }
        }
    }

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

## Column Spanning

The grid has option to span the adjacent cells. You need to define the
[`colSpan`](../api/grid/queryCellInfoEventArgs/#colspan) attribute to span cells in the
[`QueryCellInfo`](../api/grid/queryCellInfoEventArgs) event.

In the following demo, Employee **Davolio** doing analysis from 9.00 AM to 10.00 AM, so that cells have spanned.

{% tab template="grid/spanning", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { QueryCellInfoEventArgs, GridLine } from '@syncfusion/ej2-angular-grids';
import { columnSpanData, ColumnSpanDataType } from './datasource';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [height]='height' [width]='width' [gridLines]='gridLines'
     [allowTextWrap]='textWrap' (queryCellInfo)='queryCellInfoEvent($event)'>
        <e-columns>
            <e-column field='EmployeeID' headerText='Employee ID' width='150' textAlign="Right" isPrimaryKey=true></e-column>
            <e-column field='EmployeeName' headerText='Employee Name' width='200'></e-column>
            <e-column field='9:00' headerText='9:00 AM' width='120'></e-column>
            <e-column field='9:30' headerText='9:30 AM' width='120'></e-column>
            <e-column field='10:00' headerText='10:00 AM' width='120'></e-column>
            <e-column field='10:30' headerText='10:30 AM' width='120'></e-column>
            <e-column field='11:00' headerText='11:00 AM' width='120'></e-column>
            <e-column field='11:30' headerText='11:30 AM' width='120'></e-column>
            <e-column field='12:00' headerText='12:00 PM' width='120'></e-column>
            <e-column field='12:30' headerText='12:30 PM' width='120'></e-column>
            <e-column field='2:30' headerText='2:30 PM' width='120'></e-column>
            <e-column field='3:00' headerText='3:00 PM' width='120'></e-column>
            <e-column field='3:30' headerText='3:30 PM' width='120'></e-column>
            <e-column field='4:00' headerText='4:00 PM' width='120'></e-column>
            <e-column field='4:30' headerText='4:30 PM' width='120'></e-column>
            <e-column field='5:00' headerText='5:00 PM' width='120'></e-column>
        </e-columns>
    </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public height: string | number;
    public width: string | number;
    public gridLines: GridLine;
    public textWrap: boolean;
    public queryCellInfoEvent: EmitType<QueryCellInfoEventArgs> = (args: QueryCellInfoEventArgs) => {
        const data: ColumnSpanDataType = args.data as ColumnSpanDataType;
        switch (data.EmployeeID) {
            case 10001:
                if (args.column.field === '9:00' || args.column.field === '2:30' || args.column.field === '4:30') {
                    args.colSpan = 2;
                } else if (args.column.field === '11:00') {
                    args.colSpan = 3;
                }
                break;
            case 10002:
                if (args.column.field === '9:30' || args.column.field === '2:30' ||
                    args.column.field === '4:30') {
                    args.colSpan = 3;
                } else if (args.column.field === '11:00') {
                    args.colSpan = 4;
                }
                break;
            case 10003:
                if (args.column.field === '9:00' || args.column.field === '11:30') {
                    args.colSpan = 3;
                } else if (args.column.field === '10:30' || args.column.field === '3:30' ||
                    args.column.field === '4:30' || args.column.field === '2:30') {
                    args.colSpan = 2;
                }
                break;
            case 10004:
                if (args.column.field === '9:00') {
                    args.colSpan = 3;
                } else if (args.column.field === '11:00') {
                    args.colSpan = 4;
                } else if (args.column.field === '4:00' || args.column.field === '2:30') {
                    args.colSpan = 2;
                }
                break;
            case 10005:
                if (args.column.field === '9:00') {
                    args.colSpan = 4;
                } else if (args.column.field === '11:30') {
                    args.colSpan = 3;
                } else if (args.column.field === '3:30' || args.column.field === '4:30' || args.column.field === '2:30') {
                    args.colSpan = 2;
                }
                break;
            case 10006:
                if (args.column.field === '9:00' || args.column.field === '4:30' ||
                    args.column.field === '2:30' || args.column.field === '3:30') {
                    args.colSpan = 2;
                } else if (args.column.field === '10:00' || args.column.field === '11:30') {
                    args.colSpan = 3;
                }
                break;
            case 10007:
                if (args.column.field === '9:00' || args.column.field === '3:00' || args.column.field === '10:30') {
                    args.colSpan = 2;
                } else if (args.column.field === '11:30' || args.column.field === '4:00') {
                    args.colSpan = 3;
                }
                break;
            case 10008:
                if (args.column.field === '9:00' || args.column.field === '10:30' || args.column.field === '2:30') {
                    args.colSpan = 3;
                } else if (args.column.field === '4:00') {
                    args.colSpan = 2;
                }
                break;
            case 10009:
                if (args.column.field === '9:00' || args.column.field === '11:30') {
                    args.colSpan = 3;
                } else if (args.column.field === '4:30' || args.column.field === '2:30') {
                    args.colSpan = 2;
                }
                break;
            case 100010:
                if (args.column.field === '9:00' || args.column.field === '2:30' ||
                    args.column.field === '4:00' || args.column.field === '11:30') {
                    args.colSpan = 3;
                } else if (args.column.field === '10:30') {
                    args.colSpan = 2;
                }
                break;
        }
    }
    ngOnInit(): void {
        this.data = columnSpanData;
        this.gridLines = 'Both';
        this.height = 'auto';
        this.width = 'auto';
        this.textWrap = true;
    }
}

```

{% endtab %}

## Responsive columns

You can toggle column visibility based on media queries which are defined
at the [`hideAtMedia`](../api/grid/column/#hideatmedia).
The [`hideAtMedia`](../api/grid/column/#hideatmedia) accepts valid
[Media Queries]( http://cssmediaqueries.com/what-are-css-media-queries.html ). In the below sample, for **OrderID** column, [`hideAtMedia`](../api/grid/column/#hideatmedia) property value is set as **(min-width: 700px)** so that **OrderID** column will gets hidden when the browser screen width is lessthan 700px.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120 hideAtMedia='(min-width: 700px)'>
                    </e-column> //  column visibility hide when browser screen width lessthan 700px;
                    <e-column field='CustomerID' headerText='Customer ID' width=140 hideAtMedia='(max-width: 700px)'>
                    </e-column> // column Visibility show when browser screen width  500px or less;
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C' width=120
                    hideAtMedia='(min-width: 500px)'>
                    </e-column> // column visibility hide when browser screen width lessthan 500px;
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=140>
                    </e-column> // it always shown
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

## Controlling Grid Actions

You can enable or disable grid action for a particular column by setting the [`allowFiltering`](../api/grid/columnModel/#allowfiltering),
[`allowGrouping`](../api/grid/columnModel/#allowgrouping), [`allowSorting`](../api/grid/columnModel/#allowsorting), [`allowReordering`](../api/grid/columnModel/#allowreordering) and [`allowEditing`](../api/grid/columnModel/#allowediting) properties.

{% tab template="grid/control-actions", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, IEditCell, ReorderService, EditService } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [allowReordering]="true" [editSettings]='editSettings'
               [allowSorting]="true" [allowFiltering]="true" [allowGrouping]="true" height="220px">
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90 [allowGrouping]="false"></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right'
                     format='C2' width=90 [allowFiltering]="false"></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right'
                     format='yMd' width=120 [allowSorting]="false"></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
    }
}

```

{% endtab %}

## Show/Hide Columns by External Button

You can show or hide the grid columns dynamically through external buttons by invoking the [`showColumns`](../api/grid/#showcolumns)/[`hideColumns`](../api/grid/#hidecolumns)
methods.

{% tab template="grid/grid", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: ` <button id='show' ej-button class='e-flat' (click)='show()'> Show </button>
                <button id='hide' ej-button class='e-flat' (click)='hide()'> Hide </button>
                <ejs-grid #grid [dataSource]='data' [height]='280'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=90></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=90></e-column>
                        <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=120></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }

    show() {
        this.grid.showColumns(['Customer ID', 'Ship Name']); // show by HeaderText
    }

    hide() {
        this.grid.hideColumns(['Customer ID', 'Ship Name']); // hide by HeaderText
    }
}

```

{% endtab %}

## ValueAccessor

The [`valueAccessor`](../api/grid/column/#valueaccessor) is used to access/manipulate the value of display data.
You can achieve custom value formatting by using [`valueAccessor`](../api/grid/column/#valueaccessor).

{% tab template="grid/grid", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right'
                         [valueAccessor]='currencyFormatter' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130 [valueAccessor]='valueAccess' ></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public currencyFormatter = (field: string, data1: object, column: object) => {
        const Freight = 'Freight';
        return '€' + data1[Freight];
    }

    public valueAccess = (field: string, data1: object, column: object) => {
        const ShipRegion = 'ShipRegion';
        return data1[field] + '-' + data1[ShipRegion];
    }

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

### Display Array type Columns

You can bind an Array of Objects in a column by using [`valueAccessor`](../api/grid/column/#valueaccessor) property.
In this example, The Name field has an array of two objects FirstName and LastName. These two objects are joined and bind to a column using
[`valueAccessor`](../api/grid/column/#valueaccessor).

{% tab template="grid/grid", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { stringData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=90></e-column>
                        <e-column field='Name' headerText='Full Name' [valueAccessor]= 'valueAccess' width=120></e-column>
                        <e-column field='Title' headerText='Title' width=150></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public valueAccess = (field: string, data: object, column: object) => {
        return data[field].map((s: { FirstName: string, LastName: string }) => {
            return s.LastName || s.FirstName;
         }).join(' ');
    }

    ngOnInit(): void {
        this.data = stringData;
    }
}

```

{% endtab %}

### Expression Column

You can achieve the expression column by using [`valueAccessor`](../api/grid/column/#valueaccessor) property.

{% tab template="grid/expression", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { foodInformation } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [height]='315'>
                    <e-columns>
                        <e-column field='FoodName' headerText='Food Name' width=150></e-column>
                        <e-column field='Protein' headerText='Protein' textAlign='Right' width=120></e-column>
                        <e-column field='Fat' headerText='Fat' textAlign='Right' width=80></e-column>
                        <e-column field='Carbohydrate' headerText='Carbohydrate' textAlign='Right' width=120></e-column>
                        <e-column headerText='Calories Intake' textAlign='Right' [valueAccessor]='totalCalories' width=150></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    public totalCalories = (field: string, data: { Protein: number, Fat: number, Carbohydrate: number }, column: Object): number => {
        return data.Protein * 4 + data.Fat * 9 + data.Carbohydrate * 4;
    }

    ngOnInit(): void {
        this.data = foodInformation;
    }
}


```

{% endtab %}

## Render boolean value as checkbox

To render boolean values as checkbox in columns, you need to set [`displayAsCheckBox`](../api/grid/column/#displayascheckbox) property as **true**.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [height]='315'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign= 'Right' width=120 format= 'C2'></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' width=150></e-column>
                    <e-column field='Verified' headerText='Verified' [displayAsCheckBox]="true" width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

## See Also

* [How to Change Column Header Text Dynamically](./how-to/change-header-text-dynamically)
* [Customize Column Styles](./how-to/customize-column-styles)
* [Custom Tooltip for Columns](./how-to/custom-tool-tip-for-columns)
* [How to Render Other Component in a Column](how-to/render-other-components-in-column)
* [Group Column by Format](./grouping#group-by-format)
* [How to Use Edit Template in Foreign Key Column](./how-to/use-edit-template-in-foreign-key-column)
* [How to Create and use custom Filter UI in Foreign Key Column](./how-to/customize-filter-in-foreign-key)
* [How to Use Filter Bar Template in Foreign Key Column](./how-to/use-filter-bar-template-in-foreign-key-column)
* [How to Perform aggregation in Foreign Key Column](./how-to/perform-aggregation-in-foreign-key-column)
* [How to set complex column as Foreignkey column](./how-to/complex-column-as-foreign-key-column)
* [Complex Data Binding with list of Array Of Objects](./how-to/list-of-array-of-objects)