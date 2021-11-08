---
title: "BaseLine"
component: "Gantt"
description: "Learn how to render the baseline in the Essential JS 2 Gantt component."
---

# Baseline

The baseline feature enables users to view the deviation between the planned dates and actual dates of the tasks in a project. Baseline dates or planned dates of a task may or may not be same as the actual task dates. The baseline can be enabled by setting the [`renderBaseline`](../api/gantt/#renderbaseline) property to `true` and the baseline color can be changed using the [`baselineColor`](../api/gantt/#baselinecolor) property. To render the baseline, you should map the baseline start and end date values from the data source. This can be done using the [`baselineStartDate`](../api/gantt/taskFields/#baselinestartdate) and [`baselineEndDate`](../api/gantt/taskFields/#baselineenddate) properties. The following code example shows how to enable a baseline in the Gantt component.

{% tab template= "gantt/baseline/default",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { baselineData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings" [columns]="columns" [timelineSettings]="timelineSettings" [renderBaseline]="true" [treeColumnIndex]="1" height="450px" [allowSelection]="true" durationUnit="Minute" dateFormat="hh:mm a" [projectStartDate]="projectStartDate" [projectEndDate]="projectEndDate" [dayWorkingTime]="dayWorkingTime" [includeWeekend]="true" baselineColor='red'></ejs-gantt>`,
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
            progress: 'Progress',
            baselineStartDate: 'BaselineStartDate',
            baselineEndDate: 'BaselineEndDate',
            child: 'subtasks'
        };
        this.columns =  [
            { field: 'TaskName', headerText: 'Service Name', width: '250' },
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
    }
}

```

{% endtab %}