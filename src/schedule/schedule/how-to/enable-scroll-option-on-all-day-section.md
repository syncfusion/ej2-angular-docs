---
title: "All-day scroller"
component: "Scheduler"
description: "This section explains how to enable scroller for all-day row in the scheduler"
---

# Enable scroll option on all-day section

When you have larger number of appointments in all-day row, it is difficult to view all the appointments properly. In that case you can enable scroller option for all-day row by setting true to `enableAllDayScroll` whereas its default value is false. When setting this property to true, individual scroller for all-day row is enabled when it reaches its maximum height on expanding.

> Note: This property is not applicable for Scheduler with height `auto`.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { generateObject } from './datasource.ts';

@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate"
  [eventSettings]="eventSettings" [enableAllDayScroll]="enableAllDayScroll"></ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2021, 3, 28);
    public eventSettings: EventSettingsModel = {
        dataSource: generateObject(),
    };
    public enableAllDayScroll: true;
}
```

{% endtab %}