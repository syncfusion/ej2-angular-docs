---
title: "Filtering"
component: "TreeGrid"
description: "Learn how to filter rows in the TreeGrid using the filter bar, and menu filtering. Also learn how to use custom filter components in the Essential JS 2 TreeGrid control."
---

# Filtering

Filtering allows you to view specific or related records based on filter criteria. To enable filtering in the TreeGrid, set the [`allowFiltering`](../api/treegrid/#allowfiltering) to true. Filtering options can be configured through [`filterSettings`](../api/treegrid/#filtersettings).

To use filter, inject the [`Filter`] module in the treegrid.

You can check this video to learn about Filtering feature in Angular TreeGrid.

`youtube:3aQueqaspzQ`

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='275' [allowFiltering]='true' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' type='date' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}

```

{% endtab %}

> * You can apply and clear filtering by using [`filterByColumn`](../api/treegrid/#filterbycolumn) and [`clearFiltering`](../api/treegrid/#clearfiltering) methods.
> * To disable filtering for a particular column, set
[`columns.allowFiltering`](../api/treegrid/column/#allowfiltering) to false.

## Filter Hierarchy Modes

TreeGrid provides support for a set of filtering modes with [`filterSettings.filterHierarchyMode`](../api/treegrid/filterSettingsModel/#hierarchymode) property.
The below are the type of filter mode available in TreeGrid.

* **Parent** : This is the default filter hierarchy mode in TreeGrid. The filtered records are displayed with its parent records, if the filtered records not have any parent record then the filtered records only displayed.

* **Child** : The filtered records are displayed with its child record, if the filtered records not have any child record then the filtered records only displayed.

* **Both** : The filtered records are displayed with its both parent and child record, if the filtered records not have any parent and child record then the filtered records only displayed.

* **None** : The filtered records are only displayed.

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { ChangeEventArgs } from '@syncfusion/ej2-angular-dropdowns';
import { TreeGridComponent  } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<div style="padding-top: 7px; display: inline-block">Hierarchy Mode<ejs-dropdownlist (change)='onChange($event)' [dataSource]='dropData' value='Parent' [fields]='fields'></ejs-dropdownlist></div>
    <ejs-treegrid #treegrid [dataSource]='data' height='210' [treeColumnIndex]='1' [allowFiltering]='true'  childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' type='date' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public dropData: Object[];
    public fields: Object;
     @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
        this.dropData = [
        { id: 'Parent', mode: 'Parent' },
        { id: 'Child', mode: 'Child' },
        { id: 'Both', mode: 'Both' },
        { id: 'None', mode: 'None' },
    ];
    this.fields = { text: 'mode', value: 'id' };
    }
        onChange(e: ChangeEventArgs): any {
        let mode: any = <string>e.value;
        this.treeGridObj.filterSettings.hierarchyMode = mode;
        this.treeGridObj.clearFiltering();
    }
}

```

{% endtab %}

## Initial filter

To apply the filter at initial rendering, set the filter `predicate` object in
[`filterSettings.columns`](../api/treegrid/filterSettingsModel/#columns).

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='275' [treeColumnIndex]='1'  [allowFiltering]='true' [filterSettings]="filterSettings" childMapping='subtasks' >
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
    public filterSettings: Object;

    ngOnInit(): void {
        this.data = sampleData;
        this.filterSettings={
        columns: [{ field: 'taskName', matchCase: false, operator: 'startswith', predicate: 'and', value: 'plan' },
        { field: 'duration', matchCase: false, operator: 'equal', predicate: 'and', value: 5 }]
    };
    }
}

```

{% endtab %}

## Filter operators

The filter operator for a column can be defined in the `filterSettings.columns.operator` property.

The available operators and its supported data types are:

Operator |Description |Supported Types
-----|-----|-----
startswith |Checks whether the value begins with the specified value. |String
endswith |Checks whether the value ends with the specified value. |String
contains |Checks whether the value contains the specified value. |String
equal |Checks whether the value is equal to the specified value. |String &#124; Number &#124; Boolean &#124; Date
notequal |Checks for values not equal to the specified value. |String &#124; Number &#124; Boolean &#124; Date
greaterthan |Checks whether the value is greater than the specified value. |Number &#124; Date
greaterthanorequal|Checks whether a value is greater than or equal to the specified value. |Number &#124; Date
lessthan |Checks whether the value is less than the specified value. |Number &#124; Date
lessthanorequal |Checks whether the value is less than or equal to the specified value. |Number &#124; Date

> By default, the `filterSettings.columns.operator` value is `equal`.

## Filter bar

By setting the [`allowFiltering`](../api/treegrid/#allowfiltering) to true, the filter bar row will render next to the header, which allows you to filter data. You can filter the records with different expressions depending upon the column type.

 **Filter bar expressions:**

 You can enter the following filter expressions (operators) manually in the filter bar.

Expression |Example |Description |Column Type
-----|-----|-----|-----
= |=value |equal |Number
!= |!=value |notequal |Number
> |>value |greaterthan |Number
< |<value |lessthan |Number
>= |>=value |greaterthanorequal |Number
<=|<=value|lessthanorequal |Number
* |*value |startswith |String
% |%value |endswith |String
N/A |N/A | `Equal` operator will always be used for date filter. |Date
N/A |N/A |`Equal` operator will always be used for Boolean filter. |Boolean

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='275' [treeColumnIndex]='1'  [allowFiltering]='true' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' type='date' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}
```

{% endtab %}

### Filter bar template with custom component

The [`filterBarTemplate`](../api/treegrid/column/#filterbartemplate) is used to add custom components to a particular column, and does the following functions:
* `create`: Creates custom components.
* `write`: Wires events for custom components.

You can check this video to learn about how to use Filter bar template with custom component in Angular TreeGrid.

`youtube:LZQjc7DFni4`

In the following sample, the dropdown is used as a custom component in the Duration column.

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { DropDownList, ChangeEventArgs } from '@syncfusion/ej2-dropdowns';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='275' [treeColumnIndex]='1' [allowFiltering]='true' [filterSettings]="filterSettings" childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=150></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' type='date' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration' [filterBarTemplate]="filterBarTemplate" textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public filterSettings: Object;
    public filterBarTemplate: Object;
     @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
        this.filterSettings = { type: 'FilterBar', hierarchyMode: 'Parent', mode: 'Immediate' };
        this.filterBarTemplate = {
                create: (args: { element: Element, column: Column }) => {
                    let dd: HTMLInputElement = document.createElement('input');
                    dd.id = 'duration';
                    return dd;
                },
                write: (args: { element: Element, column: Column }) => {
                    let dataSource: string[] = ['All', '1', '3', '4', '5', '6', '8', '9'];
                    this.dropDownFilter = new DropDownList({
                        dataSource: dataSource,
                        value: 'All',
                        change: (e: ChangeEventArgs) => {
                            let valuenum: any = +e.value;
                            let id: any = <string>this.dropDownFilter.element.id;
                            let value: any = <string>e.value;
                            if ( value !== 'All') {
                                this.treeGridObj.filterByColumn( id, 'equal', valuenum );
                            } else {
                                this.treeGridObj.removeFilteredColsByField(id);
                            }
                        }
                    });
                    this.dropDownFilter.appendTo('#duration');
                }
            }
    }
}


