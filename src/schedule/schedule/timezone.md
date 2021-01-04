---
title: "Scheduler Timezone"
component: "Scheduler"
description: "This article explains how to handle timezone on Scheduler and its events, and also lists out the generic methods available in it."
---

# Timezone

The Scheduler makes use of the current system time zone by default. If it needs to follow some other user-specific time zone, then the `timezone` property needs to be used. Apart from the default action of applying specific timezone to the Scheduler, it is also possible to set different time zone values for each appointments through the properties `startTimezone` and `endTimezone` which can be defined as separate fields within the event fields collection.

## Understanding date manipulation in JavaScript

The `new Date()` in JavaScript returns the exact current date object with complete time and timezone information. For example, it may return value such as `Wed Dec 12 2018 05:23:27 GMT+0530 (India Standard Time)` which indicates that the current date is December 12, 2018 and the current time is 5.23 AM on browsers following the IST timezone.

## Scheduler with no timezone

When no specific time zone is set to Scheduler, appointments will be displayed based on the client system's timezone which is the default behavior. Here, the same appointment when viewed from different timezone will have different start and end times.

The following code example displays an appointment from 9.00 AM to 10.00 AM when you open the Scheduler from any of the timezone. This is because, we are providing the start and end time enclosing with `new Date()` which works based on the client browser's timezone.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, MonthService, AgendaService, TimelineViewsService } from '@syncfusion/ej2-angular-schedule';
import { fifaEventsData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, MonthService, AgendaService, TimelineViewsService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" > <e-views> <e-view option="Day"></e-view> <e-view option="Week"></e-view> <e-view option="TimelineWeek"></e-view> <e-view option="Month"></e-view> <e-view option="Agenda"></e-view> </e-views> </ejs-schedule>`
})
export class AppComponent {
    public eventSettings: EventSettingsModel = {
        dataSource: [{
            Id: 1,
            Subject: 'Paris',
            StartTime: new Date(2018, 1, 15, 9, 0),
            EndTime: new Date(2018, 1, 15, 10, 0)
        }]
    };
    public selectedDate: Date = new Date(2018, 1, 15);
}
```

{% endtab %}

## Scheduler set to specific timezone

When a time zone is set to Scheduler through `timezone` property, the appointments will be displayed exactly based on the Scheduler timezone regardless of its client timezone. In the following code example, appointments will be displayed based on Eastern Time (UTC -05:00).

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { timeZoneData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" timezone="America/New_York" [eventSettings]="eventSettings" > <e-views> <e-view option="Day"></e-view> <e-view option="Week"></e-view> <e-view option="Month"></e-view> </e-views> </ejs-schedule>`
})
export class AppComponent {
    public eventSettings: EventSettingsModel = {
        dataSource: <Object[]>extend([], timeZoneData, null, true)
    };
    public selectedDate: Date = new Date(2018, 1, 17);
}
```

{% endtab %}

## Display events on same time everywhere with no time difference

Setting `timezone` to UTC for Scheduler will display the appointments on same time as in the database for all the users in different time zone.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, MonthService, Timezone } from '@syncfusion/ej2-angular-schedule';
import { fifaEventsData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" timezone="UTC" [eventSettings]="eventSettings" > <e-views> <e-view option="Day"></e-view> <e-view option="Week"></e-view> <e-view option="Month"></e-view> </e-views> </ejs-schedule>`
})
export class AppComponent {
    public fifaEvents: Object[] = <Object[]>extend([], fifaEventsData, null, true);
    public selectedDate: Date = new Date(2018, 5, 17);
    public eventSettings: EventSettingsModel;
    constructor() {
        let timezone: Timezone = new Timezone();
        for (let fifaEvent of this.fifaEvents) {
            let event: { [key: string]: Object } = fifaEvent as { [key: string]: Object };
            event.StartTime = timezone.removeLocalOffset(<Date>event.StartTime);
            event.EndTime = timezone.removeLocalOffset(<Date>event.EndTime);
        }
        this.eventSettings = { dataSource: this.fifaEvents };
    }
}
```

{% endtab %}

## Set specific timezone for events

It is possible to set different timezone for Scheduler events by setting `startTimezone` and `endTimezone` properties within the `eventSettings` option. It allows each appointment to maintain different timezone and displays on Scheduler with appropriate time differences.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { fifaEventsData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" > <e-views> <e-view option="Day"></e-view> <e-view option="Week"></e-view> <e-view option="Month"></e-view> </e-views> </ejs-schedule>`
})
export class AppComponent {
    public eventSettings: EventSettingsModel = {
        dataSource: [{
            Id: 1,
            Subject: 'Paris',
            StartTime: new Date(2018, 1, 15, 10, 0),
            EndTime: new Date(2018, 1, 15, 12, 30),
            StartTimezone: 'Europe/Moscow',
            EndTimezone: 'Europe/Moscow'
        }]
    };
    public selectedDate: Date = new Date(2018, 1, 15);
}
```

{% endtab %}

## Add or remove timezone names to/from the timezone collection

Instead of displaying all the timezone names within the timezone collection (more than 200 are displayed on the editor window timezone fields by default), you can customize the timezone collection at application end as shown in the following example.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, MonthService, timezoneData } from '@syncfusion/ej2-angular-schedule';
import { timeZoneData } from './datasource';
import { extend } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" > <e-views> <e-view option="Day"></e-view> <e-view option="Week"></e-view> <e-view option="Month"></e-view> </e-views> </ejs-schedule>`
})
export class AppComponent {
    public eventSettings: EventSettingsModel = {
        dataSource: <Object[]>extend([], timeZoneData, null, true)
    };
    public selectedDate: Date = new Date(2018, 1, 11);
    private timeZones: { [key: string]: Object }[] = [
        { Value: 'America/New_York', Text: '(UTC-05:00) Eastern Time' },
        { Value: 'UTC', Text: 'UTC' },
        { Value: 'Asia/Kolkata', Text: '(UTC+05:30) India Standard Time' }
    ];
    constructor() {
        timezoneData.splice(0, timezoneData.length, ...this.timeZones);
    }
}
```

{% endtab %}

## Timezone methods

### offset

This method is used to calculate the difference between passed UTC date and timezone.

| Parameters | Type | Description |
|------------|------|-------------|
| Date | Date | UTC time as date object.|
| Timezone | String | Timezone.|

Returns `number`

```typescript
    // Assume your local timezone as IST/UTC+05:30
    let timezone: Timezone = new Timezone();
    let date: Date = new Date(2018,11,5,15,25,11);
    let timeZoneOffset: number = timezone.offset(date,"Europe/Paris");
    console.log(timeZoneOffset); //-60
