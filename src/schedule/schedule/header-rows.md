---
title: "Timeline header rows in Angular Scheduler"
component: "Scheduler"
description: "This section explains how to display the additional header rows on timeline view of Scheduler."
---

# Timeline header rows

The Timeline views can have additional header rows other than its default date and time header rows. It is possible to show individual header rows for displaying year, month and week separately using the `headerRows` property. This property is applicable only on the timeline views. The possible rows which can be added using `headerRows` property are as follows.

* `Year`
* `Month`
* `Week`
* `Date`
* `Hour`

> The `Hour` row is not applicable for Timeline month view.

Learn to add and customize additional header rows in the Timeline views of Angular Scheduler from this video:

`youtube:x4QmJxt0adg`

The following example shows the Scheduler displaying all the available header rows on timeline views.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineViewsService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineViewsService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" startHour='09:00' endHour='18:00'>
        <e-header-rows>
            <e-header-row option='Year'></e-header-row>
            <e-header-row option='Month'></e-header-row>
            <e-header-row option='Week'></e-header-row>
            <e-header-row option='Date'></e-header-row>
            <e-header-row option='Hour'></e-header-row>
        </e-header-rows>
        <e-views>
            <e-view option='TimelineWeek'></e-view>
        </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 11, 31);
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

## Display year and month rows in timeline views

To display the timeline Scheduler simply with year and month names alone, define the option `Year` and `Month` within the `headerRows` property.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineMonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings">
        <e-header-rows>
            <e-header-row option='Year'></e-header-row>
            <e-header-row option='Month'></e-header-row>
        </e-header-rows>
        <e-views>
            <e-view option='TimelineMonth' [interval]="viewInterval"></e-view>
        </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 11, 31);
    public viewInterval: Boolean = 24;
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

## Display week numbers in timeline views

The week number can be displayed in a separate header row of the timeline Scheduler by setting `Week` option within `headerRows` property.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineViewsService, TimelineMonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineViewsService, TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings">
        <e-header-rows>
            <e-header-row option='Week'></e-header-row>
            <e-header-row option='Date'></e-header-row>
            <e-header-row option='Hour'></e-header-row>
        </e-header-rows>
        <e-views>
            <e-view option='TimelineMonth' [interval]="monthInterval"></e-view>
            <e-view option='TimelineWeek' [interval]="weekInterval"></e-view>
            <e-view option='TimelineDay' [interval]="dayInterval"></e-view>
        </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public monthInterval: Boolean = 24;
    public weekInterval: Boolean = 3;
    public dayInterval: Boolean = 4;
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

## Timeline view displaying dates of a complete year

It is possible to display a complete year in a timeline view by setting `interval` value as 12 and defining **TimelineMonth** view option within the `views` property of Scheduler.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineMonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings">
        <e-header-rows>
            <e-header-row option='Month'></e-header-row>
            <e-header-row option='Date'></e-header-row>
        </e-header-rows>
        <e-views>
            <e-view option='TimelineMonth' [interval]="viewInterval"></e-view>
        </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 0, 1);
    public viewInterval: Boolean = 12;
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

## Customizing the header rows using template

You can customize the text of the header rows and display any images or formatted text on each individual header rows using the built-in `template` option available within the `headerRows` property.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { Internationalization } from '@syncfusion/ej2-base';
import { EventSettingsModel, TimelineMonthService, getWeekNumber, getWeekLastDate, CellTemplateArgs } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings">
        <e-header-rows>
            <e-header-row option='Year'>
                <ng-template #template let-data>
                    <span [innerHTML]="getYearDetails(data)"></span>
                </ng-template>
            </e-header-row>
            <e-header-row option='Month'>
                <ng-template #template let-data>
                    <span [innerHTML]="getMonthDetails(data)"></span>
                </ng-template>
            </e-header-row>
            <e-header-row option='Week'>
                <ng-template #template let-data>
                    <span [innerHTML]="getWeekDetails(data)"></span>
                </ng-template>
            </e-header-row>
            <e-header-row option='Date'></e-header-row>
        </e-header-rows>
        <e-views>
            <e-view option='TimelineMonth'></e-view>
        </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 0, 1);
    public instance: Internationalization = new Internationalization();
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
    public getYearDetails(value: CellTemplateArgs): string {
        return 'Year: ' + this.instance.formatDate((value as CellTemplateArgs).date, { skeleton: 'y' });
    }
    public getMonthDetails(value: CellTemplateArgs): string {
        return 'Month: ' + this.instance.formatDate((value as CellTemplateArgs).date, { skeleton: 'yMMM' });
    }
    public getWeekDetails(value: CellTemplateArgs): string {
        return 'Week: ' + getWeekNumber(getWeekLastDate((value as CellTemplateArgs).date, 0));
    }
}
```

{% endtab %}

> You can refer to our [Angular Scheduler](https://www.syncfusion.com/angular-ui-components/angular-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [Angular Scheduler example](https://ej2.syncfusion.com/angular/demos/#/material/schedule/overview) to knows how to present and manipulate data.