```

{% endtab %}

### Change default Filter bar operator

You can change the default filter operator by extending [`filterModule.filterOperators`](../api/treegrid/filterSettings/#operators) property in [`dataBound`](../api/treegrid/#databound) event. In the following sample, we have changed the default operator for string typed columns as `contains` from `startsWith`.

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { TreeGridComponent  } from '@syncfusion/ej2-angular-treegrid';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='275' [treeColumnIndex]='1' [allowFiltering]='true' (dataBound)='dataBound($event)' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=150></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' type='date' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration'  textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {
    public data: Object[];
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;
    dataBound(args) {
    Object.assign((this.treeGridObj.grid.filterModule as any).filterOperators, { startsWith: 'contains' });
    }
    ngOnInit(): void {
        this.data = sampleData;
    }
}

```

{% endtab %}

## Filter menu

You can enable filter menu by setting the [`filterSettings.type`](../api/treegrid/filterSettingsModel/#type) as `Menu`. The filter menu UI will be rendered based on its column type, which allows you to filter data.
You can filter the records with different operators.

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='275' [allowFiltering]='true' [filterSettings]="filterSettings" childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=150></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' type='date' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public filterSettings: Object;
    ngOnInit(): void {
        this.data = sampleData;
        this.filterSettings = {type: 'Menu'};
    }
}
```

{% endtab %}

> * [`allowFiltering`](../api/treegrid/#allowfiltering) must be set as true to enable filter menu.
> * Setting [`columns.allowFiltering`](../api/treegrid/column/#allowfiltering) as false will prevent filter menu rendering for a particular column.

### Custom component in filter menu

The [`column.filter.ui`](../api/treegrid/column/#filter) is used to add custom filter components to a particular column. To implement custom filter ui, define the following functions:

* `create`:  Creates custom component.
* `write`: Wire events for custom component.
* `read`: Read the filter value from custom component.

In the following sample, dropdown is used  as custom component in the duration column.

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { DataManager } from '@syncfusion/ej2-data';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { createElement } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='275' [allowFiltering]='true' [filterSettings]="filterSettings" childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=150></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' type='date' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration' [filter]='filterui' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public filterSettings: Object;
    public filterui: Object;

    ngOnInit(): void {
        this.data = sampleData;
        this.filterSettings = {type: 'Menu'};
        this.filterui = {
                ui: {
                    create: (args: { target: Element, column: Object }) => {
                        let flValInput: HTMLElement = createElement('input', { className: 'flm-input' });
                        args.target.appendChild(flValInput);
                        let dataSource: string[] = ['All', '1', '3', '4', '5', '6', '8', '9'];
                        this.dropDownFilter = new DropDownList({
                            dataSource: dataSource,
                            value: 'All', popupHeight: '200px'
                        });
                        this.dropDownFilter.appendTo(flValInput);
                    },
                    write: (args: {
                        column: Object, target: Element, parent: any,
                        filteredValue: number | string
                    }) => {
                        this.dropDownFilter.value = args.filteredValue;
                    },
                    read: (args: { target: Element, column: any, operator: string, fltrObj: Filter }) => {
                        args.fltrObj.filterByColumn(args.column.field, args.operator, parseInt(this.dropDownFilter.value));

                    }
                }}
    }
}
```

