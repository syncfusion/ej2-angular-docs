---
title: "Infinite Scrolling"
component: "Grid"
description: "Learn how to improve performance in the Essential JS 2 DataGrid control by using this infinite scroll feature. Also learn about the limitations of this feature."
---

# Infinite scrolling

Infinite scrolling is used to load a huge amount of data without degrading the Grid performance. This feature works like the lazy loading concept, which means the buffer data is loaded only when the scrollbar reaches the end of the scroller.

To enable Infinite scrolling, set `enableInfiniteScrolling` property as true.

> * In this feature, Grid will not make a new data request when you visit the same page again.

{% tab template="grid/paging1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { InfiniteScrollService } from '@syncfusion/ej2-angular-grids';
import { PageSettingsModel, InfiniteScrollSettingsModel } from '@syncfusion/ej2-angular-grids';

const names = ['TOM', 'Hawk', 'Jon', 'Chandler', 'Monica', 'Rachel', 'Phoebe', 'Gunther', 'Ross', 'Geller', 'Joey', 'Bing', 'Tribbiani',
 'Janice', 'Bong', 'Perk', 'Green', 'Ken', 'Adams'];
const hours = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const designation = ['Manager', 'Engineer 1', 'Engineer 2', 'Developer', 'Tester'];
const status = ['Completed', 'Open', 'In Progress', 'Review', 'Testing']
const data = (count) => {
    const result = [];
    for (let i = 0; i < count; i++) {
        result.push({
          TaskID: i + 1,
          Engineer: names[Math.round(Math.random() * names.length)] || names[0],
          Designation: designation[Math.round(Math.random() * designation.length)] || designation[0],
          Estimation: hours[Math.round(Math.random() * hours.length)] || hours[0],
          Status: status[Math.round(Math.random() * status.length)] || status[0]
        });
    }
    return result;
};

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height=300 enableInfiniteScrolling='true' [pageSettings]='options'>
                <e-columns>
                    <e-column field='TaskID' headerText='Task ID' textAlign='Right' width=70></e-column>
                    <e-column field='Engineer' width=100></e-column>
                    <e-column field='Designation' width=100></e-column>
                    <e-column field='Estimation' textAlign='Right' width=100></e-column>
                    <e-column field='Status' width=100></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [InfiniteScrollService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public options: PageSettingsModel;
    public infiniteOptions: InfiniteScrollSettingsModel;
    ngOnInit(): void {
        this.data = data(1000);
        this.options = { pageSize: 50 };
        this.infiniteOptions = { enableScroll: true };
    }
}

```

{% endtab %}

## InitialBlocks

You can define the initial loading pages count by using `infiniteScrollSettings.initialBlocks` property. By default, this feature loads three pages in initial rendering.

In the below demo, we have changed this property value to load five page records instead of three.

{% tab template="grid/paging1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { InfiniteScrollService } from '@syncfusion/ej2-angular-grids';
import { PageSettingsModel, InfiniteScrollSettingsModel } from '@syncfusion/ej2-angular-grids';

const names = ['TOM', 'Hawk', 'Jon', 'Chandler', 'Monica', 'Rachel', 'Phoebe', 'Gunther', 'Ross', 'Geller', 'Joey', 'Bing', 'Tribbiani',
 'Janice', 'Bong', 'Perk', 'Green', 'Ken', 'Adams'];
const hours = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const designation = ['Manager', 'Engineer 1', 'Engineer 2', 'Developer', 'Tester'];
const status = ['Completed', 'Open', 'In Progress', 'Review', 'Testing']
const data = (count) => {
    const result = [];
    for (let i = 0; i < count; i++) {
        result.push({
          TaskID: i + 1,
          Engineer: names[Math.round(Math.random() * names.length)] || names[0],
          Designation: designation[Math.round(Math.random() * designation.length)] || designation[0],
          Estimation: hours[Math.round(Math.random() * hours.length)] || hours[0],
          Status: status[Math.round(Math.random() * status.length)] || status[0]
        });
    }
    return result;
};

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height=300 enableInfiniteScrolling='true' [infiniteScrollSettings]='infiniteOptions' [pageSettings]='options'>
                <e-columns>
                    <e-column field='TaskID' headerText='Task ID' textAlign='Right' width=70></e-column>
                    <e-column field='Engineer' width=100></e-column>
                    <e-column field='Designation' width=100></e-column>
                    <e-column field='Estimation' textAlign='Right' width=100></e-column>
                    <e-column field='Status' width=100></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [InfiniteScrollService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public options: PageSettingsModel;
    public infiniteOptions: InfiniteScrollSettingsModel;
    ngOnInit(): void {
        this.data = data(1000);
        this.options = { pageSize: 50 };
        this.infiniteOptions = { initialBlocks: 5 };
    }
}

```

{% endtab %}

## Cache Mode

Cache is used to store the loaded rows object in the Grid instance which can be reused for creating the row elements whenever you scroll to already visited page. Also, this mode maintains row elements based on the `infiniteScrollSettings.maxBlocks` count value, once this limit exceeds then it will remove row elements from DOM for new rows.

To enable the cache mode in Infinite scrolling, set `infiniteScrollSettings.enableCache` property as true.

{% tab template="grid/paging1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { InfiniteScrollService } from '@syncfusion/ej2-angular-grids';
import { PageSettingsModel, InfiniteScrollSettingsModel } from '@syncfusion/ej2-angular-grids';

const names = ['TOM', 'Hawk', 'Jon', 'Chandler', 'Monica', 'Rachel', 'Phoebe', 'Gunther', 'Ross', 'Geller', 'Joey', 'Bing', 'Tribbiani',
 'Janice', 'Bong', 'Perk', 'Green', 'Ken', 'Adams'];
const hours = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const designation = ['Manager', 'Engineer 1', 'Engineer 2', 'Developer', 'Tester'];
const status = ['Completed', 'Open', 'In Progress', 'Review', 'Testing']
const data = (count) => {
    const result = [];
    for (let i = 0; i < count; i++) {
        result.push({
          TaskID: i + 1,
          Engineer: names[Math.round(Math.random() * names.length)] || names[0],
          Designation: designation[Math.round(Math.random() * designation.length)] || designation[0],
          Estimation: hours[Math.round(Math.random() * hours.length)] || hours[0],
          Status: status[Math.round(Math.random() * status.length)] || status[0]
        });
    }
    return result;
};

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height=300 enableInfiniteScrolling='true' [infiniteScrollSettings]='infiniteOptions' [pageSettings]='options'>
                <e-columns>
                    <e-column field='TaskID' headerText='Task ID' textAlign='Right' width=70></e-column>
                    <e-column field='Engineer' width=100></e-column>
                    <e-column field='Designation' width=100></e-column>
                    <e-column field='Estimation' textAlign='Right' width=100></e-column>
                    <e-column field='Status' width=100></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [InfiniteScrollService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public options: PageSettingsModel;
    public infiniteOptions: InfiniteScrollSettingsModel;
    ngOnInit(): void {
        this.data = data(1000);
        this.options = { pageSize: 50 };
        this.infiniteOptions = { enableCache: true };
    }
}

```

{% endtab %}

## Limitations for Infinite Scrolling

* Due to the element height limitation in browsers, the maximum number of records loaded by the grid is limited due to the browser capability.
* Initial loading rows total height must be greater than the viewport height.
* Cell selection will not be persisted in cache mode.
* Infinite scrolling is not compatible with batch editing, detail template and hierarchy features.
* Group expand and collapse state will not be persisted in cache mode.
* The aggregated information and total group items are displayed based on the current view items. To get these information regardless of the view items, refer to the
[`Group with Page`](./grouping/#Group-with-paging) topic.
* Programmatic selection using the [`selectRows`](../api/grid/#selectrows) and [`selectRow`](../api/grid/#selectrow) method is not supported in infinite scrolling.
