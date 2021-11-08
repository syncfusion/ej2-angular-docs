---
title: "How To"
component: "Gantt"
description: "Learn how to maintain zoomtofit."
---

# Maintain zoomToFit

In the Gantt control, While performing edit actions or dynamically change dataSource, the timeline gets refreshed. When zoomToFit toolbar item is clicked and perform editing actions or dynamically change dataSource, the timeline gets refreshed. So that, the timeline will not fit to the project any more.

## Maintain zoomToFit after edit actions

We can maintain `zoomToFit` after editing actions(cell edit,dialog edit,taskbar edit) by using [`fitToProject`](../api/gantt/#fittoproject) method in `actionComplete` and `taskbarEdited` event.

{% tab template="gantt/how-to/maintainzoomtofit",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit, ViewChild} from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { GanttComponent } from '@syncfusion/ej2-angular-gantt';
import { ToolbarItem, ZoomTimelineSettings, EditSettingsModel  } from '@syncfusion/ej2-angular-gantt';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt #gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings"[toolbar]="toolbar" [editSettings]="editSettings" (actionComplete)="actionComplete($event)" (taskbarEdited)="taskbarEdited($event)"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public toolbar: ToolbarItem[];
    public editSettings: EditSettingsModel;
    @ViewChild('gantt', {static: true})
    public ganttObj: GanttComponent;
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            endDate: 'EndDate',
            duration: 'Duration',
            progress: 'Progress',
            dependency: 'Predecessor',
            child: 'subtasks'
        };
        this.editSettings = {
            allowEditing: true,
            allowTaskbarEditing: true,
        };
        this.toolbar =  ['Edit','ZoomToFit'];
    }
    public actionComplete(args: any) {
      if ((args.action === "CellEditing" || args.action === "DialogEditing") && args.requestType === "save") {
        this.ganttObj.dataSource = projectNewData;
        this.ganttObj.fitToProject();
      }
    };
    public taskbarEdited(args: any) {
      if (args) {
        this.ganttObj.dataSource = projectNewData;
        this.ganttObj.fitToProject();
      }
    };
}

```

{% endtab %}

## Maintain zoomToFit after change dataSource dynamically

We can maintain `zoomToFit` after change dataSource dynamically, by calling [`fitToProject`](../api/gantt/#fittoproject) method in dataBound event.

{% tab template="gantt/how-to/maintainzoomtofitdatasource",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit,  ViewChild } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { GanttComponent } from '@syncfusion/ej2-angular-gantt';
import { ToolbarItem, ZoomTimelineSettings  } from '@syncfusion/ej2-angular-gantt';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';
import { projectNewData, data } from './data';

@Component({
    selector: 'app-root',
    template:
       `<button ejs-button id='changeData' (click)='changeData()'>Change Data</button>
       <br><br>
       <ejs-gantt #gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings"[toolbar]="toolbar" (dataBound)="dataBound($event)"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public toolbar: ToolbarItem[];
    @ViewChild('gantt', {static: true})
    public ganttObj: GanttComponent;
    public ngOnInit(): void {
        this.data = projectNewData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            endDate: 'EndDate',
            duration: 'Duration',
            progress: 'Progress',
            dependency: 'Predecessor',
            child: 'subtasks'
        };
        this.toolbar =  ['ZoomToFit'];
    }
    public dataBound(args: any) {
      this.ganttObj.fitToProject();
    };
    changeData(): void {
      this.ganttObj.dataSource = data;
    };
}

```

{% endtab %}