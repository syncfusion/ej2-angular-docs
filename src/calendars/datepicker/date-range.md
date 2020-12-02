---
title: "Choose a date in range"
component: "DatePicker"
description: "Date picker has `min` and `max` properties which restricts the user from selecting a value out of given min/max date range"
---

# Date Range

You can restrict the user to select the date
from the specified range of dates by using the
[`min`](../api/datepicker#min)
  and
[`max`](../api/datepicker#max) properties.

When the min and max properties are configured and the selected date value is out-of-range or
invalid, then the model value will be set to `out of range` date value or `null` respectively
with highlighted `error` class to indicates the date is out of range or invalid.

The below example demonstrates the Calendar to select a date within a range from 1 to 27 in a month.

{% tab template="datepicker/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <ejs-datepicker [value]='dateValue' [min]='minDate' [max]='maxDate'></ejs-datepicker>
        `
})
export class AppComponent {
    public today: Date = new Date();
    public currentYear: number = this.today.getFullYear();
    public currentMonth: number = this.today.getMonth();
    public currentDay: number = this.today.getDate();
    public dateValue: Object = new Date(new Date().setDate(14));
    public minDate: Object = new Date(this.currentYear, this.currentMonth, 1);
    public maxDate: Object =  new Date(this.currentYear, this.currentMonth, 27);
    constructor() {
    }
}

```

{% endtab %}