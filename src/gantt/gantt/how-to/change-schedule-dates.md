---
title: "How To"
component: "Gantt"
description: "Learn how to change schedule start date and end date values dynamically in the JS 2 Gantt component."
---
# Change Schedule Dates

In the Gantt component, you can change the schedule start and end dates by clicking the custom button programmatically using the [`updateProjectDates`](../../api/gantt/#updateprojectdates) method. You can pass the start and end dates as method arguments to the [`updateProjectDates`](../../api/gantt/#updateprojectdates) method. You can also pass the Boolean value as an additional parameter, which is used to round-off the schedule start and end dates displayed in Gantt timeline.

{% tab template="gantt/how-to/changescheduledates",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { GanttComponent } from '@syncfusion/ej2-angular-gantt';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';
import { editingData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<button ejs-button id='changedate' (click)='change()'>Change Date</button>
       <br><br>
       <ejs-gantt #gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    @ViewChild('gantt', {static: true})
    public ganttObj: GanttComponent;
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
    }
    change(): void {
        this.ganttObj.updateProjectDates(new Date('04/10/2019'),new Date('06/20/2019'),true);
        };
}

```

{% endtab %}
