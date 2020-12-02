---
title: "Context Menu"
component: "TreeGrid"
description: "Learn how to use the context menu and add custom context menu items in the Essential JS 2 TreeGrid control."
---

# Context menu

The TreeGrid has options to show the context menu when right clicked on it. To enable this feature, you need to define either default or custom item in the [`contextMenuItems`](../api/treegrid/#contextmenuitems).

To use the context menu, inject the `ContextMenu` module in the treegrid.

The default items are in the following table.

Items| Description
----|----
`AutoFit`|  Auto fit the current column.
`AutoFitAll` | Auto fit all columns.
`Edit`|  Edit the current record.
`Delete` | Delete the current record.
`Save` | Save the edited record.
`Cancel` | Cancel the edited state.
`PdfExport` | Export the treegrid data as Pdf document.
`ExcelExport` | Export the treegrid data as Excel document.
`CsvExport` | Export the treegrid data as CSV document.
`SortAscending` | Sort the current column in ascending order.
`SortDescending` | Sort the current column in descending order.
`FirstPage` | Go to the first page.
`PrevPage` | Go to the previous page.
`LastPage` | Go to the last page.
`NextPage` | Go to the next page.
`AddRow` | Add new row to the treegrid.

{% tab template="treegrid/context-menu", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' #treegrid height='220' [allowPaging]='true' pageSettings='pager'
    [contextMenuItems]='contextMenuItems'
    [allowResizing]='true' [allowSorting]='true' [treeColumnIndex]='1'  childMapping='subtasks' [allowExcelExport]='true' [allowPdfExport]='true'>
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
    public pager: Object;
    public editSettings: Object;
    public contextMenuItems: Object[];

    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = {allowEditing: true, allowAdding: true, allowDeleting: true, mode:"Row"};
        this.contextMenuItems = ['AutoFit', 'AutoFitAll', 'SortAscending', 'SortDescending','Edit',                     'Delete', 'Save', 'Cancel', 'PdfExport', 'ExcelExport', 'CsvExport'                              'FirstPage', 'PrevPage', 'LastPage', 'NextPage'];
        this.pager = { pageSize: 8 }
    }
}

```

{% endtab %}

## Custom context menu items

The custom context menu items can be added by defining the [`contextMenuItems`](../api/treegrid/#contextmenuitems) as a collection of
[`contextMenuItemModel`](../api/grid/contextMenuItemModel/).
Actions for this customized items can be defined in the [`contextMenuClick`](../api/treegrid/#contextmenuclick) event.

In the below sample, we have shown context menu item for parent rows to expand or collapse child rows.

{% tab template="treegrid/context-menu", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { getValue, isNullOrUndefined } from '@syncfusion/ej2-base';
import { BeforeOpenCloseEventArgs } from '@syncfusion/ej2-inputs';
import { MenuEventArgs } from '@syncfusion/ej2-navigations';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' #treegrid height='220' [allowPaging]='true' pageSettings='pager'
    [contextMenuItems]='contextMenuItems' [treeColumnIndex]='1'
    (contextMenuClick)='contextMenuClick($event)' (contextMenuOpen)='contextMenuOpen($event)'  childMapping='subtasks'>
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
    public pager: Object;
    public editSettings: Object;
    public contextMenuItems: Object[];
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = {allowEditing: true, allowAdding: true, allowDeleting: true, mode:"Row"};
        this.contextMenuItems =  [
                {text: 'Collapse the Row', target: '.e-content', id: 'collapserow'},
                {text: 'Expand the Row', target: '.e-content', id: 'expandrow'}
            ];
        this.pager = { pageSize: 8 }
    }
    contextMenuClick(args?: MenuEventArgs): void {
        treeGridObj.getColumnByField('taskID');
        if (args.item.id === 'collapserow') {
            this.treeGridObj.collapseRow(<HTMLTableRowElement>(this.treeGridObj.getSelectedRows()[0]));
        } else {
            this.treeGridObj.expandRow(<HTMLTableRowElement>(this.treeGridObj.getSelectedRows()[0]));
            }
    },
    contextMenuOpen(arg?: BeforeOpenCloseEventArgs) : void {
        let elem: Element = arg.event.target as Element;
        let uid: string = elem.closest('.e-row').getAttribute('data-uid');
        if (isNullOrUndefined(getValue('hasChildRecords', this.treeGridObj.grid.getRowObjectFromUID(uid).data))) {
            arg.cancel = true;
        } else {
            let flag: boolean = getValue('expanded', this.treeGridObj.grid.getRowObjectFromUID(uid).data);
            let val: string = flag ? 'none' : 'block';
            document.querySelectorAll('li#expandrow')[0].setAttribute('style', 'display: ' + val + ';');
            val = !flag ? 'none' : 'block';
            document.querySelectorAll('li#collapserow')[0].setAttribute('style', 'display: ' + val + ';');
        }
    }
}

```

{% endtab %}

> You can hide or show an item in context menu for specific area inside of treegrid by defining the [`target`](../api/grid/contextMenuItemModel/#target) property.