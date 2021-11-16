---
title: "ToolBar"
component: "Grid"
description: "Learn how to use the toolbar and add custom toolbar items in the Essential JS 2 DataGrid control."
---

# Toolbar

The Grid provides ToolBar support to handle grid actions. The [`toolbar`](../api/grid/#toolbar)
property accepts either the collection of built-in toolbar items and
[`ItemModel`](../api/toolbar/itemModel) objects for custom toolbar items or
HTML element ID for toolbar template.

To use Toolbar, you need to inject **ToolbarService** in the provider section of **AppModule**.

## Built-in Toolbar Items

Built-in Toolbar Items execute standard actions of the Grid and it can be added by defining
[`toolbar`](../../api/grid/#toolbar)
as a collection of built-in items. It renders the button with icon and text.

The following table shows Built-in toolbar items and its action.

| Built-in Toolbar Items | Actions |
|------------------------|---------|
| Add | Add a new record.|
| Edit | Edit the selected record.|
| Update | Update edited record.|
| Delete | Delete the selected record.|
| Cancel | Cancel the edit state.|
| Search | Search the records by given key.|
| Print | Print the Grid.|
| ColumnChooser | Choose the column's visibility.|
| PdfExport | Exports grid to PDF document.|
| ExcelExport | Exports grid to Excel document.|
| CsvExport | Exports grid to CSV document.|

{% tab template="grid/toolbar", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { ToolbarItems } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height='270px' [toolbar]='toolbar'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.data = data;
        this.toolbar = ['Print', 'Search'];
    }
}

```

{% endtab %}

> * The [`toolbar`](../api/grid/#toolbar) has options to define both built-in and custom toolbar items.

## Custom Toolbar Items

Custom toolbar items can be added by defining [`toolbar`](../api/grid/#toolbar) as a collection of
[`ItemModel`](../api/toolbar/itemModel).
Actions for this customized toolbar items are defined in the [`toolbarClick`](../api/grid/#toolbarclick) event.

By default, Custom toolbar items are in position **Left**. You can change the position by using the [`align`](../api/toolbar/itemModel) property. In the below sample, we have applied position **Right** for the **Collapse All** toolbar item.

{% tab template="grid/custom-toolbar", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { data } from './datasource';
import { GroupSettingsModel, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' height='200px' [allowGrouping]='true' [groupSettings]='groupOptions'
               [toolbar]='toolbar' (toolbarClick)='clickHandler($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbar: object[];
    public groupOptions: GroupSettingsModel;

    @ViewChild('grid') public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbar = [{ text: 'Expand All', tooltipText: 'Expand All', prefixIcon: 'e-expand', id: 'expandall' },
         { text: 'Collapse All', tooltipText: 'collection All', prefixIcon: 'e-collapse', id: 'collapseall', align: 'Right' }];
        this.groupOptions = { columns: ['CustomerID'] };
    }

    clickHandler(args: ClickEventArgs): void {
        if (args.item.id === 'expandall') {
            this.grid.groupModule.expandAll();
        }

        if (args.item.id === 'collapseall') {
            this.grid.groupModule.collapseAll();
        }
    }
}

```

{% endtab %}

> * The [`toolbar`](../api/grid/#toolbar) has options to define both built-in and custom toolbar items.
> * If a toolbar item does not match with built-in items, it will be treated as custom toolbar item.

## Built-in and custom items in toolbar

Grid have an option to use both built-in and custom toolbar items at same time.

In the below example, **Add**, **Edit**, **Delete**, **Update**, **Cancel** are built-in toolbar items and **Click** is custom toolbar item.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar'
               (toolbarClick)='clickHandler($event)' height='273px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                    <e-column field='Freight' headerText='Freight' textAlign= 'Right' width=120 format= 'C2'></e-column>
                    <e-column field='ShipCountry' headerText='Ship Country' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[] | object;

    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel',
         { text: 'Click', tooltipText: 'Click', prefixIcon: 'e-expand', id: 'Click' }];
    }

    clickHandler(args: ClickEventArgs): void {
        if (args.item.id === 'Click') {
            alert('Custom Toolbar Click...');
        }
    }
}

```

{% endtab %}

## Custom Toolbar

Custom Toolbar is used to customize the whole toolbar. It can be added by defining
**toolbarTemplate**. Actions for this toolbar template items are defined in the
**clicked** event in toolbar.

{% tab template="grid/toolbar-template", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { data } from './datasource';
import { GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' height='200px' [allowGrouping]='true' [groupSettings]='groupOptions'>
                <ng-template #toolbarTemplate let-data>
                    <ejs-toolbar (clicked)='clickHandler($event)'>
                        <e-items>
                            <e-item id='collapse' prefixIcon='e-collapse'></e-item>
                        </e-items>
                    </ejs-toolbar>
                </ng-template>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public groupOptions: object;

    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.groupOptions = { columns: ['CustomerID'] };
    }

    clickHandler(args: ClickEventArgs): void {
        const target: HTMLElement = (args.originalEvent.target as HTMLElement).closest('button'); // find clicked button
        if (target.id === 'collapse') {
            // collapse all expanded grouped row
            this.grid.groupModule.collapseAll();
        }
    }
}

```

{% endtab %}

## Enable/Disable Toolbar Items

You can enable/disable toolbar items by using the **enableItems** method.

{% tab template="grid/toolbar-enable", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { data } from './datasource';
import { GroupService, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<button ej-button id='enable' cssClass='e-flat' (click)='enable()'>Enable</button>
                <button ej-button id='disable' cssClass='e-flat' (click)='disable()'>Disable</button>
                <ejs-grid id='Grid' #grid [dataSource]='data' height='200px' [allowGrouping]='true'
                [groupSettings]='groupOptions' [toolbar]='toolbar' (toolbarClick)='clickHandler($event)'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [GroupService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public toolbar: string[];
    public groupOptions: object;
    public toolbarObj;

    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
        this.toolbar = ['Expand', 'Collapse'];
        this.groupOptions = { columns: ['CustomerID'] };
    }

    clickHandler(args: ClickEventArgs): void {
        if (args.item.id === 'Grid_Collapse') { // Grid_Collapse is control id + '_' + toolbar value.
            this.grid.groupModule.collapseAll();
        }

        if (args.item.id === 'Grid_Expand') {
            this.grid.groupModule.expandAll();
        }
    }
    enable() {
        this.grid.toolbarModule.enableItems(['Grid_Collapse', 'Grid_Expand'], true); // Enable toolbar items.
    }

    disable() {
        this.grid.toolbarModule.enableItems(['Grid_Collapse', 'Grid_Expand'], false); // Disable toolbar items.
    }
}

```

{% endtab %}

## See Also

* [Toolbar Component](../../toolbar/getting-started)
* [How to add a router link in the toolbar in Angular Grid](https://www.syncfusion.com/forums/154693/how-to-add-a-router-link-in-the-toolbar-in-angular-grid)
* [How to show or hide the delete button in the toolbar in Angular Grid](https://www.syncfusion.com/forums/158052/how-to-show-or-hide-the-delete-button-in-the-toolbar-in-angular-grid)
* [How to display column as radio button in dialog editing in Angular Grid](https://www.syncfusion.com/forums/153052/how-to-display-column-as-radio-button-in-dialog-editing-in-angular-grid)