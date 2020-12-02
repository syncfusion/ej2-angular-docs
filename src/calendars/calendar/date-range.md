---
title: "Date Range"
component: "Calendar"
description: "Calendar has `min` and `max` properties which restricts the user from selecting a value out of given min/max date range"
---

# Date Range

You can restrict the user to select the date from a specified range of dates by utilizing the
[`min`](../api/calendar#min)
  and
  [`max`](../api/calendar#max)
  properties.  Always the min date has to be lesser than the max date.

The below example allows you to select a
date within a range from 7th to 27th days in
a month.

{% tab template="calendar/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <!--Sets the value, min and max -->
        <ejs-calendar [value]='dateValue' [min]='minDate' [max]='maxDate'></ejs-calendar>
        `
})
export class AppComponent {
    public today: Date = new Date();
    public currentYear: number = this.today.getFullYear();
    public currentMonth: number = this.today.getMonth();
    public currentDay: number = this.today.getDate();
    public dateValue: Object = new Date(new Date().setDate(14));
    public minDate: Object = new Date(this.currentYear, this.currentMonth, 7);
    public maxDate: Object =  new Date(this.currentYear, this.currentMonth, 27);
    constructor() {
    }
}

```

{% endtab %}

> If the value of `min` or `max` properties changed
through code behind, then you have to update the `value`
property to set within the range. Or else, if the value is out of specified date range and less than `min` date, value property will
be updated with min date or the value is higher than max date, value property will be updated with `max` date.