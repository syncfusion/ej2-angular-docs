---
title: "ToolBar"
component: "TreeGrid"
description: "Learn how to use the toolbar and add custom toolbar items in the Essential JS 2 TreeGrid control."
---

# ToolBar

The TreeGrid provides ToolBar support to handle treegrid actions. The [`toolbar`](../api/treegrid/#toolbar)
property accepts either the collection of built-in toolbar items and [`ItemModel`](../api/toolbar/itemModel/) objects for custom toolbar items or
HTML element ID for toolbar template.

To use ToolBar, inject `Toolbar` module in the treegrid.

## Built-in toolbar items

Built-in toolbar items execute standard actions of the treegrid, and it can be added by defining the [`toolbar`](../api/treegrid/#toolbar)
as a collection of built-in items. It renders the button with icon and text.

The following table shows built-in toolbar items and its actions.

| Built-in Toolbar Items | Actions |
|------------------------|---------|
| ExpandAll | Expands all the rows.|
| CollapseAll | Collapses all the rows.|
| Add | Adds a new record.|
| Edit | Edits the selected record.|
| Update | Updates the edited record.|
| Delete | Deletes the selected record.|
| Cancel | Cancels the edit state.|
| Search | Searches the records by the given key.|
| Print | Prints the treegrid.|
| ExcelExport | Exports the treegrid to Excel.|
| PdfExport | Exports the treegrid to PDF.|
| WordExport | Exports the treegrid to Word.|

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='220' [allowPaging]='true' pageSettings='pager' [treeColumnIndex]='1'  childMapping='subtasks' [toolbar]='toolbarOptions'>
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
    public toolbarOptions: ToolbarItems[];
    public pager: Object;

    ngOnInit(): void {
        this.data = sampleData;
        this.toolbarOptions = ['Print', 'Search'];
        this.pager = { pageSize: 8 }
    }
}

```

{% endtab %}

> * The [`toolbar`](../api/treegrid/#toolbar) has options to define both built-in and custom toolbar items.

## Custom toolbar items

Custom toolbar items can be added by defining the [`toolbar`](../api/treegrid/#toolbar) as a collection of
[`ItemModels`](../api/toolbar/itemModel/).
Actions for this customized toolbar items are defined in the [`toolbarClick`](../api/treegrid/#toolbarclick) event.

By default, Custom toolbar items are in position `Left`. You can change the position by using the [`align`](../api/toolbar/itemModel/#align) property. In the below sample, we have applied position `Right` for the `Quick Filter` toolbar item.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [allowFiltering]='true' #treegrid height='220' (toolbarClick)='toolbarClick($event)' [allowPaging]='true' pageSettings='pager' [treeColumnIndex]='1' childMapping='subtasks' [toolbar]='toolbarOptions'>
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
    public toolbarOptions: ToolbarItems[];
    public pager: Object;
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
        this.toolbarOptions = [{text: 'Quick Filter', tooltipText: 'Quick Filter', id: 'toolbarfilter', align:'Right'}];
        this.pager = { pageSize: 8 }
    }

    toolbarClick(args: Object): void {
        if (args.item.id === 'toolbarfilter') {
            this.treeGridObj.filterByColumn('taskName', 'startswith', 'Testing');
        }
    }
}

```

{% endtab %}

> * The [`toolbar`](../api/treegrid/#toolbar) has options to define both built-in and custom toolbar items.
> * If a toolbar item does not match the built-in items, it will be treated as a custom toolbar item.

## Built-in and custom items in toolbar

TreeGrid have an option to use both built-in and custom toolbar items at same time.

In the below example, `ExpandAll`, `CollapseAll` are built-in toolbar items and `Click` is custom toolbar item.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' #treegrid height='220' (toolbarClick)='toolbarClick($event)' [allowPaging]='true' pageSettings='pager'[treeColumnIndex]='1'  childMapping='subtasks' [toolbar]='toolbarOptions'>
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
    public toolbarOptions: ToolbarItems[];
    public pager: Object;
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
        this.toolbarOptions = ['ExpandAll', 'CollapseAll', { text: 'Click', tooltipText: 'Click', prefixIcon: 'e-time', id: 'Click' }];
        this.pager = { pageSize: 8 }
    }

    toolbarClick(args: Object): void {
        if (args.item.text === 'Click') {
            alert("Custom toolbar click...");
        }
    }
}

```

{% endtab %}

## Enable/disable toolbar items

You can enable/disable toolbar items by using the `enableItems` method.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `
      <button ejs-button (click)='enableClick()'>Enable</button>
      <button ejs-button (click)='disableClick()'>Disable</button>
    <ejs-treegrid [dataSource]='data' #treegrid height='220' [allowFiltering]='true' (toolbarClick)='toolbarClick($event)' [allowPaging]='true' pageSettings='pager'[treeColumnIndex]='1'  childMapping='subtasks' [toolbar]='toolbarOptions'>
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
    public toolbarOptions: ToolbarItems[];
    public pager: Object;
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
        this.toolbarOptions = ['QuickFilter', 'ClearFilter'];
        this.pager = { pageSize: 8 }
    }

    toolbarClick(args: Object): void{
        if (args.item.text === 'QuickFilter') {
            this.treeGridObj.filterByColumn('taskName', 'startswith', 'Testing');
        }
        if (args.item.text === 'ClearFilter') {
            this.treeGridObj.clearFiltering();
        }
    }
    enableClick() {
        this.treeGridObj.toolbarModule.enableItems([this.treeGridObj.element.id + '_gridcontrol_QuickFilter', this.treeGridObj.element.id + '_gridcontrol_ClearFilter'], true);// enable toolbar items.
    };

    disableClick() {
        this.treeGridObj.toolbarModule.enableItems([this.treeGridObj.element.id + '_gridcontrol_QuickFilter', this.treeGridObj.element.id + '_gridcontrol_ClearFilter'], false);// disable toolbar items.
    };
}

```

{% endtab %}