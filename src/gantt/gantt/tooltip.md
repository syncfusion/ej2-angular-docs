---
title: "Tooltip"
component: "Gantt"
description: "Learn how to enable the tooltip for the task's in the Essential JS 2 Gantt component."
---

# Tooltip

The Gantt component has a support to display a tooltip for various UI elements like taskbar, timeline cells, and grid cells.

## Enable tooltip

In the Gantt component, you can enable or disable the mouse hover tooltip for the following UI elements using the [`tooltipSettings.showTooltip`](../api/gantt/tooltipSettings/#showtooltip) property:

* Taskbar
* Connector line
* Baseline
* Event marker

{% tab template="gantt/tooltip/default",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings" [renderBaseline]="true" [treeColumnIndex]="1" height="450px" baselineColor='red' [tooltipSettings]="tooltipSettings" [eventMarkers]="eventMarkers"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: Object[];
    public taskSettings: object;
    public columns: object[];
    public timelineSettings: object;
    public labelSettings: object;
    public tooltipSettings: object;
    public eventMarkers : object[];
    public dayWorkingTime: object[];
    public ngOnInit(): void {
        this.data =  [
        {
            TaskID: 1,
            TaskName: 'Project Initiation',
            StartDate: new Date('04/02/2019'),
            EndDate: new Date('04/21/2019'),
            subtasks: [
                { TaskID: 2, TaskName: 'Identify Site location',BaselineStartDate: new Date('04/02/2019'),BaselineEndDate: new Date('04/02/2019'), StartDate: new Date('04/02/2019'), Duration: 0, Progress: 50 },
                { TaskID: 3, TaskName: 'Perform Soil test', StartDate: new Date('04/02/2019'),BaselineStartDate: new Date('04/04/2019'),BaselineEndDate: new Date('04/09/2019'), Duration: 4, Progress: 50  },
                { TaskID: 4, TaskName: 'Soil test approval', StartDate: new Date('04/02/2019'),BaselineStartDate: new Date('04/08/2019'),BaselineEndDate: new Date('04/12/2019'), Duration: 4,Predecessor:"2FS", Progress: 50 },
            ]
        },
        {
            TaskID: 5,
            TaskName: 'Project Estimation',
            StartDate: new Date('04/02/2019'),
            EndDate: new Date('04/21/2019'),
            subtasks: [
                { TaskID: 6, TaskName: 'Develop floor plan for estimation',BaselineStartDate: new Date('04/04/2019'),BaselineEndDate: new Date('04/08/2019'), StartDate: new Date('04/04/2019'), Duration: 3, Progress: 50 },
                { TaskID: 7, TaskName: 'List materials', StartDate: new Date('04/04/2019'),BaselineStartDate: new Date('04/02/2019'),BaselineEndDate: new Date('04/04/2019'), Duration: 3, Progress: 50 },
                { TaskID: 8, TaskName: 'Estimation approval', StartDate: new Date('04/02/2019'),BaselineStartDate: new Date('04/02/2019'),BaselineEndDate: new Date('04/08/2019'), Duration: 0,Predecessor:"6SS", Progress: 50 }
            ]
        },
    ];
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            baselineStartDate: "BaselineStartDate",
            baselineEndDate: "BaselineEndDate",
            progress: 'Progress',
            dependency: 'Predecessor',
            child: 'subtasks'
        };
        this.tooltipSettings = {
            showTooltip:true
            }
        this.eventMarkers = [
            {
                day: '04/10/2019',
                label: 'Project approval and kick-off'
            }
        ];
    }
}

```

{% endtab %}

> The default value of the [`tooltipSettings.showTooltip`](../api/gantt/tooltipSettings/#showtooltip) property is `true`.

## Timeline cells tooltip

In the Gantt component, you can enable or disable the mouse hover tooltip of timeline cells using the [`timelineSettings.showTooltip`](../api/gantt/timelineSettings/#showtooltip) property. The default value of this property is `true`. The following code example shows how to enable the timeline cells tooltip in Gantt.

{% tab template="gantt/tooltip/timelinecell",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings"  [columns]="columns" [timelineSettings]="timelineSettings"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public columns: object[];
     public timelineSettings: object;

    public ngOnInit(): void {
        this.data = editingData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            endDate: 'EndDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns = [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '250' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
        this.timelineSettings = {
                showTooltip: true
        };
    }
}

```

{% endtab %}

## Cell tooltip

You can enable or disable the Grid cell tooltip using the [`columns.clipMode`](../api/gantt/column/#clipmode) property.

{% tab template="gantt/tooltip/cell",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings"  [columns]="columns"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public columns: object[];

    public ngOnInit(): void {
        this.data = editingData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            endDate: 'EndDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.columns = [
            { field: 'TaskID', headerText: 'Task ID', textAlign: 'Left', width: '100' },
            { field: 'TaskName', headerText: 'Task Name', width: '150', clipMode: 'EllipsisWithTooltip' },
            { field: 'StartDate', headerText: 'Start Date', width: '150' },
            { field: 'Duration', headerText: 'Duration', width: '150',clipMode: 'Clip' },
            { field: 'Progress', headerText: 'Progress', width: '150' },
        ];
    }
}

