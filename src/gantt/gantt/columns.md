---
title: "Columns"
component: "Gantt"
description: "Documentation on column reordering, resizing, header templates (custom header content), and column templates (custom cell content) in the Essential JS 2 Gantt component."
---

# Columns

The column displays information from a bound data source, and you can edit the values of column to update the task details through TreeGrid. The operations such as sorting, filtering, and searching can be performed based on column definitions. To display a Gantt column, the [`field`](../api/gantt/column/#field) property should be mapped from the data source to the column.

> If the column [`field`](../api/gantt/column/#field) is not specified in the dataSource, the column values will be empty.

The [`treeColumnIndex`](../api/gantt/#treecolumnindex) property is used to define the expander column in the Gantt component to expand and collapse the child rows.

## Defining columns

Using the [`columns`](../api/gantt/#columns) property, you can define the columns in Gantt. If the columns are not defined, then the default columns will be rendered based on the mapped data source fields in the [`taskFields`](../api/gantt/#taskfields) property. Refer to the following code example for defining the columns in Gantt along with their widths.

{% tab template="gantt/columns/default",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns"  [splitterSettings] = "splitterSettings"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = [
        {
            TaskID: 1,
            TaskName: 'Project Initiation',
            StartDate: new Date('04/02/2019'),
            EndDate: new Date('04/21/2019'),
            subtasks: [
                { TaskID: 2, TaskName: 'Identify Site location', StartDate: new Date('04/02/2019'), Duration: 4, Progress: 50 },
                { TaskID: 3, TaskName: 'Perform Soil test', StartDate: new Date('04/02/2019'), Duration: 4, Progress: 50  },
                { TaskID: 4, TaskName: 'Soil test approval', StartDate: new Date('04/02/2019'), Duration: 4, Progress: 50 },
            ]
        },
        {
            TaskID: 5,
            TaskName: 'Project Estimation',
            StartDate: new Date('04/02/2019'),
            EndDate: new Date('04/21/2019'),
            subtasks: [
                { TaskID: 6, TaskName: 'Develop floor plan for estimation', StartDate: new Date('04/04/2019'), Duration: 3, Progress: 50 },
                { TaskID: 7, TaskName: 'List materials', StartDate: new Date('04/04/2019'), Duration: 3, Progress: 50 },
                { TaskID: 8, TaskName: 'Estimation approval', StartDate: new Date('04/04/2019'), Duration: 3, Progress: 50 }
            ]
        },
    ];
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', width: '150' },
            { field: 'TaskName', width: '250' }
        ];
        this.splitterSettings = {
            columnIndex:2
            };
        }
}

```

{% endtab %}

## Custom column header

The column header text can be defined using the [`headerText`](../api/gantt/column/#headertext) property, and you can customize the column headers using the [`headerTemplate`](../api/gantt/column/#headertemplate) property.

{% tab template="gantt/columns/headertemplate",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [splitterSettings] = "splitterSettings" [taskFields]="taskSettings">
       <e-columns>
            <e-column field='TaskName' width='150'><ng-template #headerTemplate>
        <div>
            <img src="taskname.png" width="20" height="20" class="e-image" />  Task Name
        </div></ng-template> </e-column>
         <e-column field='StartDate' width='150'><ng-template #headerTemplate>
        <div>
            <img src="startdate.png" width="20" height="20" class="e-image" />  Start Date
        </div></ng-template> </e-column>
         <e-column field='Duration' width='150'><ng-template #headerTemplate>
        <div>
            <img src="duration.png" width="20" height="20" class="e-image" />  Duration
        </div></ng-template> </e-column>
         <e-column field='Progress' width='150'><ng-template #headerTemplate>
        <div>
            <img src="progress.png" width="20" height="20" class="e-image" />  Progress
        </div></ng-template> </e-column>
        </e-columns>
       </ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public columns: object[];
    public splitterSettings: object;
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '250' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
            columnIndex:4
            };
    }
}

```

{% endtab %}

## Format

To format the cell values based on a specific culture, use the [`columns.format`](../api/gantt/column/#format) property. The Gantt component uses the [`Internationalization`](../../common/internationalization/) library to format `number` and `date` values.

{% tab template="gantt/columns/format",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [rowHeight]="50" [splitterSettings] = "splitterSettings"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = editingData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'Progress', headerText: 'Progress', width: '150',format: 'C' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' }
        ];
        this.splitterSettings = {
            columnIndex:3
            };
    }
}

