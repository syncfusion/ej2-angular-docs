---
title: "Recurrence Editor | Angular Scheduler"
component: "Scheduler"
description: "This section demonstrates the options available in recurrence editor and how to use its available methods separately in an application."
---

# Recurrence editor

The Recurrence editor is integrated into Scheduler editor window by default, to process the recurrence rule generation for events. Apart from this, it can also be used as an individual component referring from the Scheduler repository to work with the recurrence related processes.

> All the valid recurrence rule string mentioned in the [iCalendar](https://tools.ietf.org/html/rfc5545#section-3.3.10) specifications are applicable to use with the recurrence editor.

## Customizing the repeat type option in editor

By default, there are 5 types of repeat options available in recurrence editor such as,

* Never
* Daily
* Weekly
* Monthly
* Yearly

It is possible to customize the recurrence editor to display only the specific repeat options such as `Daily` and `Weekly` options alone by setting the appropriate `frequencies` option.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component, ViewChild} from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService, PopupOpenEventArgs, ScheduleComponent } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule #scheduleObj width='100%' height='550px' [selectedDate]='selectedDate'
  [eventSettings]='eventSettings' (popupOpen)='onPopupOpen($event)'>
  </ejs-schedule>`
})
export class AppComponent {
  @ViewChild('scheduleObj')
  public scheduleObj: ScheduleComponent;
  public selectedDate: Date = new Date(2018, 1, 15);
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
  onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type == 'Editor') {
        (<any>this.scheduleObj.eventWindow).recurrenceEditor.frequencies = ['daily', 'weekly'];
    }
  }
}
```

{% endtab %}

The other properties available in recurrence editor are tabulated below,

| Properties | Type | Description |
|------------|------|-------------|
| firstDayOfWeek | number | Sets the first day of the week on recurrence editor.|
| startDate | Date | Sets the start date from which date the recurrence event starts. |
| dateFormat | string | Sets the specific date format on recurrence editor.|
| locale | string | Sets the locale to be applied on recurrence editor.|
| cssClass | string | Allows styling to be applied on recurrence editor with custom class names.|
| enableRtl | boolean | Allows recurrence editor to render in RTL mode.|
| minDate | Date | Sets the minimum date on recurrence editor.|
| maxDate | Date | Sets the maximum date on recurrence editor.|
| value | string | Sets the recurrence rule value on recurrence editor. |
| selectedType | number | Sets the specific repeat type on the recurrence editor.|

## Accessing the recurrence rule string

