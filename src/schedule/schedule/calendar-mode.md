---
title: "Calendar Mode in JavaScript Scheduler"
component: "Scheduler"
description: "This section explains how to change the default calendar mode on Scheduler to display it either on Gregorian or Islamic mode."
---

# Calendar mode

The Scheduler supports the following two types of calendar mode.

* Gregorian Calendar
* Islamic Calendar

## Gregorian Calendar

The Scheduler by default displays the gregorian calendar dates which is the most widely used calendar in the world. The Gregorian calendar is a solar calendar which has 12 months with 28 to 31 days each. A year which is divisible by four is said to be a leap year in this calendar mode. A leap year usually has 366 days whereas the regular year has 365 days.

## Islamic Calendar

The Islamic Calendar, also known as the Hijri or Muslim calendar, is a lunar calendar which has 12 months in a year with 354 or 355 days. Each month of this calendar denotes the birth of the new lunar cycle and therefore, each month can have 29 or 30 days depending on the visibility of the moon. Here, the odd-numbered months have 30 days and the even months have 29 days.

> The current Islamic year is 1440 AH. Usually the Gregorian calendar runs from approximately 11 September 2018 to 30 August 2019 for this 1440 AH year.

The Scheduler has a property `calendarMode` which is used to switch between the gregorian and islamic calendar modes. By default, it is set to `Gregorian` and to use it with Islamic calendar dates, define the `calendarMode` of Scheduler to `Islamic`. The following example depicts, how to display the Islamic calendar dates on Scheduler.

To make use of Islamic calendar in Scheduler, import the `Calendar` and `Islamic` module from `ej2-calendars` package and also inject it using the `Calendar.Inject` method. Apart from this, it requires the following CLDR data to be loaded using loadCldr function.

* numberingSystems.json
* ca-gregorian.json
* numbers.json
* timeZoneNames.json
* ca-islamic.json

> To know more information on, how to install the CLDR data, refer the [`Internationalization`](https://ej2.syncfusion.com/angular/documentation/common/internationalization/#installing-cldr-data) topic.

{% tab template="schedule/islamic-calendar", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { loadCldr, L10n } from '@syncfusion/ej2-base';
import { Calendar, Islamic } from '@syncfusion/ej2-angular-calendars';
import {
  ScheduleComponent, DayService, WeekService, MonthService, MonthAgendaService,
  AgendaService, TimelineViewsService, TimelineMonthService, EventSettingsModel
} from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';
import * as localeObj from "./locale.json";
import * as numberingSystems from "./numberingSystems.json";
import * as ca_gregorian from "./ca-gregorian.json";
import * as numbers from "./numbers.json";
import * as timeZoneNames from "./timeZoneNames.json";
import * as ca_islamic from "./ca-islamic.json";

Calendar.Inject(Islamic);

L10n.load(localeObj);
loadCldr(numberingSystems, ca_gregorian, numbers, timeZoneNames, ca_islamic);

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, MonthService, AgendaService, MonthAgendaService, TimelineViewsService, TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' calendarMode='Islamic' locale='ar' [enableRtl]="enableRtl" showQuickInfo="false" [selectedDate]="selectedDate" [eventSettings]="eventSettings">
    <e-views>
    <e-view option='Day'></e-view>
      <e-view option='TimelineDay'></e-view>
      <e-view option='Week'></e-view>
      <e-view option='TimelineWeek'></e-view>
      <e-view option='Month'></e-view>
      <e-view option='TimelineMonth'></e-view>
      <e-view option='Agenda'></e-view>
      <e-view option='MonthAgenda'></e-view>
    </e-views>
  </ejs-schedule>`
})
export class AppComponent {
    public enableRtl: Boolean = true;
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

> You can refer to our [Angular Scheduler](https://www.syncfusion.com/angular-ui-components/angular-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [Angular Scheduler example](https://ej2.syncfusion.com/angular/demos/#/material/schedule/overview) to knows how to present and manipulate data.