```

{% endtab %}

> By default, the number and date values are formatted in `en-US` culture.

### Number formatting

The number or integer values can be formatted using the following format strings.

Format |Description |Remarks
-----|-----
N | Denotes numeric type. | The numeric format is followed by integer value as N2, N3. etc which denotes the number of precision to be allowed.
C | Denotes currency type. | The currency format is followed by integer value as C2, C3. etc which denotes the number of precision to be allowed.
P | Denotes percentage type | The percentage format expects the input value to be in the range of 0 to 100. For example the cell value `0.2` is formatted as `20%`. The percentage format is followed by integer value as P2, P3. etc which denotes the number of precision to be allowed.

### Date formatting

You can format date values either using built-in date format string or custom format string.

For the built-in date format, you can specify the [`columns.format`](../api/gantt/column/#format) property as string (example: `yMd`).

You can also use the custom format string to format the date values. Some of the custom formats and the formatted date values are given in the following table.

Format | Formatted value
-----|-----
{ type:'date', format:'dd/MM/yyyy' } | 04/07/1996
{ type:'date', format:'dd.MM.yyyy' } | 04.07.1996
{ type:'date', skeleton:'short' } | 7/4/96
{ type: 'dateTime', format: 'dd/MM/yyyy hh:mm a' } | 04/07/1996 12:00 AM
{ type: 'dateTime', format: 'MM/dd/yyyy hh:mm:ss a' } | 07/04/1996 12:00:00 AM

{% tab template="gantt/columns/dateformat",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [rowHeight]="50" [splitterSettings] = "splitterSettings"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = editingData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150', format: { format: 'dd/MM/yyyy', type: 'date' } },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150',format: 'C' },
        ];
        this.splitterSettings = {
            columnIndex:3
            };
    }
}

```

{% endtab %}

## Column reordering

The column reordering can be done by dragging a column header from one index to another index within the TreeGrid. To enable reordering, set the [`allowReordering`](../api/gantt/#allowreordering) property to `true`.

To reorder the columns, inject the `ReorderService` in the provider section of `AppModule`.

{% tab template="gantt/columns/reorder",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [splitterSettings] = "splitterSettings" [allowReordering] = 'true'></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
            columnIndex:4
            };
    }
}

```

{% endtab %}

> You can disable the reordering of a particular column by setting the [`columns.allowReordering`](../api/gantt/column/#allowreordering) property to `false`.

## Reorder multiple columns

Multiple columns can be reordered at a time by using the [`reorderColumns`](../api/gantt/column/#reordercolumns) method.

{% tab template="gantt/columns/reordermultiple",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { GanttComponent } from '@syncfusion/ej2-angular-gantt';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<button ejs-button id='reordercolumns' (click)='reorderColumns()'>Reorder Multiple Columns</button>
       <br><br><br>
       <ejs-gantt #gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [splitterSettings] = "splitterSettings" [allowReordering] = 'true'></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    @ViewChild('gantt', {static: true})
    public ganttObj: GanttComponent;
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
            columnIndex:4
            };
    };
    reorderColumns(): void {
        this.ganttObj.reorderColumns('TaskName'  ,'Progress');
        };
}

```

{% endtab %}

## Reorder Events

During the reorder action, the gantt component triggers the below three events.

