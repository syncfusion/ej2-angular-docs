---
title: "Data binding"
component: "TreeGrid"
description: "Learn how to bind local and remote data in the Essential JS 2 TreeGrid control."
---

# Data binding

The TreeGrid uses `DataManager`, which supports both RESTful JSON data services binding and local JavaScript object array binding. The [`dataSource`](../api/treegrid/#datasource) property can be assigned either with the instance of `DataManager` or JavaScript object array collection.
It supports two kinds of data binding method:
* Local data
* Remote data

To learn about how to bind local or remote data to Tree Grid, you can check on this video:

`youtube:N-TS5zv_3cg`

## Local Data

In Local Data binding, data source for rendering the TreeGrid control is retrieved from the same application locally.

Two types of Data binding are possible with the TreeGrid control.

* Hierarchical Datasource binding
* Self-Referential Data binding (Flat Data)

To bind local data to the treegrid, you can assign a JavaScript object array to the [`dataSource`](../api/treegrid#datasource) property. The local data source can also be provided as an instance of the `DataManager`.

> By default, `DataManager` uses `JsonAdaptor` for local data-binding.

### Hierarchy data source binding

The [`childMapping`](../api/treegrid/#childMapping) property is used to map the child records in hierarchy data source.

The following code example shows you how to bind the hierarchical local data into the TreeGrid control.

{% tab template="treegrid/data-binding", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import {PageSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [treeColumnIndex]='1' childMapping='subtasks'
                [allowPaging]="true" [pageSettings]='pageSettings'>
                <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public pageSettings: PageSettingsModel;

    ngOnInit(): void {
        this.data = sampleData;
        this.pageSettings = { pageSize: 6 };
    }
}

```

{% endtab %}

### Self-Referential Data binding (Flat Data)

TreeGrid is rendered from Self-Referential data structures by providing two fields, ID field and parent ID field.

* **ID Field**: This field contains unique values used to identify nodes. Its name is assigned to the [`idMapping`](../api/treegrid/#idmapping) property.
* **Parent ID Field**: This field contains values that indicate parent nodes. Its name is assigned to the [`parentIdMapping`](../api/treegrid/#parentidmapping) property.

{% tab template="treegrid/data-binding", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { projectData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' parentIdMapping='parentID' idMapping='TaskID' height=265 [allowPaging]="true">
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='170'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='130' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='80' textAlign='Right'></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = projectData;
    }
}

```

{% endtab %}

> Herewith we have provided list of reserved properties and the purpose used in TreeGrid. We recommend to avoid these reserved properties for Internal purpose(To get rid of conflicts).

Reserved keywords | Purpose
-----|-----
childRecords | Specifies the childRecords of a parentData
hasChildRecords | Specifies whether the record contains child records
hasFilteredChildRecords | Specifies whether the record contains filtered child records
expanded | Specifies whether the child records are expanded
parentItem | Specifies the parentItem of childRecords
index | Specifies the index of current record
level | Specifies the hierarchy level of record
filterLevel | Specifies the hierarchy level of filtered record
parentIdMapping | Specifies the parentID
uniqueID | Specifies the unique ID of a record
parentUniqueID | Specifies the parent Unique ID of a record
checkboxState | Specifies the checkbox state of a record
isSummaryRow | Specifies the summary of a record
taskData | Specifies the main data
primaryParent | Specifies the Primary data

## Remote data

To bind remote data to TreeGrid component, assign service data as an instance of `DataManager` to the [`dataSource`](../api/treegrid/#datasource) property. To interact with remote data source,  provide the endpoint `url` and define the [`hasChildMapping`](../api/treegrid/#haschildmapping) property of treegrid.

The [`hasChildMapping`](../api/treegrid/#haschildmapping) property maps the field name in data source, that denotes whether current record holds any child records. This is useful internally to show expand icon while binding child data on demand.

The TreeGrid provides `Load on Demand` support for rendering remote data. The Load on demand is considered in TreeGrid for the following actions.

* Expanding root nodes.
* Navigating pages, with paging enabled in TreeGrid.

When load on demand is enabled, all the root nodes are rendered in collapsed state at initial load.

When load on demand support is enabled in TreeGrid with paging, the current or active page’s root node alone will be rendered in collapsed state. On expanding the root node, the child nodes will be loaded from the remote server.

When a root node is expanded, its child nodes are rendered and are cached locally, such that on consecutive expand/collapse actions on root node, the child nodes are loaded from the cache instead from the remote server.

Similarly, if the user navigates to a new page, the root nodes of that specific page, will be rendered with request to the remote server.

{% tab template="treegrid/data-binding", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' hasChildMapping='isParent' parentIdMapping='ParentItem' idMapping='TaskID' [allowPaging]="true">
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='170'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='130' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='80' textAlign='Right'></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    ngOnInit(): void {
        this.data = new DataManager({
                url: 'https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData',
                adaptor: new WebApiAdaptor, crossDomain: true
            });
    }
}

```

{% endtab %}

> By default, `DataManager` uses `ODataAdaptor` for remote data-binding.
> Based on the RESTful web services, set the corresponding adaptor to DataManager. Refer [`here`](https://ej2.syncfusion.com/documentation/data/adaptors/?no-cache=1) for more details.
> Filtering and searching server-side data operations are not supported in load on demand

### Offline Mode

On remote data binding, all treegrid actions such as paging, loading child on-demand, will be processed on server-side. To avoid postback, set the treegrid to load all data on initialization and make the actions process in client-side. To enable this behavior, use the `offline` property of `DataManager`.

{% tab template="treegrid/data-binding", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' parentIdMapping='ParentItem' idMapping='TaskID' [allowPaging]="true">
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='170'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='130' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='80' textAlign='Right'></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    ngOnInit(): void {
        this.data = new DataManager({
                url: 'https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData',
                adaptor: new WebApiAdaptor, crossDomain: true, offline: true
            });
    }
}

```

{% endtab %}

### Custom Adaptor

You can create your own adaptor by extending the built-in adaptors. The following demonstrates custom adaptor approach and how to add a serial number for the records by overriding the built-in response processing using the `processResponse` method of the `ODataAdaptor`.

{% tab template="treegrid/data-binding", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' parentIdMapping='ParentItem' idMapping='TaskID' height=265 [allowPaging]="true">
        <e-columns>
            <e-column field='Sno' headerText='SNO' width='60' textAlign='Right'></e-column>
            <e-column field='TaskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='170'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='130' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='80' textAlign='Right'></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    ngOnInit(): void {
        class SerialNoAdaptor extends WebApiAdaptor {
            public processResponse(): Object[] {
                let i: number = 0;
                // calling base class processResponse function
                let original: Object[] = super.processResponse.apply(this, arguments);
                // adding serial number
                original.forEach((item: Object) => item['Sno'] = ++i);
                return original;
            }
}
        this.data = new DataManager({
                url: 'https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData',
                adaptor: new SerialNoAdaptor, crossDomain: true, offline: true
            });
    }
}
```

{% endtab %}

### Sending additional parameters to the server

To add a custom parameter to the data request, use the `addParams` method of `Query` class. Assign the `Query` object with additional parameters to the treegrid [`query`](../api/treegrid/#query) property.

{% tab template="treegrid/data-binding", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager,Query, WebApiAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' [query]='query' parentIdMapping='ParentItem' idMapping='TaskID' height=265 [allowPaging]="true">
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='170'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='130' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='80' textAlign='Right'></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    public query: Query;

    ngOnInit(): void {
        this.data = new DataManager({
                url: 'https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData',
                adaptor: new WebApiAdaptor, crossDomain: true
            });
        this.query = new Query().addParams('ej2treegrid', 'true');
}
}
```

{% endtab %}

### Handling HTTP error

During server interaction from the treegrid, some server-side exceptions may occur, and you can acquire those error messages or exception details
in client-side using the [`actionFailure`](../api/treegrid/#actionfailure) event.

The argument passed to the [`actionFailure`](../api/treegrid/#actionfailure) event contains the error details returned from the server.

{% tab template="treegrid/data-binding", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { DataManager } from '@syncfusion/ej2-data';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';
@Component({
    selector: 'app-container',
    template: `<ejs-treegrid  #treegrid [treeColumnIndex]='1' (actionFailure)="onActionFailure($event)"
    parentIdMapping='ParentItem' [dataSource]='data' idMapping='TaskID' [allowPaging]="true">
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='170'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='130' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='80' textAlign='Right'></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    @ViewChild('treegrid')
    public treegrid: TreeGridComponent;

    ngOnInit(): void {
        this.data = new DataManager({
    url: 'http://some.com/invalidUrl'
});
}
 onActionFailure(e: any): any {
       let span: HTMLElement = document.createElement('span');
       this.treegrid.element.parentNode.insertBefore(span, this.treegrid.element);
       span.style.color = '#FF0000'
       span.innerHTML = 'Server exception: 404 Not found';
    }
}
```

{% endtab %}

> The [`actionFailure`](../api/treegrid/#actionfailure) event will be triggered not only for the server errors, but
also when there is an exception while processing the treegrid actions.

## Binding with ajax

You can use TreeGrid [`dataSource`](../api/treegrid/#datasource) property to bind the data source to TreeGrid from external ajax request. In the below code we have fetched the data source from the server with the help of ajax request and provided that to [`dataSource`](../api/treegrid/#datasource) property by using `onSuccess` event of the ajax.

{% tab template="treegrid/data-binding", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { Ajax } from '@syncfusion/ej2-base';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: ` <button ejs-button (click)="click()">Bind Data</button>
    <ejs-treegrid #treegrid [dataSource]='data' [treeColumnIndex]='1' parentIdMapping='ParentItem' idMapping='TaskID' [allowPaging]="true" height=240>
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='170'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='130' format="yMd" textAlign='Right'></e-column>
            <e-column field='Duration' headerText='Duration' width='80' textAlign='Right'></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    @ViewChild('treegrid')
    public treegrid: TreeGridComponent;
    ngOnInit(): void {
}
 click(e: any): any{
    let ajax = new Ajax("https://ej2services.syncfusion.com/production/web-services/api/SelfReferenceData","GET");
    let trgrid = this.treegrid;
    ajax.send();
    ajax.onSuccess = function (data: string) {
        trgrid.hideSpinner();
        trgrid.dataSource = JSON.parse(data);
    };
}
}
```

{% endtab %}

> * If you bind the dataSource from this way, then it acts like a local dataSource. So you cannot perform any server side crud actions.