```

### convert

This method is used to convert the passed date from one timezone to another timezone.

| Parameters | Type | Description |
|------------|------|-------------|
| Date | Date | UTC time as date object.|
| fromOffset | number/string | Timezone from which date need to be converted.|
| toOffset | number/string | Timezone to which date need to be converted.|

Returns `Date`

```typescript
    // Assume your local timezone as IST/UTC+05:30
    let timezone: Timezone = new Timezone();
    let date: Date = new Date(2018,11,5,15,25,11);
    let convertedDate: Date = timezone.convert(date, "Europe/Paris", "Asia/Tokya");
    let convertedDate1: Date = timezone.convert(date, 60, -360);
    console.log(convertedDate); //2018-12-05T08:55:11.000Z
    console.log(convertedDate1); //2018-12-05T16:55:11.000Z
```

### add

This method is used to add the time difference between passed UTC date and timezone.

| Parameters | Type | Description |
|------------|------|-------------|
| Date | Date | UTC time as date object.|
| Timezone | String | Timezone.|

Returns `Date`

```typescript
    // Assume your local timezone as IST/UTC+05:30
    let timezone: Timezone = new Timezone();
    let date: Date = new Date(2018,11,5,15,25,11);
    let convertedDate: Date = timezone.add(date, "Europe/Paris");
    console.log(convertedDate); //2018-12-05T05:25:11.000Z
```

### remove

This method is used to remove the time difference between passed UTC date and timezone.

| Parameters | Type | Description |
|------------|------|-------------|
| Date | Date | UTC as date object.|
| Timezone | String | Timezone.|

Returns `Date`

```typescript
    // Assume your local timezone as IST/UTC+05:30
    let timezone: Timezone = new Timezone();
    let date: Date = new Date(2018,11,5,15,25,11);
    let convertedDate: Date = timezone.remove(date, "Europe/Paris");
    console.log(convertedDate); //2018-12-05T14:25:11.000Z
```

### removeLocalOffset

This method is used to remove the local offset time from the date passed.

| Parameters | Type | Description |
|------------|------|-------------|
| Date | Date | UTC as date object.|

Returns `Date`

```typescript
    // Assume your local timezone as IST/UTC+05:30
    let timezone: Timezone = new Timezone();
    let date: Date = new Date(2018,11,5,15,25,11);
    let convertedDate: Date = timezone.removeLocalOffset(date);
    console.log(convertedDate); //2018-12-05T15:25:11.000Z
```