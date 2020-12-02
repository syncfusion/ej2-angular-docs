---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Two-way binding

The following example demonstrates how to achieve **two-way binding** by binding the **value** to the first Calendar component by using property binding and binding the model data using **ngModel** by using model binding to the Calendar component. The **value** of the Calendar will get change, when their is any change in the property value or model value.

> The two-way binding can also be achieved only by using **property binding** or **model binding** in the Calendar component.

{% tab template="calendar/two-way", isDefaultActive = "true", sourceFiles="app/**/*.ts,styles.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { CalendarComponent } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    template: `
        <!-- two-way binding using the value binding and model binding in the Calendar --->
        <ejs-calendar id="firstcalendar" #ejCalendar [(value)]='value'></ejs-calendar>
        <ejs-calendar id="secondcalendar" #ejCalendars [(ngModel)]='value'></ejs-calendar>
        `
})
export class AppComponent {
    value: Date;
    constructor() {
        this.value = new Date('1/1/2020');
    }
}

```

{% endtab %}