{% endtab %}

### Enable different filter for a column

You can use both `Menu` and `Excel` filter in a same TreeGrid. To do so, set the
[`column.filter.type`](../api/treegrid/column/#filter) as `Menu` or `Excel`.

In the following sample menu filter is enabled by default and excel filter is enabled for the Task Name column using the
[`column.filter.type`](../api/treegrid/column/#filter).

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { FilterSettingsModel, IFilter } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='273' [allowFiltering]='true' childMapping='subtasks' [filterSettings]='filterOptions'>
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=80></e-column>
                    <e-column field='taskName' headerText='Task Name' [filter] = 'filter' textAlign='Left' width=150></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public filterOptions: FilterSettingsModel;
    public filter : IFilter;

    ngOnInit(): void {
        this.data = sampleData;
        this.filterOptions = {
           type: 'Menu'
        };
        this.filter = {
            type : 'Excel';
        }
    }
    }
}

```

{% endtab %}

## Excel like filter

You can enable Excel like filter by defining.
[`filterSettings.type`](../api/treegrid/filterSettingsModel/#type) as `Excel`.The excel menu contains an option such as Sorting, Clear filter, Sub menu for advanced filtering.

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='273' [allowFiltering]='true' [filterSettings]="filterSettings" childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=150></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' type='date' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public filterSettings: Object;
    ngOnInit(): void {
        this.data = sampleData;
        this.filterSettings = {type: 'Excel'};
    }
}
```

{% endtab %}

### Custom component in Excel Filter

The [`columns.filterTemplate`](../api/treegrid/column/#filtertemplate) property is used to define custom component in excel filter for a particular column.

The following example demonstrates the way to use filter template for a column when using excel filter. In the following example, the `DropdownList` component is used to filter `taskName` column using filter template.

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { DataUtil } from '@syncfusion/ej2-data';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' (created) = 'created($event)' [treeColumnIndex]='1' height='275' [allowFiltering]='true' [filterSettings]="filterSettings" childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=150>
                     <ng-template #filterTemplate let-data>
                            <ejs-dropdownlist id='dropdown' [dataSource]='dropdata'
                             [fields]='fields' [popupHeight]='height'></ejs-dropdownlist>
                       </ng-template>
                    </e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' type='date' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {
    @ViewChild('treegrid')
    public treegrid: TreeGridComponent;
    public data: Object[];
    public filterSettings: Object;
    public dropdata: string[] = [];
    public fields: object = { text: 'taskName', value: 'taskName' };
    public height = '220px';
    ngOnInit(): void {
        this.data = sampleData;
        this.filterSettings = {type: 'Excel'};
    }
    created(args: any): void{
        this.dropdata = DataUtil.distinct(this.treegrid.grid.dataSource, 'taskName') as string[];
    }
}
```

{% endtab %}

### Change default Excel Filter operator

You can change the default excel-filter operator by changing the column operator as `contains` from `startsWith` in the [`actionBegin`](../api/treegrid/#actionBegin) event

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='275' [treeColumnIndex]='1' [allowFiltering]='true' [filterSettings]="filterSettings" (actionBegin)='actionBegin($event)' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=150></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' type='date' format='yMd' width=120></e-column>
                    <e-column field='duration' headerText='Duration'  textAlign='Right' width=120></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {
    public data: Object[];
    public filterSettings: Object;
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;
    actionBegin(e) {
     if(e.requestType === 'filtersearchbegin' && e.column.type === "string")
     {
        e.operator = 'contains';
      }
    }
    ngOnInit(): void {
        this.data = sampleData;
        this.filterSettings = {type: 'Excel'};

    }
}

```

{% endtab %}

## Diacritics

By default, treegrid ignores diacritic characters while filtering. To include diacritic characters, set the
[`filterSettings.ignoreAccent`](../api/treegrid/filterSettingsModel/#ignoreaccent) as `true`.

In the following sample, type **aero** in `Name` column to filter diacritic characters.

{% tab template="treegrid/filtering", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { diacritics } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='0' height='275' [allowFiltering]='true' [filterSettings]='filterSettings'childMapping='Children' >
        <e-columns>
                    <e-column field='EmpID' headerText='Employee ID' textAlign='Right' width=90></e-column>
                    <e-column field='Name' headerText='Name' textAlign='Left' width=180></e-column>
                    <e-column field='DOB' headerText='DOB' textAlign='Right' type='date' format='yMd' width=90></e-column>
                    <e-column field='Country' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public filterSettings: Object:

    ngOnInit(): void {
        this.data = diacritics;
        this.filterSetings = { ignoreAccent: true };
    }
}

```

{% endtab %}