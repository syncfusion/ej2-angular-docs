---
title: "Working days and Hours in Angular Scheduler"
component: "Scheduler"
description: "This section shows the way to set different working days and hours, start and end hours, and start day of the week on Scheduler."
---

# Setting working days and hours

The Scheduler can be customized on various aspects as well as it inherits almost all the calendar-specific features such as options,

* To set custom time range display on Scheduler
* To set different working hours
* To set different working days
* To set different first day of week
* To show/hide weekend days
* To show the week number

## Set working days

By default, Scheduler considers the week days from Monday to Friday as `Working days` and therefore defaults to [1,2,3,4,5] - where 1 represents Monday, 2 represents Tuesday and so on. The days which are not defined in this working days collection are considered as non-working days. Therefore, when the weekend days are set to hide from Scheduler, all those non-working days too gets hidden from the layout.

The Work week and Timeline Work week views displays exactly the defined working days on Scheduler layout, whereas other views displays all the days and simply differentiates the non-working days on UI with inactive cell color.

> The working or business hours depiction on Scheduler are usually valid only on these specified working days.

The following example code depicts how to set the Scheduler to display Monday, Wednesday and Friday as working days of a week.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, WeekService, WorkWeekService, MonthService, TimelineViewsService, View } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [WeekService, WorkWeekService, MonthService, TimelineViewsService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' currentView='WorkWeek' [views]="scheduleViews" [workDays]='workWeekDays' [selectedDate]="selectedDate" [eventSettings]="eventSettings"></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public workWeekDays: number[] = [1, 3, 5];
  public scheduleViews: View[] = ['Week', 'WorkWeek', 'Month', 'TimelineWeek', 'TimelineWorkWeek'];
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Hiding weekend days

The `showWeekend` property is used to either show or hide the weekend days of a week and it is not applicable on Work week view (as non-working days are usually not displayed on work week view). By default, it is set to `true`. The days which are not a part of the working days collection of a Scheduler are usually considered as non-working or weekend days.

Here, the working days are defined as [1, 3, 4, 5] on Scheduler and therefore the remaining days (0, 2, 6 – Sunday, Tuesday and Saturday) are considered as non-working or weekend days and will be hidden from all the views when `showWeekend` property is set to `false`.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, TimelineMonthService, View } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [views]="scheduleViews" [showWeekend]="showWeekend" [workDays]='workWeekDays' [selectedDate]="selectedDate" [eventSettings]="eventSettings"></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public workWeekDays: number[] = [1, 3, 4, 5];
  public showWeekend: boolean = false;
  public scheduleViews: View[] = ['Day', 'Week', 'TimelineMonth'];
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Show week numbers

It is possible to show the week number count of a week in the header bar of the Scheduler by setting true to `showWeekNumber` property. By default, its default value is `false`. In Month view, the week numbers are displayed as a first column.

> The `showWeekNumber` property is not applicable on Timeline views, as it has the equivalent [headerRows](./header-rows/#display-week-numbers-in-timeline-views) property to handle such requirement with additional customizations.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, MonthService, View } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' currentView='Month' [views]="scheduleViews" [showWeekNumber]="showWeekNumber" [selectedDate]="selectedDate" [eventSettings]="eventSettings"></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public workWeekDays: number[] = [1, 3, 4, 5];
  public showWeekNumber: boolean = true;
  public scheduleViews: View[] = ['Day', 'Week', 'Month'];
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Set working hours

Working hours indicates the work hour limit within the Scheduler, which is visually highlighted with an active color on work cells. The working hours can be set on Scheduler using the `workHours` property which is of object type and includes the following sub-options,

* `highlight` – enables/disables the highlighting of work hours.
* `start` - sets the start time of the working/business hour of a day.
* `end` - sets the end time limit of the working/business hour of a day.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, View, WorkHoursModel } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [views]="scheduleViews" [workHours]="scheduleHours" [selectedDate]="selectedDate" [eventSettings]="eventSettings"></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public scheduleHours: WorkHoursModel  = { highlight: true, start: '11:00', end: '20:00' };
  public scheduleViews: View[] = ['Day', 'Week', 'WorkWeek'];
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Scheduler displaying custom hours

