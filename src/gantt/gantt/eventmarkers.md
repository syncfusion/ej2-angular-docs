---
title: "Event Marker"
component: "Gantt"
description: "Learn how to highlight the important event in Gantt chart part in the Essential JS 2 Gantt component."
---

# Event markers

The event markers in the Gantt component is used to highlight the important events in a project. Event markers can be initialized by using the [`eventMarkers`](../api/gantt/#eventmarkers) property, and you can define date and label for the event markers using the [`day`](../api/gantt/eventMarker/#day) and [`label`](../api/gantt/eventMarker/#label) properties. You can also customize it using the [`cssClass`](../api/gantt/eventMarker/#cssclass) properties. The following code example shows how to add event markers in the Gantt component.

To highlight the days, inject the `DayMarkersService` in the provider section of `AppModule`.

{% tab template= "gantt/eventmarkers/default",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { projectNewData } from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings" [eventMarkers]="eventMarkers"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public eventMarkers : object[];
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
        this.eventMarkers = [
            {
                day: new Date('04/09/2019'),
                label: 'Research phase'
            }, {
                day: new Date('04/30/2019'),
                label: 'Design phase'
            }, {
                day: new Date('05/23/2019'),
                label: 'Production phase'
            }, {
                day: new Date('06/20/2019'),
                label: 'Sales and marketing phase'
            }
        ];
    }
}

```

{% endtab %}