1. The [`columnDragStart`](../api/gantt/#columndragstart) event triggers when column header element drag (move) starts.
2. The [`columnDrag`](../api/gantt/#columndrag) event triggers when column header element is dragged (moved) continuously.
3. The [`columnDrop`](../api/gantt/#columndrop) event triggers when a column header element is dropped on the target column.

{% tab template="gantt/columns/reorder-events",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { GanttComponent } from '@syncfusion/ej2-angular-gantt';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt #gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [splitterSettings] = "splitterSettings" [allowReordering] = 'true'
       (columnDragStart)="columnDragStart()" (columnDrag)="columnDrag()" (columnDrop)="columnDrop()"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    @ViewChild('gantt', {static: true})
    public ganttObj: GanttComponent;
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
            columnIndex:4
            };
    };
     columnDrop() {
        alert('columnDrop event is Triggered');
    }
    columnDragStart() {
        alert('columnDragStart event is Triggered');
    }
    columnDrag() {
        alert('columnDrag event is Triggered');
    }
}

```

{% endtab %}

## Column resizing

The column width can be resized by clicking and dragging the right edge of the column header. While dragging, the width of the column will be resized immediately. Each column can be auto resized by double-clicking the right edge of the column header to fit the width of that column based on the widest cell content. To resize the column, set the [`columns.allowResizing`](../api/gantt/column/#allowresizing) property to `true`. The following code example shows how to enable the column resize feature in the Gantt component.

To resize the column, inject the `ResizeService` in the provider section of `AppModule`.

{% tab template="gantt/columns/resize",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [splitterSettings] = "splitterSettings" [allowResizing] = 'true'></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
            columnIndex:4
            };
    }
}

```

{% endtab %}

> You can disable resizing for a particular column by setting the [`columns.allowResizing`](../api/gantt/column/#allowresizing) to `false`.

### Defining minimum and maximum column width

The column resizing can be restricted between minimum and maximum widths by defining the [`columns->minWidth`](../api/gantt/column/#minwidth) and [`columns->maxWidth`](../api/gantt/column/#maxwidth) properties.

In the following example, the minimum and maximum widths are defined for the `Duration`, and `Task Name` columns.

{% tab template="gantt/columns/min-max",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [splitterSettings] = "splitterSettings" [allowResizing] = 'true'></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '200',minWidth: '150' ,maxWidth: '250',},
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '100',minWidth: '50' ,maxWidth: '200' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
            columnIndex:4
            };
    }
}

```

{% endtab %}

## Column template

A column template is used to customize the column’s look. The following code example explains how to define the custom template in Gantt using the [`template`](../api/gantt/column/#template) property.

{% tab template="gantt/columns/columntemplate",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingResources } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [allowResizing] = 'true' rowHeight='50' [splitterSettings]="splitterSettings" [resourceFields]="resourceFields" [resources]="resources">
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' textAlign= 'Left' width= 100></e-column>
                <e-column field='TaskName' headerText= 'Task Name' width= 150></e-column>
                <e-column field= 'resources' headerText= 'Resources' width= 250>
                <ng-template #template let-data>
                 <div *ngIf="data.ganttProperties.resourceNames">
                <img src="{{data.TaskID}}.png" style="height:40px;width:40px"/>{{data.ganttProperties.resourceNames}}
                </div>
                </ng-template>
                </e-column>
                <e-column field= 'StartDate' headerText='Start Date' width= 150 ></e-column>
                <e-column field= 'Duration' headerText='Duration' width= 150 ></e-column>
                <e-column field= 'Progress' headerText= 'Progress' width= 150 ></e-column>
            </e-columns></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public resources: object[];
    public resourceFields: object;
    public ngOnInit(): void {
        this.data = [
    {
        TaskID: 1,
        TaskName: 'Project Initiation',
        StartDate: new Date('04/02/2019'),
        EndDate: new Date('04/21/2019'),
        subtasks: [
            {
                TaskID: 2, TaskName: 'Identify Site location', StartDate: new Date('04/02/2019'), Duration: 0,
                Progress: 30, resources: [1], info: 'Measure the total property area alloted for construction'
            },
            {
                TaskID: 3, TaskName: 'Perform Soil test', StartDate: new Date('04/02/2019'), Duration: 4, Predecessor: '2',
                resources: [2, 3, 5], info: 'Obtain an engineered soil test of lot where construction is planned.' +
                    'From an engineer or company specializing in soil testing'
            },
            { TaskID: 4, TaskName: 'Soil test approval', StartDate: new Date('04/02/2019'), Duration: 0, Predecessor: '3', Progress: 30, resources: [9, 11], },
        ]
    },
    {
        TaskID: 5,
        TaskName: 'Project Estimation',
        StartDate: new Date('04/02/2019'),
        EndDate: new Date('04/21/2019'),
        subtasks: [
            {
                TaskID: 6, TaskName: 'Develop floor plan for estimation', StartDate: new Date('04/04/2019'),
                Duration: 3, Predecessor: '4', Progress: 30, resources: [4],
                info: 'Develop floor plans and obtain a materials list for estimations'
            },
            {
                TaskID: 7, TaskName: 'List materials', StartDate: new Date('04/04/2019'),
                Duration: 3, Predecessor: '6', resources: [4, 8], info: ''
            },
            {
                TaskID: 8, TaskName: 'Estimation approval', StartDate: new Date('04/04/2019'),
                Duration: 0, Predecessor: '7', info: ''
            }
        ]
    },
            ];
        this.taskSettings = {
             id: 'TaskID',
            name: 'TaskName',
            resourceInfo: 'resources',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks',
        };
        this.splitterSettings = {
            columnIndex:4
            };
        this.resourceFields = {
            id: 'resourceId',
            name: 'resourceName'
        };
        this.resources = editingResources;
    }
}

```

