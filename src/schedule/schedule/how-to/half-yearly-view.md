---
title: "Scheduler Year view customization"
component: "Scheduler"
description: "This section explains how to customize the Year view using different properties in scheduler"
---

# Half-yearly view

The year view of our scheduler displays all the 365 days and their related appointments of a particular year. You can customize the year view by using the following properties.

* [`firstMonthOfYear`](../../api/schedule#firstmonthofyear)
* [`monthsCount`](../../api/schedule#monthscount)
* [`monthHeaderTemplate`](../../api/schedule#monthheadertemplate)

In the following code example, you can see how to render only the last six months of a year in the scheduler. To start with the month of  June, `firstMonthYear` is set to 6 and `monthsCount` is set to 6 to render only 6 months.

{% tab template="schedule/year-customizations", sourceFiles="app/**/*.ts,app/app.component.html,app/index.css", iframeHeight="588px" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import {
  ScheduleComponent, EventSettingsModel, EventRenderedArgs, YearService, TimelineYearService, GroupModel, ResizeService, DragAndDropService
} from '@syncfusion/ej2-angular-schedule';
import { resourceData } from './datasource.ts';

@Component({
    selector: 'app-root',
    templateUrl: 'app/app.component.html',
    providers: [YearService, TimelineYearService, ResizeService, DragAndDropService],
    styleUrls: ['app/index.css'],
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public selectedDate: Date = new Date(2021, 7, 4);
    public firstMonthOfYear: number = 6;
    public monthsCount: number = 6;
    public eventSettings: EventSettingsModel = {
        dataSource: resourceData
    };
    public group: GroupModel = {
        resources: ['Owners']
    };
    public ownerDataSource: Object[] = [
        { OwnerText: 'Nancy', Id: 1, OwnerColor: '#ffaa00' },
        { OwnerText: 'Steven', Id: 2, OwnerColor: '#f8a398' },
        { OwnerText: 'Robert', Id: 3, OwnerColor: '#7499e1' },
        { OwnerText: 'Smith', Id: 4, OwnerColor: '#f8a398' },
        { OwnerText: 'Michael', Id: 5, OwnerColor: '#f8a398' }
    ];
    public getMonthHeaderText(date: Date): string {
        return date.toLocaleString('en-us', { month: 'long' }) + ' ' + date.getFullYear();
  }
}

```

{% endtab %}
