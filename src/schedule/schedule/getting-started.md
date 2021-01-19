---
title: "Angular Scheduler - Getting Started"
component: "Scheduler"
description: "This article demonstrates how to create a simple Scheduler and configure its available features."
---

# Getting Started

This section briefly explains how to create **Scheduler** component and configure its available functionalities in Angular Environment.

To get start quickly with Angular Scheduler using CLI and Schematics, you can check on this video:

`youtube:dE_9t5HJ8rc`

## Setup Angular Environment

You can use [`Angular CLI`](https://github.com/angular/angular-cli) to setup your Angular applications.
To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion Schedule package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Schedule component, use the following command.

```javascript
npm install @syncfusion/ej2-angular-schedule --save
```

> The **--save** will instruct NPM to include the schedule package inside of the `dependencies` section of the `package.json`.

## Registering Schedule Module

Import Schedule module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-schedule` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the ScheduleModule for the Schedule component
import { ScheduleModule } from '@syncfusion/ej2-angular-schedule';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-schedule module into NgModule
  imports:      [ BrowserModule, ScheduleModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS reference

Schedule CSS files are available in the ej2-angular-schedule package folder. This can be referenced in your application using the following code.

`[src/styles/styles.css]`.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-calendars/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-angular-schedule/styles/material.css';
```

## Module injection

Each view types available in scheduler are maintained as individual modules and to work with those views, it is necessary to inject the required modules. The following modules are available in scheduler namely,

* **Day** - Inject this module for displaying day view.
* **Week** - Inject this module for displaying week view.
* **WorkWeek** - Inject this module for displaying work week view.
* **Month** - Inject this module for displaying month view.
* **Year** - Inject this module for displaying year view.
* **Agenda** - Inject this module for  displaying agenda view.
* **MonthAgenda** - Inject this module for displaying month agenda view.
* **TimelineViews** - Inject this module for displaying  timeline day, timeline week, timeline work week view.
* **TimelineMonth** - Inject this module for displaying timeline month view.
* **TimelineYear** - Inject this module for displaying timeline year view.

These modules should be injected into the schedule using the `providers` method within the `app.component.ts` file as shown below. On doing so, only the injected views will be loaded and displayed on the schedule.

`[src/app/app.component.ts]`

```typescript
@Component({
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService, MonthAgendaService, TimelineViewsService, TimelineMonthService]
})
```

## Initialize the Schedule

Modify the template in [src/app/app.component.ts] file to render the `ej2-angular-schedule` component.

`[src/app/app.component.ts]`

```typescript
import { Component } from '@angular/core';
import { DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule> </ejs-schedule>`
})
export class AppComponent { }
```

Now, run the application in the browser using the following command.

```sh
npm start
```

The output will display the empty scheduler.

## Populating appointments

To populate the empty Scheduler with appointments, define either the local JSON data or remote data through the `dataSource` property available within the `eventSettings` option. To define any appointments, start and end time fields are mandatory. In the following example, you can see the appointment defined with default fields such as Id, Subject, StartTime and EndTime.

`[src/app/app.component.ts]`

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the Schedule component
  template: `<ejs-schedule [eventSettings]='eventSettings'></ejs-schedule>`
})
export class AppComponent {
  public data: object[] = [{
    Id: 1,
    Subject: 'Meeting',
    StartTime: new Date(2018, 1, 15, 10, 0),
    EndTime: new Date(2018, 1, 15, 12, 30)
  }];
  public eventSettings: EventSettingsModel = {
    dataSource: this.data
  }
}
```

You can also provide different names to these default fields, for which the custom names of those fields must be mapped appropriately within `fields` property as shown below.

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate'
  [eventSettings]='eventSettings'></ejs-schedule>`
})
export class AppComponent {
  public data: object [] = [{
    id: 2,
    eventName: 'Meeting',
    startTime: new Date(2018, 1, 15, 10, 0),
    endTime: new Date(2018, 1, 15, 12, 30),
    isAllDay: false
  }];
  public selectedDate: Date = new Date(2018, 1, 15);
  public eventSettings: EventSettingsModel = {
    dataSource: this.data,
    fields: {
      id: 'id',
      subject: { name: 'eventName' },
      isAllDay: { name: 'isAllDay' },
      startTime: { name: 'startTime' },
      endTime: { name: 'endTime' },
    }
  };
}
```

The other fields available in Scheduler can be referred from [here](./appointments#appointment-fields).

## Setting date

Scheduler usually displays the system date as its current date. To change the current date of Scheduler with specific date, define the `selectedDate` property.

`[src/app/app.component.ts]`

```typescript
import { Component } from '@angular/core';
import { DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate'></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
}
```

## Setting view

Scheduler displays `week` view by default. To change the current view, define the applicable view name to the `currentView` property. The applicable view names are,

* Day
* Week
* WorkWeek
* Month
* Year
* Agenda
* MonthAgenda
* TimelineDay
* TimelineWeek
* TimelineWorkWeek
* TimelineMonth
* TimelineYear

```typescript
import { Component } from '@angular/core';
import { DayService, WeekService, WorkWeekService, MonthService, AgendaService, View } from '@syncfusion/ej2-angular-schedule';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [currentView]='currentView' [eventSettings]='eventSettings'></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public currentView: View = 'Month';
}

```

## Individual view customization

Each individual Scheduler views can be customized with its own options such as setting different start and end hour on Week and Work Week views, whereas hiding the weekend days on Month view alone.
This can be achieved by defining views property to accept the array of object type, where each object depicts the individual view customization.

The output will display the Scheduler with the specified view configuration.

{% tab template="schedule/views", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { WeekService, MonthService, WorkWeekService, EventSettingsModel } from '@syncfusion/ej2-angular-schedule';
import { defaultData } from './datasource.ts';

@Component({
  selector: 'app-root',
  providers: [WeekService, MonthService, WorkWeekService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings"><e-views> <e-view option="Week" startHour="07:00" endHour="15:00"></e-view>
  <e-view option="WorkWeek" startHour="10:00" endHour="18:00"></e-view> <e-view option="Month" [showWeekend]="showWeekend"></e-view></e-views></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public showWeekend: boolean = false;
  public eventSettings: EventSettingsModel = { dataSource: defaultData };
}
```

{% endtab %}