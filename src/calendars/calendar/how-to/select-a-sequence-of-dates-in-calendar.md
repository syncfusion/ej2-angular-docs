---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Select a sequence of dates in Calendar

The following example demonstrates how to select the week dates of chosen date in the Calendar using [`values`](../../api/calendar#values) property, when [`isMultiSelection`](../../api/calendar#ismultiselection) property is enabled. Methods of Moment.js is used in this sample for calculating the start and end of week from the selected date.

{% tab template="calendar/how-to-multiselect", isDefaultActive = "true", sourceFiles="app/**/*.ts,styles.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { CalendarComponent } from '@syncfusion/ej2-angular-calendars';
import moment from 'moment';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template: `
        <!-- Rendering the Calendar with Multi selection option--->
        <div class="wrapelement">
            <ejs-calendar #ejCalendar id="calendar" isMultiSelection='true' (change)="onChange($event)"></ejs-calendar>
            </div>
            <div class='btncontainer e-btn-group e-vertical'>
            <input type="radio" id="workweek" name="week" value="workweek" (click)="workWeek()" />
            <label class="e-btn" for="workweek">Work Week</label>
            <input type="radio" id="week" name="week" value="week" (click)="week()"/>
            <label class="e-btn" for="week">Week</label>
            </div>
        `
})
export class AppComponent {
    @ViewChild('ejCalendar')
    public CalendarInstance: CalendarComponent;
    /*selected current week dates when click the button*/
    workWeek() {
        if (this.CalendarInstance.element.classList.contains('week')) {
            this.CalendarInstance.element.classList.remove('week')
        }
        this.CalendarInstance.element.classList.add('workweek');
    }

    week() {
        if (this.CalendarInstance.element.classList.contains('workweek')) {
            this.CalendarInstance.element.classList.remove('workweek')
        }
        this.CalendarInstance.element.classList.add('week');
    }

    onChange(args) {
        var startOfWeek = moment(args.value).startOf('week');
        var endOfWeek = moment(args.value).endOf('week');
        if (this.CalendarInstance.element.classList.contains('workweek')) {
            getWeekArray(startOfWeek.day(1), endOfWeek.day(5), this);
        } else if (this.CalendarInstance.element.classList.contains("week")) {
            getWeekArray(startOfWeek, endOfWeek, this);
        }
    }

    getWeekArray(startOfWeek, endOfWeek, obj) {
        var days = [];
        var day = startOfWeek;
        while (day <= endOfWeek) {
            days.push(day.toDate());
            day = day.clone().add(1, 'd');
        }
        obj.CalendarInstance.values = days;
    }
}

```

{% endtab %}
