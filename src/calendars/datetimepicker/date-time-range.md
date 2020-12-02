---
title: "Date Time Range"
component: "DateTimePicker"
description: "Date time picker has `min` and `max` properties which restricts the user from selecting a value out of given min/max datetime range"
---

# DateTime Range

DateTimePicker provides an option to select a date and time value within a specified range
by using the [`min`](../api/datetimepicker#min)
and [`max`](../api/datetimepicker#max)properties.
Always the min value has to be lesser than the max value.

When the min and max properties are configured and the selected datetime value is out-of-range
or invalid, then the model value will be set to `out of range` datetime value or `null`
respectively with highlighted `error` class to indicates the datetime is out of range or invalid.

The value property depends
on the min/max with respect to [`strictMode`](./strict-mode/) property.

The below example allows selecting a
date within the range from 7th to 27th day in
a month.

{% tab template="datetimepicker/accessibility", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from "@angular/core";

@Component({
  selector: 'app-root',
  template: `<ejs-datetimepicker [value]='date' [min]='minDate' [max]='maxDate'></ejs-datetimepicker>`
})
export class AppComponent {
  public today: Date = new Date();
  public currentYear: number = this.today.getFullYear();
  public currentMonth: number = this.today.getMonth();
  public currentDay: number = this.today.getDate();
  public currentHour: number = this.today.getHours();
  public currentMinute: number = this.today.getMinutes();
  public currentSecond: number = this.today.getSeconds();
  public date: Date = new Date(new Date().setDate(14));
  public minDate: Date = new Date(this.currentYear,this.currentMonth,7,0,0,0);
  public maxDate: Date = new Date(this.currentYear,this.currentMonth,27,this.currentHour,this.currentMinute,this.currentSecond);
  constructor() {}
}

```

{% endtab %}

> If the value of `min` or `max` properties
changed through code behind, then you have to
update the `value` property to set within the
range.