{% endtab %}

## Column menu

The column menu has options to integrate features like sorting, filtering, and autofit. It will show a menu with the integrated feature when users click the Multiple icon of the column. To enable the column menu, you should set the [`showColumnMenu`](../api/gantt/#showcolumnmenu) property to `true`.

The default items are displayed in the following table:

| Item | Description |
|-----|-----|
| `SortAscending` | Sort the current column in ascending order. |
| `SortDescending` | Sort the current column in descending order. |
| `AutoFit` | Auto fit the current column. |
| `AutoFitAll` | Auto fit all columns. |
| `Filter` | Show the filter option as given in `filterSettings.type` |

{% tab template="gantt/columns/columnmenu",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [allowFiltering] = 'true' [showColumnMenu] = 'true' [allowSorting] = 'true' [splitterSettings]="splitterSettings"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
             position: '100%'
            };
    }
}

```

{% endtab %}

> You can disable the column menu for a particular column by setting the [`columns.showColumnMenu`](../api/gantt/#showcolumnmenu) to false.

### Column menu events

During the resizing action, the gantt component triggers the below two events.

1. The [`columnMenuOpen`](../api/gantt/#columnmenuopen) event triggers before the column menu opens.
2. The [`columnMenuClick`](../api/gantt/#columnmenuclick) event triggers when the user clicks the column menu of the gantt.

{% tab template="gantt/columns/columnmenu-events",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';
import { MenuEventArgs } from '@syncfusion/ej2-navigations';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [allowFiltering] = 'true' [showColumnMenu] = 'true' [allowSorting] = 'true' [splitterSettings]="splitterSettings" (columnMenuOpen)="columnMenuOpen()" (columnMenuClick)="columnMenuClick()"
       ></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
             position: '100%'
        };
    };
     columnMenuOpen() {
            alert('columnMenuOpen event is Triggered');
        }
    columnMenuClick() {
        alert('columnMenuClick event is Triggered');
    }
}

```

{% endtab %}

### Custom Column Menu Item

Custom column menu items can be added by defining the [`columnMenuItems`](../api/gantt/#columnmenuitems).
Actions for this customized items can be defined in the [`columnMenuClick`](../api/gantt/#columnmenuclick) event.

{% tab template="gantt/columns/columnmenu-cust-item",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';
import { MenuEventArgs } from '@syncfusion/ej2-navigations';
import { GanttComponent } from '@syncfusion/ej2-angular-gantt';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" #gantt height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [allowFiltering] = 'true' [allowResizing] = 'true' [showColumnMenu] = 'true' [allowSorting] = 'true' [splitterSettings]="splitterSettings" [sortSettings]='sortSettings'
       [columnMenuItems]='columnMenuItems' (columnMenuClick)='columnMenuClick($event)'></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    @ViewChild('gantt')
    public gantt: GanttComponent;
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public columnMenuItems: any = [{ text: 'Clear Sorting', id: 'ganttclearsorting' }];
    public sortSettings: any =  {columns: [{direction: 'Ascending', field: 'TaskID'}]};
    public columnMenuClick(args: MenuEventArgs) {
        if (args.item.id === 'ganttclearsorting') {
            this.gantt.clearSorting();
        }
    }
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
             position: '75%'
        };
    }
}

