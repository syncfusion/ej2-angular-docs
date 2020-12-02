---
title: "Sorting"
component: "TreeGrid"
description: "Learn how to sort rows in the Essential JS 2 TreeGrid control, perform initial sorting, and customize sorting logic."
---

# Sorting

Sorting enables you to sort data in the `Ascending` or `Descending` order.
To sort a column, click the column header.

To sort multiple columns, press and hold the CTRL key and click the column header.  You can clear sorting of any one of the multi-sorted columns by pressing and holding the SHIFT key and clicking the specific column header.

To enable sorting in the TreeGrid, set the [`allowSorting`](../api/treegrid/#allowsorting) to true. Sorting options can be configured through the [`sortSettings`](../api/treegrid/#sortsettings).

To sort, inject the [`Sort`](../api/treegrid/#sortmodule) module in the treegrid.

{% tab template="treegrid/sorting", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sortData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1'  [allowSorting]='true' childMapping='subtasks' >
        <e-columns>
                    <e-column field='Category' headerText='Category' textAlign='Right' width=140></e-column>
                    <e-column field='orderName' headerText='Order Name' textAlign='Left' width=200></e-column>
                    <e-column field='orderDate' headerText='Order Date' textAlign='Right' format='yMd' width=150></e-column>
                    <e-column field='units' headerText='Units' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sortData;
    }
}

```

{% endtab %}

> * TreeGrid columns are sorted in the `Ascending` order. If you click the already sorted column, the sort direction toggles.
> * You can apply and clear sorting by invoking [`sortColumn`](../api/treegrid/#sortcolumn) and
[`clearSorting`](../api/treegrid/#clearsorting) methods.
> * To disable sorting for a particular column, set the [`columns.allowSorting`](../api/treegrid/column/#allowSorting) to false.

## Initial sort

To sort at initial rendering, set the [`field`](../api/treegrid/sortDescriptorModel/#field) and
[`direction`](../api/treegrid/sortDescriptorModel/#direction) in the `sortSettings.columns`.

{% tab template="treegrid/sorting", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sortData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='315'  [allowSorting]='true' childMapping='subtasks' [sortSettings]='initialSort'>
        <e-columns>
                    <e-column field='Category' headerText='Category' textAlign='Right' width=140></e-column>
                    <e-column field='orderName' headerText='Order Name' textAlign='Left' width=200></e-column>
                    <e-column field='orderDate' headerText='Order Date' textAlign='Right' format='yMd' width=150></e-column>
                    <e-column field='units' headerText='Units' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public initialSort: Object;
    ngOnInit(): void {
        this.data = sortData;
        this.initialSort = { columns: [{ field: 'Category', direction: 'Ascending' }, { field: 'orderName', direction: 'Ascending' }] };
    }
}

```

{% endtab %}

## Sorting events

During the sort action, the treegrid component triggers two events. The [`actionBegin`](../api/treegrid/#actionbegin) event triggers before the sort action starts, and the [`actionComplete`](../api/treegrid/#actioncomplete) event triggers after the sort action is completed. Using these events you can perform the needed actions.

{% tab template="treegrid/sorting", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sortData } from './datasource';
import { SortEventArgs } from '@syncfusion/ej2-treegrid';
@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1'  [allowSorting]='true' childMapping='subtasks'  (actionBegin)='actionHandler($event)' (actionComplete)='actionHandler($event)'>
        <e-columns>
                    <e-column field='Category' headerText='Category' textAlign='Right' width=140></e-column>
                    <e-column field='orderName' headerText='Order Name' textAlign='Left' width=200></e-column>
                    <e-column field='orderDate' headerText='Order Date' textAlign='Right' format='yMd' width=150></e-column>
                    <e-column field='units' headerText='Units' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sortData;
    }
    actionHandler(args: SortEventArgs) {
        alert(args.requestType + ' ' + args.type); //custom Action
    }
}

```

{% endtab %}

> The `args.requestType` is the current action name. For example, in sorting the `args.requestType` value is 'sorting'.

<!--  Custom sort comparer

You can customize the default sort action for a column by defining the [`column.sortComparer`](../api/treegrid/column/#sortcomparer) property. The sort comparer function has the same functionality like [`Array.sort`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) sort comparer.

In the following example, custom sort comparer function was defined in the `Category` column.

{% tab template="treegrid/sorting", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sortData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='315' [allowSorting]='true' childMapping='subtasks' >
        <e-columns>
                    <e-column field='Category' headerText='Category' textAlign='Right' width=140></e-column>
                    <e-column field='orderName' headerText='Order Name' textAlign='Left' width=200></e-column>
                    <e-column field='orderDate' headerText='Order Date' textAlign='Right' format='yMd' width=150></e-column>
                    <e-column field='units' headerText='Units' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sortData;
    }
}

```

{% endtab %}

> The sort comparer function will work only for the local data. -->

## Touch interaction

When you tap the treegrid header on touchscreen devices, the selected column header is sorted. A popup ![Multi column sorting](images/sorting.jpg) is displayed for multi-column sorting. To sort multiple columns, tap the popup![Multi sorting](images/msorting.jpg), and then tap the desired treegrid headers.

The following screenshot shows treegrid touch sorting.

<!-- markdownlint-disable MD033 -->
<img src="../images/touch-sorting.jpg" alt="Touch interaction image" style="width:320px;height: 620px">
<!-- markdownlint-enable MD033 -->