The recurrence rule is usually generated based on the options selected from the recurrence editor and also it follows the [`iCalendar`](https://tools.ietf.org/html/rfc5545#section-3.3.10) specifications. The generated recurrence rule string is a valid one to be used with the Scheduler event’s recurrence rule field.

There is a `change` event available in recurrence editor, that triggers on every time the fields of recurrence editor tends to change. Within this event argument, you can access the generated recurrence value through the `value` option as shown in the following code example.

{% tab template="schedule/recur-editor", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component} from '@angular/core';
import { RecurrenceEditorChangeEventArgs } from '@syncfusion/ej2-angular-schedule';

@Component({
  selector: 'app-root',
  // specifies the template string for the Schedule component
  template: `<div style="padding-bottom:15px;">
            <label id="rule-label">Rule Output</label>
            <div class="rule-output-container">
                <div id="rule-output">Select Rule</div>
            </div>
        </div>
        <div id="RecurrenceEditor">
        <ejs-recurrenceeditor (change)="onChange($event)"></ejs-recurrenceeditor>
        </div>`
})
export class AppComponent {
  onChange(args: RecurrenceEditorChangeEventArgs): void {
    let outputElement: HTMLElement = <HTMLElement>document.querySelector('#rule-output');
    if(args.value == "") {
        outputElement.innerText = 'Select Rule';
    } else {
        outputElement.innerText = args.value;
    }
  }
}
```

{% endtab %}

## Set specific value on recurrence editor

It is possible to display the recurrence editor with specific options loaded initially, based on the rule string that we provide. The fields of recurrence editor will change its values accordingly, when we provide a particular rule through the `setRecurrenceRule` method.

{% tab template="schedule/recur-editor", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { isNullOrUndefined } from '@syncfusion/ej2-base';
import { RecurrenceEditorChangeEventArgs } from '@syncfusion/ej2-angular-schedule';

@Component({
    selector: 'app-root',
    // specifies the template string for the Schedule component
    template: `<div class="content-wrapper recurrence-editor-wrap">
  <div style="padding-bottom:15px;">
      <label>Rule Output</label>
      <div class="rule-output-container">
          <div id="rule-output">FREQ=DAILY;INTERVAL=2;COUNT=8</div>
      </div>
  </div>
  <ejs-recurrenceeditor (change)="onChange($event)" value="FREQ=DAILY;INTERVAL=2;COUNT=8"></ejs-recurrenceeditor>
</div>`
})
export class AppComponent {
    public onChange(args: RecurrenceEditorChangeEventArgs): void {
        let outputElement: HTMLElement = document.querySelector('#rule-output') as HTMLElement;
        if (!isNullOrUndefined(args.value)) {
            outputElement.innerText = args.value;
        }
    }
}
```

{% endtab %}

## Recurrence date generation

You can parse the `recurrenceRule` of an event to generate the date instances on which that particular event is going to occur, using the `getRecurrenceDates` method. It generates the dates based on the `recurrenceRule` that we provide. The parameters to be provided for `getRecurrenceDates` method are as follows.

| Field name | Type | Description |
|------------|------|-------------|
| `startDate` | Date| Appointment start date. |
| `rule` | String| Recurrence rule present in an event object. |
| `excludeDate` | String | Date collection (in ISO format) to be excluded. It is **optional**. |
| `maximumCount` | Number | Number of date count to be generated. It is **optional**. |
| `viewDate` | Date | Current view range's first date. It is **optional**. |

{% tab template="schedule/recur-editor", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { RecurrenceEditor } from '@syncfusion/ej2-angular-schedule';
import { createElement } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the Schedule component
    template: `<div style="padding-bottom:15px;">
            <label id="rule-label">Date Collections</label>
            <div class="rule-output-container">
                <div id="rule-output"></div>
            </div>
        </div>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        let outputElement: HTMLElement = <HTMLElement>document.querySelector('#rule-output');
        let labelElement: HTMLElement = <HTMLElement>document.querySelector('#rule-label');
        let recObject: RecurrenceEditor = new RecurrenceEditor();
        let dates: number[] = recObject.getRecurrenceDates(new Date(2018, 0, 7, 10, 0), 'FREQ=DAILY;INTERVAL=1', '20180108T114224Z,20180110T114224Z', 4, new Date(2018, 0, 7));
        for (let i: number = 0; i < dates.length; i++) {
            outputElement.appendChild(createElement('div', { innerHTML: new Date(dates[i]).toString() }));
        }
    }
}
```

{% endtab %}

> Above example will generate two dates January 7, 2018 & January 9 2018 by excluding the in between dates January 8 2018 & January 10 2018, since those dates were given in the exclusion list. Generated dates can then be utilised to create appointments.

## Recurrence date generation in server-side

It is also possible to generate recurrence date instances from server-side by manually referring the `RecurrenceHelper` class, which is specifically written and referred from application end to handle this date generation process.

> Refer [here](https://www.syncfusion.com/kb/10009/how-to-parse-the-recurrencerule-at-server-side) for the step by step procedure to achieve date generation in server-side.

## Restrict date generation with specific count

In case, if the rule is given in "NEVER ENDS" category, then you can mention the maximum count when you actually want to stop the date generation starting from the provided start date. To do so, provide the appropriate `maximumCount` value within the `getRecurrenceDates` method as shown in the following code example.

{% tab template="schedule/recur-editor", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { RecurrenceEditor } from '@syncfusion/ej2-angular-schedule';
import { createElement } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the Schedule component
    template: `<div style="padding-bottom:15px;">
            <label id="rule-label">Date Collections</label>
            <div class="rule-output-container">
                <div id="rule-output"></div>
            </div>
        </div>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        let outputElement: HTMLElement = <HTMLElement>document.querySelector('#rule-output');
        let labelElement: HTMLElement = <HTMLElement>document.querySelector('#rule-label');
        let recObject: RecurrenceEditor = new RecurrenceEditor();
        let dates: number[] = recObject.getRecurrenceDates(new Date(2018, 0, 7, 10, 0), 'FREQ=DAILY;INTERVAL=1; COUNT=30', '20180108T114224Z,20180110T114224Z', 10, new Date(2018, 0, 7));
        for (let i: number = 0; i < dates.length; i++) {
            outputElement.appendChild(createElement('div', { innerHTML: new Date(dates[i]).toString() }));
        }
    }
}
```

{% endtab %}