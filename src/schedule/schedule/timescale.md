---
title: "Timescale Customization | Angular Scheduler"
component: "Scheduler"
description: "This section demonstrates how to set different time slot duration on Scheduler and also to customize the major and minor time slots using templates."
---

# TimeScale Customization

The time slots are usually the time cells that are displayed on the Day, Week and Work Week views of both the vertical views (to the left most position) and timeline views (at the top position). The `timeScale` property allows you to control and set the required time slot duration for the work cells displayed on Scheduler. It includes the following sub-options such as,

* `enable` - When set to `true`, allows the Scheduler to display the appointments accurately against the exact time duration. If set to `false`, all the appointments of a day will be displayed one below the other with no grid lines displayed. Its default value is `true`.
* `interval` – Defines the time duration on which the time axis to be displayed either in 1 hour or 30 minutes interval and so on. It accepts the values in minutes and defaults to 60.
* `slotCount` – Decides the number of slot count to be split for the specified time interval duration. It defaults to 2, thus displaying two slots to represent an hour(each slot depicting 30 minutes duration).

## Setting different time slot duration

The `interval` and `slotCount` properties can be used together on the Scheduler to set different time slot duration which is depicted in the following code example. Here, six time slots together represents an hour.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimeScaleModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings"  [timeScale]="timeScale" > </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public timeScale: TimeScaleModel = { enable: true, interval: 60, slotCount: 6 };
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Customizing time cells using template

The `timeScale` property also provides template option to allow customization of time slots which are as follows,

* `majorSlotTemplate` - The template option to be applied for major time slots. Here, the template accepts either the string or HTMLElement as template design and then the parsed design is displayed onto the time cells. The time details can be accessed within this template.
* `minorSlotTemplate` - The template option to be applied for minor time slots. Here, the template accepts either the string or HTMLElement as template design and then the parsed design is displayed onto the time cells. The time details can be accessed within this template.

{% tab template="schedule/timescale", sourceFiles="app/app.component.html,app/app.component.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimeScaleModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';
import { Internationalization } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public timeScale: TimeScaleModel = {
        enable: true,
        interval: 60,
        slotCount: 6,
        majorSlotTemplate: '#majorSlotTemplate',
        minorSlotTemplate: '#minorSlotTemplate'
    };
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
    public instance: Internationalization = new Internationalization();
    getMajorTime(date: Date): string {
        return this.instance.formatDate(date, { skeleton: 'hm' });
    }
    getMinorTime(date: Date): string {
        return this.instance.formatDate(date, { skeleton: 'ms' }).replace(':00', '');
    }
}
```

{% endtab %}

## Hide the timescale

The grid lines which indicates the exact time duration can be enabled or disabled on the Scheduler, by setting `true` or `false` to the `enable` option within the `timeScale` property. It's default value is `true`.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimeScaleModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings"  [timeScale]="timeScale" > </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public timeScale: TimeScaleModel = { enable: false };
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Highlighting current date and time

By default, Scheduler indicates current date with a highlighted date header on all views, as well as marks accurately the system's current time on specific views such as Day, Week, Work Week, Timeline Day, Timeline Week and Timeline Work Week views. To stop highlighting the current time indicator on Scheduler views, set `false` to the `showTimeIndicator` property which defaults to `true`.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimeScaleModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [eventSettings]="eventSettings"  [showTimeIndicator]="showTimeIndicator" > </ejs-schedule>`
})
export class AppComponent {
    public showTimeIndicator: boolean = true;
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}