```

{% endtab %}

### Customize menu items for particular columns

Sometimes, you have a scenario that to hide an item from column menu for particular columns. In that case, you need to define the [`columnMenuOpenEventArgs.hide`](../api/grid/columnMenuOpenEventArgs) as true in the [`columnMenuOpen`](../api/gantt/#columnmenuopen) event.

The following sample, **Filter** item was hidden in column menu when opens for the **Task Name** column.

{% tab template="gantt/columns/columnmenu-cust-action",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';
import { ColumnMenuOpenEventArgs, ColumnMenuItemModel } from '@syncfusion/ej2-grids';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" #gantt height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [allowFiltering] = 'true' [allowResizing] = 'true' [showColumnMenu] = 'true' [allowSorting] = 'true' [splitterSettings]="splitterSettings" [sortSettings]='sortSettings'
       (columnMenuOpen)='columnMenuOpen($event)'></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public columnMenuOpen(args: ColumnMenuOpenEventArgs) {
        for (const item of args.items) {
            if (item.text === 'Filter' && args.column.field === 'TaskName') {
                (item as ColumnMenuItemModel).hide = true;
            } else {
                (item as ColumnMenuItemModel).hide = false;
            }
        }
    }
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
             position: '75%'
        };
    }
}

```

{% endtab %}

## Responsive columns

You can toggle the column visibility based on media queries, which are defined in the [`hideAtMedia`](../api/gantt/column/#hideatmedia). The [`hideAtMedia`](../api/gantt/column/#hideatmedia) accepts valid [Media Queries]( http://cssmediaqueries.com/what-are-css-media-queries.html ).

{% tab template="gantt/columns/responsivecolumn",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [columns]="columns" [splitterSettings] = "splitterSettings" [allowResizing] = 'true'></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public columns: object[];
    public splitterSettings: object;
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.splitterSettings = {
            columnIndex:3
            };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '200',hideAtMedia: '(min-width: 700px)'},
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '100', hideAtMedia: '(max-width: 500px)'},
            { field: 'Progress', headerText: 'Progress', width: '150' }
        ];
    }
}

```

{% endtab %}

## Change tree/expander column

The tree/expander column is a column in the Gantt component, that has icons to expand or collapse the parent records. You can define the tree column index in the Gantt component by using the [`treeColumnIndex`](../api/gantt/#treecolumnindex) property and the default value of this property is `0`. The following code example shows how to use this property.

{% tab template="gantt/columns/treecolumn",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data"  [taskFields]="taskSettings" [treeColumnIndex]='2' [splitterSettings] = "splitterSettings" [allowResizing] = 'true'></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.splitterSettings = {
            columnIndex:3
            };
    }
}

```

{% endtab %}

## Show or Hide columns dynamically

