---
title: "Hierarchical Binding"
component: "Grid"
description: "Learn how to display master-detail data in the Essential JS 2 DataGrid control in a hierarchical manner."
---

# Hierarchical Binding

The Grid allows display of table data in a hierarchical structure to visualize relations between parent and child records.
This feature is enabled by defining the [`childGrid`](../api/grid/#childgrid) and
[`childGrid.queryString`](../api/grid/#querystring).
The [`childGrid`](../api/grid/#childgrid) describes the options of grid and the
[`childGrid.queryString`](../api/grid/#querystring) describes the relation between parent and child grids.

To use hierarchical binding, inject the **DetailRowService** in the provider section of **AppModule**.

{% tab template="grid/default", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, GridModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='pData' height='315px' [childGrid]='childGrid'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>
                `,
    providers: [DetailRowService]
})
export class AppComponent implements OnInit {

    public pData: object[];
    public childGrid: GridModel = {
        dataSource: data,
        queryString: 'EmployeeID',
        columns: [
            { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
            { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
            { field: 'ShipCity', headerText: 'Ship City', width: 150 },
            { field: 'ShipName', headerText: 'Ship Name', width: 150 }
        ],
    };

    ngOnInit(): void {
        this.pData = employeeData;
    }
}

```

{% endtab %}
> * Grid supports n level of child grids.
> * Hierarchical binding is not supported when [`DetailTemplate`](../api/grid/#detailtemplate) is enabled.

## ExpandAll by external button

By default, grid renders in collapsed state.
You can expand all child grid rows by invoking the [`expandAll`](../api/grid/detailRow/#expandall) method,
and collapse all grid rows by invoking the [`collapseAll`](../api/grid/detailRow/#collapseall) through an external button.

{% tab template="grid/default", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, GridModel, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<button ej-button (click)='expand()'>Expand All</button>
                <button ej-button (click)='collapse()'>Collapse All</button>
                <ejs-grid #grid [dataSource]='pData' height='265px' [childGrid]='childGrid'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>
                `,
    providers: [DetailRowService]
})
export class AppComponent implements OnInit {

    public pData: object[];
    public childGrid: GridModel = {
        dataSource: data,
        queryString: 'EmployeeID',
        columns: [
            { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
            { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
            { field: 'ShipCity', headerText: 'Ship City', width: 150 },
            { field: 'ShipName', headerText: 'Ship Name', width: 150 }
        ],
    };
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.pData = employeeData;
    }

    expand(): void {
        this.grid.detailRowModule.expandAll();
    }

    collapse(): void {
        this.grid.detailRowModule.collapseAll();
    }

}

```

{% endtab %}

## Expand child grid initially

You can expand a particular child grid at initial rendering by invoking the
[`expand`](../api/grid/detailRow/#expand) method in the [`dataBound`](../api/grid/#databound) event.

{% tab template="grid/default", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, GridModel, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='pData' height='265px' [childGrid]='childGrid' (dataBound)='onDataBound()'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>
                `,
    providers: [DetailRowService]
})
export class AppComponent implements OnInit {

    public pData: object[];
    public childGrid: GridModel = {
        dataSource: data,
        queryString: 'EmployeeID',
        columns: [
            { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
            { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
            { field: 'ShipCity', headerText: 'Ship City', width: 150 },
            { field: 'ShipName', headerText: 'Ship Name', width: 150 }
        ],
    };
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.pData = employeeData;
    }

    onDataBound(): void {
        this.grid.detailRowModule.expand(2); // initial expand 2 chid Grid.
    }

}


```

{% endtab %}

## Dynamically load child grid data

You can dynamically load child grid dataSource by using the
[`load`](../api/grid/#load)  event.

{% tab template="grid/default", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, GridModel, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='pData' height='265px' [childGrid]='childGrid' (load)='onLoad($event)'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>
                `,
    providers: [DetailRowService]
})
export class AppComponent implements OnInit {

    public pData: object[];
    public childGrid: GridModel = {
        queryString: 'EmployeeID',
        columns: [
            { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
            { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
            { field: 'ShipCity', headerText: 'Ship City', width: 150 },
            { field: 'ShipName', headerText: 'Ship Name', width: 150 }
        ],
    };
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.pData = employeeData;
    }

    onLoad(): void {
        this.grid.childGrid.dataSource = data; // assign data source for child grid.
    }

}


```

{% endtab %}

## Bind hierarchy grid with different field

By default, Parent and child grid relation will be maintained by [`queryString`](../api/grid/#querystring) property. We should use the same field name to map both parent and child grid. To achieve parent and child relation with different fields, we need to change the mapping value in the child grid [`load`](../api/grid/#load) event.

In the below sample, we have bound the child and parent grid with different fields. Parent grid field name as **EmployeeID** and the child grid field name as **ID**. We need to define the mapping value of **parentKeyFieldValue** from the parent row data in the child grid [`load`](../api/grid/#load) event.

{% tab template="grid/default", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, GridModel, GridComponent} from '@syncfusion/ej2-angular-grids';


@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='pData' height='265px' [childGrid]='childGrid'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>
                `,
    providers: [DetailRowService]
})
export class AppComponent implements OnInit {
    @ViewChild('grid') public grid: GridComponent;
    public pData: object[];
    public childGrid: GridModel | GridComponent = {
        queryString: 'ID',
        dataSource: data,
        columns: [
            { field: 'ID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
            { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
            { field: 'ShipCity', headerText: 'Ship City', width: 150 },
            { field: 'ShipName', headerText: 'Ship Name', width: 150 }
        ],
        load() {
            const EmployeeID = 'EmployeeID';
            (this as GridComponent).parentDetails.parentKeyFieldValue = (<{ EmployeeID?: string}>(this as GridComponent).parentDetails.parentRowData)[EmployeeID];
        }
    };

    ngOnInit(): void {
        this.pData = employeeData;
    }
}



```

{% endtab %}

## Adding Record in ChildGrid

Parent and child grid are related by [`queryString`](../api/grid/#querystring) field value.
To maintain this relation in newly added record, You need to set value for [`queryString`](../api/grid/#querystring) field in the added data
by the [`actionBegin`](../api/grid/#actionbegin) event.

In the below demo, **EmployeeID** field relates the parent and child grids. To add a new record in child grid, We have to set the **EmployeeID** field
with parent record's [`queryString`](../api/grid/#querystring) field value in the [`actionBegin`](../api/grid/#actionbegin) event.

{% tab template="grid/default", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, EditService, ToolbarService, AddEventArgs, GridModel, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='pData' height='265px' [childGrid]='childGrid'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>
                `,
    providers: [DetailRowService, EditService, ToolbarService]
})
export class AppComponent implements OnInit {

    public pData: object[];
    public childGrid: GridModel = {
        dataSource: data,
        queryString: 'EmployeeID',
        toolbar: ['Add', 'Edit', 'Delete', 'Update', 'Cancel'],
        editSettings: { allowEditing: true, allowAdding: true, allowDeleting: true },
        columns: [
            { field: 'OrderID', headerText: 'Order ID', isPrimaryKey: true, textAlign: 'Right', width: 120 },
            { field: 'EmployeeID', headerText: 'Employee ID', textAlign: 'Right', allowEditing: false, width: 120 },
            { field: 'ShipCity', headerText: 'Ship City', width: 150 },
            { field: 'ShipName', headerText: 'Ship Name', width: 150 }
        ],
        actionBegin(args: AddEventArgs) {
            if (args.requestType === 'add') {
                // `parentKeyFieldValue` refers to the queryString field value of the parent record.
                const EmployeeID = 'EmployeeID';
                (args.data as object)[EmployeeID] = this.parentDetails.parentKeyFieldValue;
            }
        }
    };
    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.pData = employeeData;
    }
}

```

{% endtab %}

## Template column in Child Grid

The column [`template`](../api/grid/column/#template) has options to display custom element instead of a field value in the column.

In the below sample, we have shown custom image in **Employee Image** column of child grid using column [`template`](../api/grid/column/#template) property.

{% tab template="grid/default", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild, ViewContainerRef, Inject, AfterViewInit } from '@angular/core';
import { data, employeeData } from './datasource';
import { DetailRowService, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='pData' height='315px' [childGrid]='childGrid'>
                    <e-columns>
                        <e-column field='EmployeeID' headerText='Employee ID' textAlign='Right' width=120></e-column>
                        <e-column field='FirstName' headerText='FirstName' width=150></e-column>
                        <e-column field='LastName' headerText='Last Name' width=150></e-column>
                        <e-column field='City' headerText='City' width=150></e-column>
                    </e-columns>
                </ejs-grid>
                <ng-template #childtemplate let-data>
                    <div class="image">
                            <img src="{{data.EmployeeID}}.png" alt="{{data.EmployeeID}}"/>
                     </div>
                </ng-template>
                `,
    providers: [DetailRowService]
})
export class AppComponent implements OnInit, AfterViewInit {

    constructor(@Inject(ViewContainerRef) private viewContainerRef?: ViewContainerRef) {

    }
    public pData: object[];
    @ViewChild('childtemplate') public childtemplate: any;
    @ViewChild('grid') public grid: GridComponent;
    public childGrid: any;

    ngAfterViewInit() {
        this.childtemplate.elementRef.nativeElement._viewContainerRef = this.viewContainerRef;
        this.childtemplate.elementRef.nativeElement.propName = 'template';
    }

    ngOnInit(): void {
        this.pData = employeeData;
        this.childGrid = {
            dataSource: data,
            queryString: 'EmployeeID',
            load() {
                this.registeredTemplate = {};   // set registertemplate value as empty in load event
            },
            columns: [
                { headerText: 'Employee Image', textAlign: 'Center', template: this.childtemplate, width: 150 },
                { field: 'OrderID', headerText: 'Order ID', textAlign: 'Right', width: 120 },
                { field: 'CustomerID', headerText: 'Customer ID', width: 150 },
                { field: 'ShipCity', headerText: 'Ship City', width: 150 },
                { field: 'ShipName', headerText: 'Ship Name', width: 150 }
            ],
        };
    }
}

```

{% endtab %}