```

{% endtab %}

### Clip mode

The clip mode provides options to display its overflow cell content and it can be defined by the [`columns.clipMode`](../api/gantt/column/#clipmode) property.

The following are three types of `clipMode`:

* `Clip`: Truncates the cell content when it overflows its area.
* `Ellipsis`: Displays ellipsis when content of the cell overflows its area.
* `EllipsisWithTooltip`: Displays ellipsis when content of the cell overflows its area; it displays the tooltip content when hover over ellipsis.

> NOTE
> By default, all the column's [`clipMode`](../api/gantt/column/#clipmode) property is defined as `EllipsisWithTooltip`.

## Tooltip template

### Taskbar tooltip

The default tooltip in the Gantt component can be customized using the [`tooltipSettings.taskbar`](../api/gantt/tooltipSettings/#taskbar) property.

{% tab template="gantt/tooltip/taskbar",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings"  [columns]="columns" [tooltipSettings]="tooltipSettings">
       <ng-template #tooltipSettingsTaskbar let-data>
        <div> <ng-container>TaskID: {{data.TaskID}}</ng-container> </div>
       </ng-template></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public tooltipSettings: object;

    public ngOnInit(): void {
        this.data = editingData;
        this.taskSettings = {
                id: 'TaskID',
                name: 'TaskName',
                startDate: 'StartDate',
                duration: 'Duration',
                baselineStartDate:"BaselineStartDate",
                baselineEndDate:"BaselineEndDate",
                progress: 'Progress',
                dependency: 'Predecessor',
                child: 'subtasks'
        };
        this.tooltipSettings = {
                showTooltip: true
        };
    }
}

```

{% endtab %}

### Connector line tooltip

The default connector line tooltip in the Gantt component can be customized using the [`tooltipSettings.connectorLine`](../api/gantt/tooltipSettings/#connectorline) property. The following code example shows how to use the [`tooltipSettings.connectorLine`](../api/gantt/tooltipSettings/#connectorline) property.

{% tab template="gantt/tooltip/dependency",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings"  [columns]="columns" [tooltipSettings]="tooltipSettings">
        <ng-template #tooltipSettingsConnectorLine let-data>
       <div> <ng-container> Offset : {{data.offsetString}}</ng-container> </div>
       </ng-template></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public tooltipSettings: object;

    public ngOnInit(): void {
        this.data = editingData;
        this.taskSettings = {
                id: 'TaskID',
                name: 'TaskName',
                startDate: 'StartDate',
                duration: 'Duration',
                progress: 'Progress',
                dependency: 'Predecessor',
                child: 'subtasks'
        };
        this.tooltipSettings = {
                showTooltip: true
        };
    }
}

```

{% endtab %}

### Taskbar editing tooltip

The taskbar editing tooltip can be customized using the [`tooltipSettings.editing`](../api/gantt/tooltipSettings/#editing) property. The following code example shows how to customize the taskbar editing tooltip in Gantt.

{% tab template="gantt/tooltip/taskbar-edit",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingData } from './data';
import { EditSettingsModel } from '@syncfusion/ej2-angular-gantt';
@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings"  [columns]="columns" [editSettings]="editSettings" [tooltipSettings]="tooltipSettings">
       <ng-template #tooltipSettingsEditing let-data>
        <div> <ng-container>Duration : {{data.duration}}</ng-container> </div>
       </ng-template></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public tooltipSettings: object;
    public editSettings: EditSettingsModel;
    public ngOnInit(): void {
        this.data = editingData;
        this.taskSettings = {
                id: 'TaskID',
                name: 'TaskName',
                startDate: 'StartDate',
                duration: 'Duration',
                baselineStartDate:"BaselineStartDate",
                baselineEndDate:"BaselineEndDate",
                progress: 'Progress',
                dependency: 'Predecessor',
                child: 'subtasks'
        };
        this.editSettings = {
            allowEditing:true,
            allowTaskbarEditing:true
            },
        this.tooltipSettings = {
                showTooltip: true
        };
    }
}

```

{% endtab %}

### Baseline tooltip

A baseline tooltip can be customized using the [`tooltipSettings.baseline`](../api/gantt/tooltipSettings/#baseline) property. The following code example shows how to customize the baseline tooltip in Gantt.

{% tab template="gantt/tooltip/baseline",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { baselineData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings" [columns]="columns" [timelineSettings]="timelineSettings" [renderBaseline]="true" [treeColumnIndex]="1" height="450px" [projectStartDate]="projectStartDate" [projectEndDate]="projectEndDate" [dayWorkingTime]="dayWorkingTime" baselineColor='red'>
       <ng-template #tooltipSettingsBaseline let-data>
       <div> <ng-container>Baseline StartDate : {{data.BaselineStartDate}}</ng-container> </div>
       </ng-template></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: Object[];
    public taskSettings: object;
    public columns: object[];
    public timelineSettings: object;
    public labelSettings: object;
    public tooltipSettings: object;
    public projectStartDate: Date;
    public projectEndDate: Date;
    public dayWorkingTime: object[];
    public ngOnInit(): void {
        this.data = baselineData;
        this.taskSettings = {
                id: 'TaskId',
                name: 'TaskName',
                startDate: 'StartDate',
                endDate: 'EndDate',
                baselineStartDate: 'BaselineStartDate',
                baselineEndDate: 'BaselineEndDate'
        };
        this.columns =  [
                { field: 'TaskName', headerText: 'Service Name', width: '250', clipMode: 'EllipsisWithTooltip' },
                { field: 'BaselineStartDate', headerText: 'Planned start time' },
                { field: 'BaselineEndDate', headerText: 'Planned end time' },
                { field: 'StartDate', headerText: 'Start time' },
                { field: 'EndDate', headerText: 'End time' },
            ];
        this.dayWorkingTime = [{ from: 0, to: 24 }];
        this.timelineSettings = {
            timelineUnitSize: 70,
            topTier: {
                unit: 'None',
            },
            bottomTier: {
                unit: 'Minutes',
                count: 15,
                format: 'hh:mm a'
            },
        };
        this.projectStartDate= new Date('03/05/2018 09:30:00 AM');
        this.projectEndDate= new Date('03/05/2018 7:00:00 PM');
        this.tooltipSettings = {
            showTooltip:true
            }
    }
}

```

{% endtab %}