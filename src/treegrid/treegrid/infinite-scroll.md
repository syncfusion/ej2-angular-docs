---
title: "Infinite Scrolling"
component: "TreeGrid"
description: "Learn how to improve performance in the Essential JS 2 Tree Grid control by using infinite scroll feature. Also learn about the limitations of this feature."
---

# Infinite scrolling

Infinite scrolling is used to load a huge amount of data without degrading the Tree Grid performance. This feature works like the lazy loading concept, which means the buffer data is loaded only when the scrollbar reaches the end of the scroller.

To use Infinite scrolling, set `enableInfiniteScrolling` property as true and inject the `InfiniteScroll` module in the treegrid.

> * In this feature, Tree Grid will not make a new data request when you visit the same page again.

{% tab template="treegrid/infinite-scroll", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dataSource, virtualData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' [enableInfiniteScrolling]=true height=317 [pageSettings]='pageSettings' childMapping='Crew' [treeColumnIndex]='1' >
        <e-columns>
            <e-column field='TaskID' headerText='Player Jersey' width='120' textAlign='Right'></e-column>
            <e-column field='FIELD1' headerText='Player Name' width='120'></e-column>
            <e-column field='FIELD2' headerText='Year' width='100' textAlign='Right'></e-column>
            <e-column field='FIELD3' headerText='Stint' width='120' textAlign='Right'></e-column>
            <e-column field='FIELD4' headerText='TMID' width='120' textAlign='Right'></e-column>
        </e-columns>
</ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public pageSettings: Object;

    ngOnInit(): void {
        dataSource();
        this.data = virtualData;
        this.pageSettings = {pageSize: 30};
    }
}

```

{% endtab %}

## InitialBlocks

You can define the initial loading pages count by using `infiniteScrollSettings.initialBlocks` property. By default, this feature loads three pages in initial rendering.

In the below demo, we have changed this property value to load five page records instead of three.

{% tab template="treegrid/infinite-scroll", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit} from '@angular/core';
import { dataSource, virtualData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' [enableInfiniteScrolling]=true height=317 [infiniteScrollSettings]='infiniteScrollSettings' [pageSettings]='pageSettings' childMapping='Crew' [treeColumnIndex]='1' >
        <e-columns>
            <e-column field='TaskID' headerText='Player Jersey' width='120' textAlign='Right'></e-column>
            <e-column field='FIELD1' headerText='Player Name' width='120'></e-column>
            <e-column field='FIELD2' headerText='Year' width='100' textAlign='Right'></e-column>
            <e-column field='FIELD3' headerText='Stint' width='120' textAlign='Right'></e-column>
            <e-column field='FIELD4' headerText='TMID' width='120' textAlign='Right'></e-column>
        </e-columns>
</ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public pageSettings: Object;
    public infiniteScrollSettings: Object;

    ngOnInit(): void {
        dataSource();
        this.data = virtualData;
        this.pageSettings = {pageSize: 30};
        this.infiniteScrollSettings = { initialBlocks: 5};
    }
}

```

{% endtab %}

## Cache Mode

Cache is used to store the loaded rows object in the Tree Grid instance which can be reused for creating the row elements whenever you scroll to already visited page. Also, this mode maintains row elements based on the `infiniteScrollSettings.maxBlocks` count value, once this limit exceeds then it will remove row elements from DOM for new rows.

To enable the cache mode in Infinite scrolling, set `infiniteScrollSettings.enableCache` property as true.

{% tab template="treegrid/infinite-scroll", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { dataSource, virtualData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' [enableInfiniteScrolling]=true height=317 [infiniteScrollSettings]='infiniteScrollSettings' [pageSettings]='pageSettings' childMapping='Crew' [treeColumnIndex]='1' >
        <e-columns>
            <e-column field='TaskID' headerText='Player Jersey' width='120' textAlign='Right'></e-column>
            <e-column field='FIELD1' headerText='Player Name' width='120'></e-column>
            <e-column field='FIELD2' headerText='Year' width='100' textAlign='Right'></e-column>
            <e-column field='FIELD3' headerText='Stint' width='120' textAlign='Right'></e-column>
            <e-column field='FIELD4' headerText='TMID' width='120' textAlign='Right'></e-column>
        </e-columns>
</ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public pageSettings: Object;
    public infiniteScrollSettings: Object;

    ngOnInit(): void {
        dataSource();
        this.data = virtualData;
        this.pageSettings = {pageSize: 30};
        this.infiniteScrollSettings = { enableCache: true};
    }
}

```

{% endtab %}

## Limitations for Virtualization

* Due to the element height limitation in browsers, the maximum number of records loaded by the tree grid is limited due to the browser capability.
* Initial loading rows total height must be greater than the viewport height.
* Cell selection will not be persisted in cache mode.
* Infinite scrolling is not compatible with batch editing, detail template and hierarchy features.
* The aggregated information and total group items are displayed based on the current view items. To get these information regardless of the view items, refer to the
* Programmatic selection using the [`selectRows`](https://ej2.syncfusion.com/angular/documentation/api/treegrid/#selectrows) and [`selectRow`](https://ej2.syncfusion.com/angular/documentation/api/treegrid/#selectrow) method is not supported in infinite scrolling.