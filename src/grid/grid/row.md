---
title: "Row"
component: "Grid"
description: "Documentation for row templates (custom row content), detail templates, and DataGrid row styles."
---

# Row

It represents the record details that are fetched from the data source.

## Row Template

The Grid provides a way to use a custom layout for its rows using template feature. The rowTemplate property accepts the template for the row.

In the below example, we have presented Employee Information with Employee Photo in the first column and employee details like Name, Address etc. in the second column.

{% tab template="grid/custom-cell", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { employeeData } from './datasource';
import { Internationalization } from '@syncfusion/ej2-base';

const instance: Internationalization = new Internationalization();

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' height=335 width='auto'>
        <e-columns>
            <e-column headerText='Employee Image' width='150' textAlign='Center'></e-column>
            <e-column headerText='Employee Details' width='300' textAlign='Left'></e-column>
        </e-columns>
        <ng-template #rowTemplate let-data>
            <tr>
                <td class="rowphoto">
                    <img src="https://ej2.syncfusion.com/angular/demos/src/grid/images/{{data.EmployeeID}}.png" alt="{{data.EmployeeID}}" />
                </td>
                <td class="details">
                    <table class="CardTable" cellpadding="3" cellspacing="2">
                        <colgroup>
                            <col width="50%">
                            <col width="50%">
                        </colgroup>
                        <tbody>
                            <tr>
                                <td class="CardHeader">First Name </td>
                                <td>{{data.FirstName}} </td>
                            </tr>
                            <tr>
                                <td class="CardHeader">Last Name</td>
                                <td>{{data.LastName}} </td>
                            </tr>
                            <tr>
                                <td class="CardHeader">Title</td>

                                <td>{{data.Title}}</td>
                            </tr>
                            <tr>
                                <td class="CardHeader">Birth Date</td>
                                <td>{{format(data.BirthDate)}}</td>
                            </tr>
                            <tr>
                                <td class="CardHeader">Hire Date</td>
                                <td>{{format(data.HireDate)}}</td>
                            </tr>
                        </tbody>
                    </table>
                </td>
            </tr>
        </ng-template>
    </ejs-grid>`,
    styleUrls: ['./app/app.style.css']
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = employeeData;
    }
    public format(value: Date): string {
        return instance.formatDate(value, { skeleton: 'yMd', type: 'date' });
    }
}
export interface DateFormat extends Window {
    format?: (value: Date) => string;
}


```

{% endtab %}

## Drag and Drop

The Grid Row drag and drop allows you to drag grid rows and drop to another Grid or custom component.
To enable Row drag and drop in the Grid, set the [`allowRowDragAndDrop`](../api/grid/#allowrowdraganddrop) to true.
The target component on which the Grid rows to be dropped can be set by using
[`targetID`](../api/grid/rowDropSettings/#targetid).

To use Row Drag and Drop, you need to inject **RowDDService** in the provider section of **AppModule**.

{% tab template="grid/dragndrop", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { RowDropSettingsModel, SelectionSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid id='Grid' [dataSource]='data' [allowRowDragAndDrop]='true'
                [rowDropSettings]='rowDropOptions' [selectionSettings]='selectionOptions'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>
                <ejs-grid id='DestGrid' [dataSource]='destGridData' [allowRowDragAndDrop]='true'
                [rowDropSettings]='destRowDropOptions' [selectionSettings]='selectionOptions'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
    styleUrls: ['./app/app.style.css']
})
export class AppComponent implements OnInit {

    public data: object[];
    public destGridData: object[];
    public rowDropOptions: RowDropSettingsModel;
    public destRowDropOptions: RowDropSettingsModel;
    public selectionOptions: SelectionSettingsModel;

    ngOnInit(): void {
        this.data = data.slice(0, 5);
        this.destGridData = [];
        this.rowDropOptions = { targetID: 'DestGrid' };
        this.destRowDropOptions = { targetID: 'Grid' };
        this.selectionOptions = { type: 'Multiple' };
    }
}

```

{% endtab %}

> * Selection feature must be enabled for row drag and drop.
> * Multiple rows can be selected by clicking and dragging inside the grid.
For multiple row selection, the [`type`](../api/grid/selectionSettings/#type) property must be set to **Multiple**.

## Row spanning

The grid has option to span row cells. To achieve this, You need to define the [`rowSpan`](../api/grid/queryCellInfoEventArgs/#rowspan) attribute to span cells in the [`QueryCellInfo`](../api/grid/queryCellInfoEventArgs) event.

In the following demo, **Davolio** cell is spanned to two rows in the **EmployeeName** column.

Also Grid supports the spanning of rows and columns for same cells. **Lunch Break** cell is spanned to two rows and three columns in the **1:00** column.

{% tab template="grid/spanning", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { QueryCellInfoEventArgs, GridLine } from '@syncfusion/ej2-angular-grids';
import { columnSpanData, ColumnSpanDataType } from './datasource';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [height]='300' [width]='width' [gridLines]='gridLines'
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
            <e-column field='1:00' headerText='1:00 PM' width='120'></e-column>
            <e-column field='1:30' headerText='1:30 PM' width='120'></e-column>
            <e-column field='2:00' headerText='2:00 PM' width='120'></e-column>
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
            } else if (args.column.field === 'EmployeeName') {
                args.rowSpan = 2;
            } else if (args.column.field === '1:00') {
                args.colSpan = 3;
                args.rowSpan = 2;
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
        this.width = 'auto';
        this.textWrap = true;
    }
}

```

{% endtab %}

> To disable the spanning for particular grid page, we need to use **requestType** from [`QueryCellInfo`](../api/grid/queryCellInfoEventArgs) event argument.

## Customize Rows

You can customize the appearance of the Row by using the [`rowDataBound`](../api/grid/#rowdatabound) event.
The [`rowDataBound`](../api/grid/#rowdatabound) event triggers for every row. In that event handler,
you can get [`RowDataBoundEventArgs`](../api/grid/rowDataBoundEventArgs) which contain details of the row.

{% tab template="grid/custom-cell", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { RowDataBoundEventArgs } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [enableHover]='false' [allowSelection]='false' [height]='315'
               (rowDataBound)='rowDataBound($event)'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130 ></e-column>
                    </e-columns>
                </ejs-grid>`,
    styleUrls: ['./app/app.style.css']
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }

    rowDataBound(args: RowDataBoundEventArgs) {
        const Freight = 'Freight';
        if (args.data[Freight] < 30) {
            args.row.classList.add('below-30');
        } else if (args.data[Freight] < 80) {
            args.row.classList.add('below-80');
        } else {
            args.row.classList.add('above-80');
        }
    }
}


```

{% endtab %}

## Styling alternate Row

 You can change the grid's alternative rows' background color by overriding the **.e-altrow** class.

```css
.e-grid .e-altrow {
    background-color: #fafafa;
}
```

Please refer the following example.

{% tab template="grid/grid", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=140></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign='Right' format='C' width=120></e-column>
                    <e-column field='OrderDate' headerText='Order Date' textAlign='Right' format='yMd' width=140></e-column>
                </e-columns>
               </ejs-grid>`,
    styles: [`
        .e-grid .e-altrow {
            background-color: #fafafa;
        }
    `]
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data.slice(0, 8);
    }
}

```

{% endtab %}

## Row height

You can customize the row height of grid rows through the [`rowHeight`](../api/grid/#rowheight) property. The [`rowHeight`](../api/grid/#rowheight) property
is used to change the row height of entire grid rows.

In the below example, the [`rowHeight`](../api/grid/#rowheight) is set as '60px'.

{% tab template="grid/custom-cell", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [enableHover]='false' [allowSelection]='false' [height]='315' [rowHeight]='60'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130 ></e-column>
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

### Customize row height for particular row

Grid row height for particular row can be customized using the [`rowDataBound`](../api/grid/#rowdatabound)
event by setting the [`rowHeight`](../api/grid/#rowheight) in arguments for each row based on the requirement.

In the below example, the row height for the row with OrderID as '10249' is set as '90px' using the [`rowDataBound`](../api/grid/#rowdatabound) event.

{% tab template="grid/custom-cell", sourceFiles="app/**/*.ts"%}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { Query, DataManager } from '@syncfusion/ej2-data';
import { RowDataBoundEventArgs } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [height]='315' (rowDataBound)='rowDataBound($event)'>
                    <e-columns>
                        <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=100></e-column>
                        <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                        <e-column field='Freight' headerText='Freight' textAlign='Right' format='C2' width=80></e-column>
                        <e-column field='ShipCity' headerText='Ship City' width=130 ></e-column>
                    </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {
    public data: object[];

    ngOnInit(): void {
        this.data = new DataManager(data as JSON[]).executeLocal(new Query().take(8));
    }

    public rowDataBound(args: RowDataBoundEventArgs) {
        const OrderID = 'OrderID';
        if (args.data[OrderID] === 10249) {
            args.rowHeight = 90;
        }
    }
}

```

{% endtab %}

> In virtual scrolling mode, it is not applicable to set the [`rowHeight`](../api/grid/#rowheight) using the [`rowDataBound`](../api/grid/#rowdatabound) event.
