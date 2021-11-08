---
title: "How To"
component: "Gantt"
description: "Learn how to change the non-working day in the JS 2 Gantt component."
---

# Weekend / Non-working days

Non-working days/weekend are used to represent the non-productive days in a project. You can define the non-working days in a week using the `workWeek` property in Gantt.

{% tab template="gantt/how-to/changenonworkingday",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings"  [workWeek]="workWeek"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
     public workWeek: object;

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
        this.workWeek = ["Sunday","Monday","Tuesday","Wednesday","Thursday"];
    }
}

```

{% endtab %}

> By default, Saturdays and Sundays are considered as non-working days/weekend in a project.
> In the Gantt component, you can make weekend as working day by setting the `includeWeekend` property to true.