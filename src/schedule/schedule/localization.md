---
title: "Globalization in Angular Scheduler"
component: "Scheduler"
description: "This section explains how the Scheduler adapts to various languages and culture by parsing and formatting the date or number appropriately."
---

# Globalization and Localization

The Scheduler integrates different date-time formats and cultures, which allows it to function globally, thus meeting the diverse needs of different regions.

You can adapt the Scheduler to various languages by parsing and formatting the date or number ([`Internationalization`](http://ej2.syncfusion.com/documentation/base/intl.html)), adding culture specific customization and translation to the text ([`Localization`](http://ej2.syncfusion.com/documentation/base/localization.html)).

## Globalization

The Internationalization library provides support for formatting and parsing the number, date, and time by using the official [`Unicode CLDR`](http://cldr.unicode.org/) JSON data and also provides the `loadCldr` method to load the culture specific CLDR JSON data.

By default, Scheduler is set to follow the English culture ('en-US'). If you want to go with different culture other than English, follow the below steps.

* Install the `CLDR-Data` package by using the below command (it installs the CLDR JSON data). For more information about CLDR-Data, refer to this [link](http://cldr.unicode.org/index/cldr-spec/json).

```cmd
npm install cldr-data --save
```

Once the package is installed, you can find the culture specific JSON data under the location `\node_modules\cldr-data`.

* Now import the installed CLDR JSON data into the `app.component.ts` file. To import JSON data, you need to install the JSON plugin loader. Here, we have used the SystemJS JSON plugin loader.

```sh
npm install systemjs-plugin-json --save-dev
```

* Once installed, configure the `system.config.js` configuration settings as shown in the following code to map the `systemjs-plugin-json` loader.

```typescript
/**
 * System configuration for Angular samples
 * Adjust as necessary for your application needs.
 */
(function (global) {
  System.config({
    paths: {
      // paths serve as alias
      'npm:': 'node_modules/',
      "syncfusion:": "node_modules/@syncfusion/", // syncfusion alias
    },
    // map tells the System loader where to look for things
    map: {
      // our app is within the app folder
      'app': 'app',

      // angular bundles
      '@angular/core': 'npm:@angular/core/bundles/core.umd.js',
      '@angular/common': 'npm:@angular/common/bundles/common.umd.js',
      '@angular/compiler': 'npm:@angular/compiler/bundles/compiler.umd.js',
      '@angular/platform-browser': 'npm:@angular/platform-browser/bundles/platform-browser.umd.js',
      '@angular/platform-browser-dynamic': 'npm:@angular/platform-browser-dynamic/bundles/platform-browser-dynamic.umd.js',
      '@angular/http': 'npm:@angular/http/bundles/http.umd.js',
      '@angular/router': 'npm:@angular/router/bundles/router.umd.js',
      '@angular/forms': 'npm:@angular/forms/bundles/forms.umd.js',

      // syncfusion bundles
      "@syncfusion/ej2-inputs": "syncfusion:ej2-inputs/dist/ej2-inputs.umd.min.js",
        "@syncfusion/ej2-calendars": "syncfusion:ej2-calendars/dist/ej2-calendars.umd.min.js",
        "@syncfusion/ej2-lists": "syncfusion:ej2-lists/dist/ej2-lists.umd.min.js",
        "@syncfusion/ej2-base": "syncfusion:ej2-base/dist/ej2-base.umd.min.js",
        "@syncfusion/ej2-schedule": "syncfusion:ej2-schedule/dist/ej2-schedule.umd.min.js",
        "@syncfusion/ej2-data": "syncfusion:ej2-data/dist/ej2-data.umd.min.js",
        "@syncfusion/ej2-buttons": "syncfusion:ej2-buttons/dist/ej2-buttons.umd.min.js",
        "@syncfusion/ej2-popups": "syncfusion:ej2-popups/dist/ej2-popups.umd.min.js",
        "@syncfusion/ej2-navigations": "syncfusion:ej2-navigations/dist/ej2-navigations.umd.min.js",
        "@syncfusion/ej2-dropdowns": "syncfusion:ej2-dropdowns/dist/ej2-dropdowns.umd.min.js",
        "@syncfusion/ej2-splitbuttons": "syncfusion:ej2-splitbuttons/dist/ej2-splitbuttons.umd.min.js",
        "@syncfusion/ej2-angular-base": "syncfusion:ej2-angular-base/dist/ej2-angular-base.umd.min.js",
        "@syncfusion/ej2-angular-schedule": "syncfusion:ej2-angular-schedule/dist/ej2-angular-schedule.umd.min.js",
        "cldr-data": 'npm:cldr-data',
        "plugin-json": "npm:systemjs-plugin-json/json.js",

      // other libraries
      'rxjs':                      'npm:rxjs',
      'angular-in-memory-web-api': 'npm:angular-in-memory-web-api/bundles/in-memory-web-api.umd.js'
    },
    meta: {
      '*.json': { loader: 'plugin-json' }
    },
    // packages tells the System loader how to load when no filename and/or no extension
    packages: {
      app: {
        defaultExtension: 'js',
        meta: {
          './*.js': {
            loader: 'systemjs-angular-loader.js'
          }
        }
      },
      "cldr-data": { main: 'index.js', defaultExtension: 'js' },
      rxjs: {
        defaultExtension: 'js'
      }
    }
  });
})(this);
```

* Now import the required cultures from the installed location to `app.component.ts` file as given in the following code example.

```typescript
//import the loadCldr from ej2-base
import { loadCldr} from '@syncfusion/ej2-base';
import * as numberingSystems from 'cldr-data/supplemental/numberingSystems.json';
import * as gregorian from 'cldr-data/main/fr-CH/ca-gregorian.json';
import * as numbers from 'cldr-data/main/fr-CH/numbers.json';
import * as timeZoneNames from 'cldr-data/main/fr-CH/timeZoneNames.json';

// Angular CLI 8.0 and above versions
loadCldr(numberingSystems['default'], gregorian['default'], numbers['default'], timeZoneNames['default']);

// Angular CLI 8.0 below versions
loadCldr(numberingSystems, gregorian, numbers, timeZoneNames);
```

* Set the culture to Scheduler by using the `locale` property.

{% tab template="schedule/localization", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
import { loadCldr } from '@syncfusion/ej2-base';
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import * as timeZoneNames from './timeZoneNames.json';

loadCldr(numberingSystems, gregorian, numbers, timeZoneNames);

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' locale='fr-CH' [selectedDate]="selectedDate" [eventSettings]="eventSettings" [views]='views'></ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Localizing the static Scheduler text

[`Localization`](http://ej2.syncfusion.com/documentation/base/localization.html) library allows to display all the static text, date content, and time mode of the Scheduler following the localized language. To achieve this, set the `locale` property of Scheduler, as well as define the translation text of static words of Scheduler through the `load` method.

For example, the following code example lets you to define the French translation words for all the static words used in Scheduler.

{% tab template="schedule/localization", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
import { L10n, loadCldr } from '@syncfusion/ej2-base';
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import * as timeZoneNames from './timeZoneNames.json';

loadCldr(numberingSystems, gregorian, numbers, timeZoneNames);
L10n.load({
    'fr-CH': {
        'schedule': {
            'day': 'journée',
            'week': 'La semaine',
            'workWeek': 'Semaine de travail',
            'month': 'Mois',
            'today': 'Aujourd`hui'
        },
        'calendar': {
            'today': 'Aujourd`hui'
        }
    }
});

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' locale='fr-CH' [selectedDate]='selectedDate'[eventSettings]='eventSettings' [views]='views'></ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

The localized words for static text used in Scheduler and Recurrence Editor can be referred from the following code.

```typescript
L10n.load({
    "en": {
        "schedule": {
            "day": "Day",
            "week": "Week",
            "workWeek": "Work Week",
            "month": "Month",
            "agenda": "Agenda",
            "weekAgenda": "Week Agenda",
            "workWeekAgenda": "Work Week Agenda",
            "monthAgenda": "Month Agenda",
            "today": "Today",
            "noEvents": "No events",
            "emptyContainer": "There are no events scheduled on this day.",
            "allDay": "All day",
            "start": "Start",
            "end": "End",
            "more": "more",
            "close": "Close",
            "cancel": "Cancel",
            "noTitle": "(No Title)",
            "delete": "Delete",
            "deleteEvent": "Delete Event",
            "deleteMultipleEvent": "Delete Multiple Events",
            "selectedItems": "Items selected",
            "deleteSeries": "Delete Series",
            "edit": "Edit",
            "editSeries": "Edit Series",
            "editEvent": "Edit Event",
            "createEvent": "Create",
            "subject": "Subject",
            "addTitle": "Add title",
            "moreDetails": "More Details",
            "save": "Save",
            "editContent": "Do you want to edit only this event or entire series?",
            "deleteRecurrenceContent": "Do you want to delete only this event or entire series?",
            "deleteContent": "Are you sure you want to delete this event?",
            "deleteMultipleContent": "Are you sure you want to delete the selected events?",
            "newEvent": "New Event",
            "title": "Title",
            "location": "Location",
            "description": "Description",
            "timezone": "Timezone",
            "startTimezone": "Start Timezone",
            "endTimezone": "End Timezone",
            "repeat": "Repeat",
            "saveButton": "Save",
            "cancelButton": "Cancel",
            "deleteButton": "Delete",
            "recurrence": "Recurrence",
            "wrongPattern": "The recurrence pattern is not valid.",
            "seriesChangeAlert": "The changes made to specific instances of this series will be cancelled and those events will match the series again.",
            "createError": "The duration of the event must be shorter than how frequently it occurs. Shorten the duration, or change the recurrence pattern in the recurrence event editor.",
            "recurrenceDateValidation": "Some months have fewer than the selected date. For these months, the occurrence will fall on the last date of the month.",
            "sameDayAlert": "Two occurrences of the same event cannot occur on the same day.",
            "editRecurrence": "Edit Recurrence",
            "repeats": "Repeats",
            "alert": "Alert",
            "startEndError": "The selected end date occurs before the start date.",
            "invalidDateError": "The entered date value is invalid.",
            "ok": "Ok",
            "occurrence": "Occurrence",
            "series": "Series",
            "previous": "Previous",
            "next": "Next",
            "timelineDay": "Timeline Day",
            "timelineWeek": "Timeline Week",
            "timelineWorkWeek": "Timeline Work Week",
            "timelineMonth": "Timeline Month"
        },
        "recurrenceeditor": {
            "none": "None",
            "daily": "Daily",
            "weekly": "Weekly",
            "monthly": "Monthly",
            "month": "Month",
            "yearly": "Yearly",
            "never": "Never",
            "until": "Until",
            "count": "Count",
            "first": "First",
            "second": "Second",
            "third": "Third",
            "fourth": "Fourth",
            "last": "Last",
            "repeat": "Repeat",
            "repeatEvery": "Repeat Every",
            "on": "Repeat On",
            "end": "End",
            "onDay": "Day",
            "days": "Day(s)",
            "weeks": "Week(s)",
            "months": "Month(s)",
            "years": "Year(s)",
            "every": "every",
            "summaryTimes": "time(s)",
            "summaryOn": "on",
            "summaryUntil": "until",
            "summaryRepeat": "Repeats",
            "summaryDay": "day(s)",
            "summaryWeek": "week(s)",
            "summaryMonth": "month(s)",
            "summaryYear": "year(s)"
        }
    }
});
```

## Setting date format

Scheduler can be used with all valid date formats and by default it follows the universal date format "MM/dd/yyyy". If the `dateFormat` property is not specified particularly, then it will work based on the locale that is assigned to the Scheduler. As the default locale applied on Scheduler is "en-US", this makes it to follow the "MM/dd/yyyy" pattern.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [dateFormat]="dateFormat" [selectedDate]="selectedDate" [eventSettings]="eventSettings"></ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public dateFormat: string = "yyyy/MM/dd";
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Time mode

The time mode of the Scheduler can be either 12 or 24 hours format which is completely based on the `locale` set to the Scheduler. Since the default `locale` value of the Scheduler is en-US, the time mode will be set to 12 hours format automatically.

{% tab template="schedule/localization", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
import { L10n, loadCldr } from '@syncfusion/ej2-base';
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import * as timeZoneNames from './timeZoneNames.json';

loadCldr(numberingSystems, gregorian, numbers, timeZoneNames);
L10n.load({
    'fr-CH': {
        'schedule': {
            'day': 'journée',
            'week': 'La semaine',
            'workWeek': 'Semaine de travail',
            'month': 'Mois',
            'today': 'Aujourd`hui'
        }
    }
});

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' locale='fr-CH' [selectedDate]="selectedDate" [eventSettings]="eventSettings" [views]='views'></ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

> Note: To import the required cultures from the installed location to `app.component.ts` file as given in the following code example.

```typescript
//import the loadCldr from ej2-base
import { loadCldr} from '@syncfusion/ej2-base';
import * as numberingSystems from 'cldr-data/supplemental/numberingSystems.json';
import * as gregorian from 'cldr-data/main/fr-CH/ca-gregorian.json';
import * as numbers from 'cldr-data/main/fr-CH/numbers.json';
import * as timeZoneNames from 'cldr-data/main/fr-CH/timeZoneNames.json';

// Angular CLI 8.0 and above versions
loadCldr(numberingSystems['default'], gregorian['default'], numbers['default'], timeZoneNames['default']);

// Angular CLI 8.0 below versions
loadCldr(numberingSystems, gregorian, numbers, timeZoneNames);
```

## Displaying Scheduler in RTL mode

The Scheduler layout and its behavior can be changed as per the common RTL (Right to Left) conventions by setting `enableRtl` to `true`. By doing so, the Scheduler will display its usual layout from right to left. It's default value is `false`.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [enableRtl]='enableRtl'
  [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings'></ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public enableRtl: boolean = true;
    public views: Array<string> = ['Day', 'Week', 'WorkWeek'];
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## See Also

* [How to change first day of the week in the Scheduler](./working-days/#setting-start-day-of-the-week)