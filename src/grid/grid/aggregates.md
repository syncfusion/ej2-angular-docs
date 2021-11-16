---
title: "Aggregates"
component: "Grid"
description: "Learn how to aggregate rows, apply custom aggregates, and format the aggregate values in the Essential JS 2 DataGrid control."
---

# Aggregates

Aggregate values are displayed in the footer, group footer and group caption of Grid. It can be configured through **e-aggregates** directive.
The [`field`](../api/grid/aggregateColumnDirective/#field) and [`type`](../api/grid/aggregateColumnDirective/#type)
 are the minimum properties required to represent an aggregate column.

To use aggregate feature, you need to inject the **AggregateService** module into the **@NgModule.providers** section.

By default, the aggregate value can be displayed in footer, group and caption cells, to
show the aggregate value in any of these cells, use the [`footerTemplate`](../api/grid/aggregateColumn/#footertemplate),
[`groupFooterTemplate`](../api/grid/aggregateColumn/#groupfootertemplate) and
[`groupCaptionTemplate`](../api/grid/aggregateColumn/#groupcaptiontemplate) properties.

## Built-in aggregate types

Aggregate type must be specified in [`type`](../api/grid/aggregateColumnDirective/#type) property to configure an aggregate column.

The built-in aggregates are,
* Sum
* Average
* Min
* Max
* Count
* TrueCount
* FalseCount

> * Multiple aggregates can be used for an aggregate column by setting the [`type`](../api/grid/aggregateColumnDirective/#type)
 property
with an array of aggregate type.
> * Multiple types for a column is supported only when one of the aggregate templates is used.

## Footer Aggregate

Footer aggregate value is calculated from all the rows and it can be displayed in footer cells. Use
[`footerTemplate`](../api/grid/aggregateColumnDirective/#footertemplate) to render the aggregate value in footer cells.

{% tab template="grid/aggregates-footer", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    templateUrl: 'app/app.template.html'
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

> * Use the template reference variable name as **#footerTemplate** to specify the footer template.
> * The aggregate values must be accessed inside the template using their corresponding
[`type`](../api/grid/aggregateColumnDirective/#type) name.

## Format the Aggregate Value

You can format the aggregate value result by using the
[`format`](../api/grid/aggregateColumn/#format) property.

{% tab template="grid/aggregates-footer", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    templateUrl: 'app/app.template.html'
})
export class AppComponent implements OnInit {

    public data: object[];

    ngOnInit(): void {
        this.data = data;
    }
}

```

{% endtab %}

## Group and Caption Aggregate

Group and caption aggregate values are calculated from the current group items.
If [`groupFooterTemplate`](../api/grid/aggregateColumnDirective/#groupfootertemplate) is provided then the aggregate values can be displayed
 in the group footer cells and
if [`groupCaptionTemplate`](../api/grid/aggregateColumnDirective/#groupcaptiontemplate)
 is provided then aggregate values can be displayed in the group caption cells.

{% tab template="grid/aggregates-group", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { GroupSettingsModel } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    templateUrl: 'app/app.template.html'
})
export class AppComponent implements OnInit {

    public data: Object[];
    public groupOptions: GroupSettingsModel = { showDropArea: false, columns: ['ShipCountry'] };

    ngOnInit(): void {
        this.data = data;
    }
}
```

{% endtab %}

> * Use the template reference variable name as **#groupFooterTemplate** to specify the group footer template
and as **#groupCaptionTemplate** to specify the group caption template.
> * The aggregate values must be accessed inside the template using their corresponding [`type`](../api/grid/aggregateColumnDirective/#type)
name.

## Custom Aggregate

Sometimes you can have a scenario to calculate aggregate value using your own aggregate function,
 we can achieve this behavior using the custom aggregate option.
To use custom aggregation, specify the
[`type`](../api/grid/aggregateColumnDirective/#type) as **Custom** and provide the custom aggregate
function in the [`customAggregate`](../api/grid/aggregateColumnDirective/#customaggregate) property.

The custom aggregate function will be invoked with different arguments for Total and Group aggregations.
* **Total aggregation** - the custom aggregate function will be called with whole data and the current [`AggregateColumn`](../api/grid/aggregateColumnDirective)
object.
* **Group aggregation** - it will be called with current group details and the [`AggregateColumn`](../api/grid/aggregateColumnDirective) object.

{% tab template="grid/aggregates-custom", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { ReturnType, AggregateColumnModel } from '@syncfusion/ej2-grids';

@Component({
    selector: 'app-root',
    templateUrl: 'app/app.template.html'
})
export class AppComponent implements OnInit {

    public data: object[];
    ngOnInit(): void {
        this.data = data;
    }
    public customAggregateFn = (sdata: ReturnType, aggColumn: AggregateColumnModel) =>
        sdata.result.filter((item: object) => item[aggColumn.columnName] === 'Brazil').length
}


```

{% endtab %}

> To access the custom aggregate value inside template, use the key as **Custom**

## Reactive aggregate update

When using batch editing, the aggregate values will be refreshed on every cell save. The footer, group footer, and group caption aggregate values will be refreshed.

> Adding a new record to the grouped grid will not refresh the aggregate values.

{% tab template="grid/reactive-aggregates-inlineedit", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { GroupSettingsModel, EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' height='290px' [allowPaging]='true' [toolbar]='toolbar' [allowGrouping]="true" [groupSettings]="groupOptions" [editSettings]='editSettings'>
    <e-columns>
        <e-column field='OrderID' headerText='Order ID' isPrimaryKey='true' textAlign='right' width=120></e-column>
        <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
        <e-column field='OrderDate' headerText='Order Date' format='yMd' width=120></e-column>
        <e-column field='Freight' format='C2' editType='numericedit' width=150></e-column>
        <e-column field='ShipCountry' headerText='Ship Country' width=150></e-column>
        <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
    </e-columns>
    <e-aggregates>
        <e-aggregate>
                <e-columns>
                    <e-column field="Freight" type="sum" format="C2">
                        <ng-template #footerTemplate let-data>Sum: {{data.sum}}</ng-template>
                    </e-column>
                    <e-column field="Freight" type="sum" format="C2">
                        <ng-template #groupFooterTemplate let-data>Sum: {{data.sum}}</ng-template>
                    </e-column>
                    <e-column field="Freight" type="average" format="C2">
                        <ng-template #groupCaptionTemplate let-data>Max: {{data.average}}</ng-template>
                    </e-column>
                </e-columns>
        </e-aggregate>
    </e-aggregates>
</ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public groupOptions: GroupSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowDeleting: true, mode: 'Batch' };
        this.toolbar = [ 'Delete', 'Update', 'Cancel'];
        this.groupOptions =  { showDropArea: false, columns: ['ShipCountry'] };
    }
}

```

{% endtab %}

### Refresh aggregates in inline edit mode

By default, reactive aggregate update is not supported by inline and dialog edit modes as it is not feasible to anticipate the value change event for every editor. But, you can refresh the aggregates manually in the inline edit mode using the refresh method of aggregate module.

In the following code, the input event for the Freight column editor has been registered and the aggregate value has been refreshed manually.

{% tab template="grid/reactive-aggregates-inlineedit", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, IEditCell, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    templateUrl: 'app/app.template.html'
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public selectedRecord: object = {};
    public numericParams: IEditCell;
    @ViewChild('grid') public gridObj: GridComponent;

    actionBegin(args): void {
        if (args.requestType === 'beginEdit') {
            this.selectedRecord = {};
            this.selectedRecord = args.rowData;
        }
    }
    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowDeleting: true, mode: 'Normal' };
        this.toolbar = ['Delete', 'Update', 'Cancel'];
        this.numericParams = { params: { change: changeFn.bind(this) } };
    }
}

function changeFn(args): void {
    const Freight = 'Freight';
    this.selectedRecord[Freight] = args.value;
    this.gridObj.aggregateModule.refresh(this.selectedRecord);
}

```

{% endtab %}

## See Also

* [Tooltip for aggregate footer in Angular Grid](https://www.syncfusion.com/forums/154190/tooltip-for-aggregate-footer-in-angular-grid)
* [How to export aggregate footer and apply outer border on excel data in Angular Grid](https://www.syncfusion.com/forums/151023/how-to-export-aggregate-footer-and-apply-outer-border-on-excel-data-in-angular-grid)