You can show or hide gantt columns dynamically using external buttons by invoking the [`showColumn`](../api/gantt/#showcolumn) or [`hideColumn`](../api/gantt/#hidecolumn) method.

{% tab template="gantt/columns/showhide",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';
import { GanttComponent } from '@syncfusion/ej2-angular-gantt';

@Component({
    selector: 'app-root',
    template:
       `<button ejs-button id='show' (click)='show()'>Show</button>
       <button ejs-button id='hide' (click)='hide()'>Hide</button>
       <br><br><br>
       <ejs-gantt id="ganttDefault" #gantt height="430px" [dataSource]="data" [taskFields]="taskSettings" [columns]="columns" [splitterSettings] = "splitterSettings"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    @ViewChild('gantt')
    public gantt: GanttComponent;
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
             position: '75%'
        };
    }
     show(): void {
        this.gantt.showColumn(['Duration']); // show by HeaderText
    }

    hide(): void {
        this.gantt.hideColumn(['Duration']); // hide by HeaderText
    }
}

```

{% endtab %}

## Checkbox Column

To render boolean values as checkbox in columns, you need to set [`displayAsCheckBox`](../api/gantt/column/#displayascheckbox) property as **true**.

{% tab template="gantt/columns/checkbox",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { GanttData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" #gantt height="430px" [dataSource]="data" [taskFields]="taskSettings" [columns]="columns" [splitterSettings] = "splitterSettings"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public ngOnInit(): void {
        this.data = GanttData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks',
            verified: 'verified'
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'verified', headerText: 'Verified', displayAsCheckBox: true, type: 'boolean' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.splitterSettings = {
            columnIndex: 5
        };
    }
}

```

{% endtab %}

## Controlling Grid actions

You can enable or disable gantt action for a particular column by setting the [`allowFiltering`](../api/gantt/#allowfiltering), [`allowSorting`](../api/gantt/#allowsorting), [`allowReordering`](../api/gantt/#allowreordering), and [`allowEditing`](../api/gantt/#editsettings) properties.

{% tab template="gantt/columns/gridactions",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';
import { EditSettingsModel } from '@syncfusion/ej2-angular-gantt';


@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" #gantt height="430px" [dataSource]="data" [taskFields]="taskSettings" [columns]="columns" [splitterSettings]="splitterSettings" [editSettings]="editSettings"
       [allowFiltering]='true' [allowResizing]='true' [allowSorting]='true' [allowReordering] = 'true'></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public editSettings: EditSettingsModel;
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.editSettings = {
            allowEditing: true
        };
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID' },
            { field: 'Progress', headerText: 'Progress', allowReordering: false },
            { field: 'TaskName', headerText: 'Task Name', allowSorting: false },
            { field: 'StartDate', headerText: 'Start Date', allowEditing: false },
            { field: 'Duration', headerText: 'Duration', allowFiltering: false }
        ];
        this.splitterSettings = {
            columnIndex: 5
        };
    }
}

```

{% endtab %}

## Column type

Column type can be specified using the `columns.type` property. It specifies the type of data the column binds.

If the `format` is defined for a column, the column uses `type` to select the appropriate format option [number](../common/internationalization/#number-formatting) or [date](../common/internationalization/#manipulating-datetime).

Gantt column supports the following types:
* string
* number
* boolean
* date
* datetime

> If the `type` is not defined, it will be determined from the first record of the [`dataSource`](../api/gantt/#datasource).
> In case if the first record of the [`dataSource`](../api/gantt/#datasource) is null/blank value for a column then it is necessary to define the `type` for that column.

## Column Spanning

The gantt has option to span the adjacent cells. You need to define the [`colSpan`](../api/gantt/queryCellInfoEventArgs/#colspan) attribute to span cells in the [`QueryCellInfo`](../api/gantt/queryCellInfoEventArgs) event.

In the following demo, **Work1**  cells have been spanned.

{% tab template="gantt/columns/columnspan",sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewEncapsulation } from '@angular/core';
import { QueryCellInfoEventArgs } from '@syncfusion/ej2-angular-gantt';
import { Gantt } from '@syncfusion/ej2-gantt';
import { GanttData } from './data';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings" [columns]="columns" [splitterSettings]="splitterSettings" [gridLines]='gridLines'
       (queryCellInfo)='queryCellInfoEvent($event)'></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public splitterSettings: object;
    public columns: object[];
    public gridLines: string;
    public queryCellInfoEvent: EmitType<QueryCellInfoEventArgs> = (args: QueryCellInfoEventArgs) => {
        switch(args.data.TaskID) {
            case 1:
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan = 2;
            }
            break;
            case 2:
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan = 2;
            }
            break;
            case 3:
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan = 2;
            }
            break;
            case 4:
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan = 2;
            }
            break;
            case 5  :
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan = 2;
            }
            break;
            case 7:
            if ((args.column.field == 'work1') && (args.data.taskData.work1 == 'support')) {
                args.colSpan = 2;
            }
            break;
        }
    }
    public ngOnInit(): void {
        this.data = GanttData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks',
            work1: 'work1',
            work2: 'work2',
        };
        this.gridLines = 'Both';
        this.columns =  [
            { field: 'TaskID', headerText: 'Task ID' },
            { field: 'TaskName', headerText: 'Task Name' },
            { field: 'work1', headerText: 'Work 1' },
            { field: 'work2', headerText: 'Work 2' },
            { field: 'StartDate', headerText: 'Start Date' },
            { field: 'Duration', headerText: 'Duration' },
            { field: 'Progress', headerText: 'Progress' }
        ];
        this.splitterSettings = {
            columnIndex: 5
        };
    }
}

```

{% endtab %}