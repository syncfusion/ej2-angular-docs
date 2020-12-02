---
title: "Print"
component: "TreeGrid"
description: "Learn how to print TreeGrid content, set up pages for printing, perform external print, and print visible pages in the Essential JS 2 TreeGrid control."
---

# Print

To print the TreeGrid, use the [`print`](../api/treegrid/#print) method from treegrid instance. The print option can be displayed on the [`toolbar`](../api/treegrid/#toolbar) by adding the `print` toolbar item.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='265' [treeColumnIndex]='1'  childMapping='subtasks' [toolbar]='toolbarOptions'>
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

    ngOnInit(): void {
        this.data = sampleData;
        this.toolbarOptions = ['Print'];
    }
}

```

{% endtab %}

## Page setup

Some of the print options cannot be configured through JavaScript code. So, you have to customize the layout, paper size, and margin options using the browser page setup dialog. Please refer to the following links to know more about the browser page setup:

* [`Chrome`](https://support.google.com/chrome/answer/1069693?hl=en&visit_id=1-636335333734668335-3165046395&rd=1)
* [`Firefox`](https://support.mozilla.org/en-US/kb/how-print-web-pages-firefox)
* [`Safari`](http://www.mintprintables.com/print-tips/adjust-margins-osx/)
* [`IE`](http://www.helpteaching.com/help/print/index.htm)

## Print using an external button

To print the treegrid from an external button, invoke the [`print`](../api/treegrid/#print) method.

{% tab template="treegrid/columns", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `
     <button  ejs-button cssClass="btn btn-default" content="Print" (click)="onClicked()"></button>  
    <ejs-treegrid [dataSource]='data' height='265' #treegrid [treeColumnIndex]='1'  childMapping='subtasks'>
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
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
    }
    onClicked(): void {
        this.treeGridObj.print();
    }

}

```

{% endtab %}

## Print the visible page

By default, the treegrid prints all the pages. To print the current page alone, set the [`printMode`](../api/treegrid/#printmode) to `CurrentPage`.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='220' [allowPaging]='true' pageSettings='pager' printMode='CurrentPage' [treeColumnIndex]='1'  childMapping='subtasks' [toolbar]='toolbarOptions'>
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
        this.toolbarOptions = ['Print'];
        this.pager = { pageSize: 8 }
    }
}

```

{% endtab %}

## Print large number of columns

By default, the browser uses A4 as page size option to print pages and to adapt the size of the page the browser print preview will auto-hide the overflowed contents. Hence treegrid with large number of columns will cut off to adapt the print page.

To show large number of columns when printing, adjust the scale option from print option panel based on your content size.

<!-- markdownlint-disable MD033 -->
<img src="../images/print-preview.png" alt="Print Preview Image" style="width:320px;height: 620px">
<!-- markdownlint-enable MD033 -->

## Show or Hide columns while Printing

You can show a hidden column or hide a visible column while printing the treegrid using [`toolbarClick`](../api/treegrid/#toolbarclick) and [`printComplete`](../api/treegrid/#printcomplete) events.

In the `toolbarClick` event, based on `args.item.text` as `Print`. We can show or hide columns by setting `column.visible` property to `true` or `false` respectively.

In the printComplete event, We have reversed the state back to the previous state.

In the below example, we have `Duration` as a hidden column in the treegrid. While printing, we have changed `Duration` to visible column and `StartDate` as hidden column.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' (toolbarClick)='toolbarClick($event)' #treegrid height='265' [allowPaging]='true' pageSettings='pager' printMode='CurrentPage' [treeColumnIndex]='1'
    (printComplete)='printComplete()' childMapping='subtasks' [toolbar]='toolbarOptions'>
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
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
        this.toolbarOptions = ['Print'];
    }
    toolbarClick(args: ClickEventArgs): void {
        if (args.item.text === 'Print') {
            let cols: Column[] = this.treeGridObj.columns;
            for (var i = 0; i < cols.length; i++) {
                if (cols[i].field == "duration") {
                    cols[i].visible = true;
                }
                else if (cols[i].field == "startDate") {
                    cols[i].visible = false;
                }
            }
        }
    }
    printComplete(): void {
        let cols: Column[] = this.treeGridObj.columns;
        for (var i = 0; i < cols.length; i++) {
            if (cols[i].field == "duration") {
                cols[i].visible = false;
            }
            else if (cols[i].field == "startDate") {
                    cols[i].visible = true;
            }
        }
    }
}

```

{% endtab %}

## Limitations of Printing Large Data

When treegrid contains large number of data, printing all the data at once is not a best option for the browser performance. Because to render all the DOM elements in one page will produce performance issues in the browser. It leads to browser slow down or browser hang.

If printing of all the data is still needed, we suggest to Export the treegrid to `Excel` or `CSV` or `Pdf` and then print it from another non-web based application.