It is possible to display the event Scheduler layout with specific time durations by hiding the unwanted hours. To do so, set the start and end hour for the Scheduler using the `startHour` and `endHour` properties respectively.

The following code example displays the Scheduler starting from the time range 7.00 AM to 6.00 PM and the remaining hours are hidden on the UI.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, View, WorkHoursModel } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [views]="scheduleViews" startHour='07:00' endHour='18:00' [selectedDate]="selectedDate" [eventSettings]="eventSettings"></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public scheduleViews: View[] = ['Day', 'Week', 'WorkWeek'];
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Setting start day of the week

By default, Scheduler defaults to `Sunday` as its first day of a week. To change the Scheduler's start day of a week with different day, set the `firstDayOfWeek` property with the values ranging from 0 to 6.

> Here, Sunday is always denoted as 0, Monday as 1 and so on.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, WeekService, TimelineMonthService, View } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [WeekService, TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [views]="scheduleViews" [firstDayOfWeek]="weekFirstDay" [selectedDate]="selectedDate" [eventSettings]="eventSettings"></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public weekFirstDay: number = 3;
  public scheduleViews: View[] = ['Week', 'TimelineMonth'];
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Scroll to specific time and date

You can manually scroll to a specific time on Scheduler by making use of the `scrollTo` method as depicted in the following code example.

{% tab template="schedule/scroll-to", sourceFiles="app/**/*.ts,app/app.component.html", iframeHeight="588px" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ChangeEventArgs } from '@syncfusion/ej2-angular-calendars';
import { ScheduleComponent, EventSettingsModel, DayService, WeekService, WorkWeekService, View } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService],
  // specifies the template string for the Schedule component
  templateUrl: 'app/app.component.html'
})
export class AppComponent {
  @ViewChild('scheduleObj')
  public scheduleObj: ScheduleComponent;
  public selectedDate: Date = new Date(2018, 1, 15);
  public scrollToHour: Date = new Date(2018, 1, 15, 9);
  public scheduleViews: View[] = ['Day', 'Week', 'WorkWeek'];
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
  onChange(args: ChangeEventArgs): void {
    this.scheduleObj.scrollTo(args.text);
  }
 }
```

{% endtab %}

### How to scroll to current time on initial load

There are scenarios where you may need to load the Scheduler displaying the system's current time on the currently visible view port area. In such cases, the Scheduler needs to be scrolled to a specific time based on the system's current time which is depicted in the following code example.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ScheduleComponent, EventSettingsModel, DayService, WeekService, TimelineViewsService, View } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, TimelineViewsService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule #scheduleObj width='100%' height='550px' [views]="scheduleViews" (created)="onCreated($event)" [selectedDate]="selectedDate" [eventSettings]="eventSettings"></ejs-schedule>`
})
export class AppComponent {
  @ViewChild('scheduleObj')
  public scheduleObj: ScheduleComponent;
  public selectedDate: Date = new Date(2018, 1, 15);
  public scheduleViews: View[] = ['Day', 'Week', 'TimelineWorkWeek'];
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
  onCreated(): void {
    let currTime: Date = new Date();
    let hours: string = currTime.getHours() < 10 ? '0' +currTime.getHours().toString() : currTime.getHours().toString();
    let minutes: string = currTime.getMinutes().toString();
    let time: string = hours + ':' + minutes;
    this.scheduleObj.scrollTo(time);
  }
 }
```

{% endtab %}

## See Also

* [To display the current time indicator](./timescale/#highlighting-current-date-and-time)
* [To set different working hours dynamically](./how-to/set-different-work-hours)
* [To set different working hours for each resources](./resources/#set-different-work-hours)
* [To set different working days for each resources](./resources/#set-different-work-days)