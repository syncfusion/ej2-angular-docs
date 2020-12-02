---
title: "Customization"
component: "Calendar"
description: "Calendar gives complete control to the user to customize overall appearance of the calendar in their application."
---

# Customization

Calendar allows you to customize the entire appearance by
using the custom CSS and
[`renderDayCell`](../api/calendar/renderDayCellEventArgs#renderdaycelleventargs)
 event
to customize the each day cell.

This following section demonstrates how to disable, highlights the specific dates in the Calendar.

## Disable Weekends

You can disable the weekends of every month in a Calendar by using the
[`renderDayCell`](../api/calendar/renderDayCellEventArgs#renderdaycelleventargs)
event. The `isDisabled` argument from this event allows you to define whether the
 date to be disabled or not.

> Set
[`isDisabled`](../api/calendar/renderDayCellEventArgs#renderdaycelleventargs)
to true to disable the date value.

The following example demonstrates how to disable weekends of every month.

{% tab template="calendar/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
         <!-- Bind renderDayCell event to customize and disable the day cell. --->
        <ejs-calendar [value]='dateValue' (renderDayCell)='disabledDate($event)'></ejs-calendar>
        `
})

export class AppComponent {
    public dateValue: Date = new Date();
    constructor() {
    }
    disabledDate(args): void {
        if (args.date.getDay() === 0 || args.date.getDay() === 6) {
            //set 'true' to disable the weekends
            args.isDisabled = true;
        }
    }

}
```

{% endtab %}

## Day Cell Format

You can highlight the specific dates by adding the
custom CSS or element to the day cell by using
[`renderDayCell`](../api/calendar/renderDayCellEventArgs#renderdaycelleventargs).

Below is the list of classes that provides the flexible way to customize the Calendar component.

| **Class Name** | **Description** |
| --- | --- |
| e-calendar | Applied to Calendar. |
| e-header | Applied to header.|
| e-title |Applied to title. |
| e-icon-container | Applied to previous and next icon container.|
| e-prev |  Applied to previous icon.|
| e-next | Applied to next icon.|
| e-weekend | Applied to weekend dates.|
| e-other-month |  Applied to other month dates.|
| e-day | Applied to each day cell.|
| e-selected | Applied to selected dates.|
| e-disabled | Applied to disabled dates.|

The following example highlights the world health date (7th April every year)
and world forest day (21st March every year) in a Calendar by using the
custom icon and tooltip.

{% tab template="calendar/highlight", sourceFiles="app/**/*.ts,styles.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template: `
        <!-- To customize day calendar appearance -->
        <!-- Refer the "special,highlight-day" class details in "styles.css"-->
        <ejs-calendar [value]='dateValue' (renderDayCell)='customDates($event)'></ejs-calendar>
        `
})

export class AppComponent {
    public dateValue: Date = new Date('3/7/2017');
    constructor() {
    }
    customDates(args): void {
         let span: HTMLElement;
    //defines the custom HTML element to be added.
    span = document.createElement('span');
    //Use "e-icons" class name to load Essential JS 2 built-in icons.
    span.setAttribute('class', 'e-icons highlight-day');
    if (+args.date.getDate() === 7 && +args.date.getMonth() == 3) {
        //append the span element to day cell.
        args.element.appendChild(span);
        //set the custom tooltip to the special dates.
        args.element.setAttribute('title', 'World health day!');
        //Use "special" class name to highlight the special dates, which you can refer in "styles.css".
        args.element.className = 'special';
    }
    if (+args.date.getDate() === 21 && +args.date.getMonth() == 2) {
        args.element.appendChild(span);
        args.element.className = 'special';
        //set the custom tooltip to the special dates.
        args.element.setAttribute('title', 'World forest day');
    }
    }
}
```

{% endtab %}

## Highlight Weekends

You can highlight the weekends of every month in a Calendar by using the
[`renderDayCell`](../api/calendar/renderDayCellEventArgs#renderdaycelleventargs)
event. The following example demonstrates how to highlights the weekends of every month.

{% tab template="calendar/highlight-weekend", sourceFiles="app/**/*.ts,styles.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
         <!-- Bind renderDayCell event to customize and highlight the weekend of every month. --->
        <ejs-calendar [value]='dateValue' (renderDayCell)='highlightWeekend($event)'></ejs-calendar>
        `
})

export class AppComponent {
    public dateValue: Date = new Date();
    constructor() {
    }
    highlightWeekend(args): void {
        if (args.date.getDay() === 0 || args.date.getDay() === 6) {
            // To highlight the week end of every month
           args.element.classList.add('e-highlightweekend');
        }
    }

}
```

{% endtab %}

## See Also

* [Add the external button in the Calendar popup](./how-to/set-clear-button-in-calendar)
* [How to skip a month in Calendar](./how-to/skip-a-month-in-calendar)
* [How to change the first day of week](./how-to/change-the-first-day-of-week)
* [How to customize the Calendar day header](./how-to/customize-the-calendar-day-header)